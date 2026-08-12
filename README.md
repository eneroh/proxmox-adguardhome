# proxmox-adguardhome

## System Requirements
Docker container - Ubuntu 24.04
<br>
<br>
**CPU:** 2 cores
<br>
**RAM:** 512MB
<br>
**Storage:** 5GB

## Procedure
1. Install Docker and Docker compose
```bash
apt update && apt install -y ca-certificates curl
install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
chmod a+r /etc/apt/keyrings/docker.asc
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  tee /etc/apt/sources.list.d/docker.list > /dev/null
apt update
apt install -y docker-ce-cli docker.io
docker run hello-world
```
2. Remove systemd-resolv from port 53, we need this port for dns traffic
```bash
sudo mkdir -p /etc/systemd/resolved.conf.d
printf "[Resolve]\nDNS=127.0.0.1\nDNSStubListener=no\n" | \
  sudo tee /etc/systemd/resolved.conf.d/adguardhome.conf
sudo mv /etc/resolv.conf /etc/resolv.conf.backup
sudo ln -s /run/systemd/resolve/resolv.conf /etc/resolv.conf
sudo systemctl reload-or-restart systemd-resolved
```
3. Check port 53 by inputting below command:
```bash
netstat -tulpn
```
<br>
Make sure port 53 is clear
4. 
