# MP-CloudServer

## Installation

```
1)
 - mv ./docker-compose.yml ../
2)
cd ../mp-server
- npm install
3)
- cd ../mp-client
- npm install
4)
- cd ..
- docker-compose up -d
- docker-compose start web
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