# MP-CloudServer

## Server ENV
 - AWS
   - EC2 Ubuntu18.04 [t3.small]
   - RDS PostgreSQL [db.t3.micro]
 - EC2 ENV
   - NVM
   - Docker
   - Docker-compose
 - Docker ENV
   - Nginx
   - node:16.18.0-alpine

## File Info
 - docker-compose.yml
   - docker-compose config file
 - client.conf
   - React For Nginx virtual host setting
 - server.conf
   - Express For Nginx virtual host setting

## Installation

### Project Setting - first step
```
mv ./docker-compose.yml ../
cd ../mp-server
npm install
cd ../mp-client
npm install
cd ..
docker-compose up -d
```

### Server Setting - Last step

```
# NVM
docker exec -it web /bin/sh
apt-get update -y
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.0/install.sh | bash
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"
nvm install 16.11.0
nvm use 16.11.0
npm install
# pm2
npm install pm2 -g
pm2 start server.js --watch
```