# git으로 받고 나서 해야 할 것
터미널에서 명령어
cd infrastructue
mkdir services
cd grobal-proxy
docker compose version -- 확인
docker --version
docker compose pull
docker network create proxy-nw
docker compose up -d
docker network ls | grep proxy-nw -- 네트워크 존재 확인 



