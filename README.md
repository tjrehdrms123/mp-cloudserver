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

## Config Notes
 - `Reverse-proxy`란 클라이언트 요청을 대신 받아 내부 서버로 전달 해주는 것이다
   - 사용자 > nginx > 웹서버(Express) 해당 Workflow처럼 중간에 nginx가 껴있어서 많은 이점이 있다 아래는 해당 설정이다
 ```
 upstream docker-server {
     server server:3601;
 }
 ```
 - 기존에 docker-compose.yml 파일 server 컨테이너에 `ports`가 아닌 `expose`로 되어 있었다 두개의 차이점은 `ports`는 퍼블릭 엑세스 설정이고 `expose`는 퍼블릭 엑세스를 제한하고 프라이빗 즉 컨테이너끼리 통신이 가능하다
 - RDS ParseDashboard AWS RDS Postgres DB "does not exist" when connecting with PG 직접 `Create Database`해줘야된다

## CMD Notes
- `up`
> 실행 로그가 출력되고, 컴포즈 파일에 정의된 모든 컨테이너가 생성 및 실행 됩니다

- `up -d`
> 실행 로그가 출력되지 않고, 백그라운드에서 생성 및 실행 됩니다

- `down`
> 컨테이너 중지 후 삭제

- `logs -t -f <name-of-service>`
> 백그라운드로 실행 시 로그 출력 

- `start,stop <name-of-service>`
> 컨테이너 실행, 중지

- `docker exec -it <name-of-service> /bin/sh`
> 컨테이너 내부 접속