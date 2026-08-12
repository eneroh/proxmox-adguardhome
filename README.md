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
apt install -y docker-ce-cli
docker run hello-world
```
