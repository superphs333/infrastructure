# git으로 받고 나서 해야 할 것
터미널에서 명령어
```bash
cd infrastructure
mkdir services
cd global-proxy
docker compose version
docker --version
docker compose pull
docker network create proxy-nw
docker compose up -d
docker network ls | grep proxy-nw
```
그 후 services폴더로 들어가서 각각 프로젝트를 git으로 다운받는다.
