# 최초 설치

[← README로 돌아가기](../README.md)

설치 전에 [사전 요구사항](prerequisites.md)을 확인한다.

## 저장소 준비

저장소를 받은 뒤 터미널에서 다음 명령을 실행한다.

```bash
cd infrastructure
mkdir services
```

## 공용 네트워크와 global-proxy 실행

```bash
cd global-proxy
docker compose version
docker --version
docker compose pull
docker network inspect proxy-nw >/dev/null 2>&1 || docker network create proxy-nw
docker compose up -d
docker network ls | grep proxy-nw
```

`proxy-nw`는 `global-proxy`와 각 서비스 컨테이너가 함께 사용하는 공용 Docker 네트워크이다. `global-proxy/docker-compose.yml`에서 `external: true`로 참조하므로, 네트워크가 없으면 `docker compose up -d`가 실패한다.

위 명령은 이미 `proxy-nw`가 있으면 그대로 사용하고, 없을 때만 새로 만든다.

## 개별 서비스 설치

`services` 디렉터리로 들어간 뒤 각 프로젝트를 Git으로 내려받는다.

현재 포함된 서비스와 각 서비스의 설치 방법은 루트 README의 [포함 서비스](../README.md#포함-서비스)에서 확인한다.
