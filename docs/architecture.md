# 아키텍처

[← README로 돌아가기](../README.md)

`global-proxy`는 서버의 공개 웹 진입점이다. 외부 사용자의 HTTP `:80` 요청과 HTTPS `:443` 요청은 먼저 `global-proxy-npm` 컨테이너로 들어오고, Nginx Proxy Manager의 도메인별 프록시 설정에 따라 `proxy-nw`에 연결된 서비스 컨테이너로 전달된다.

## 서버 구조

![global-proxy 서버 구조](assets/global-proxy-server-structure.svg)

## 외부 요청 흐름

```text
사용자 / 브라우저
  -> Host Server :80 / :443
  -> global-proxy-npm
  -> proxy-nw
  -> tipmarket-web / tiptipworld-web / devlog-app ...
  -> 서비스별 내부 네트워크
  -> app / db / redis 등
```

## Docker 네트워크 구성

서비스 컨테이너는 필요한 경우 두 종류의 네트워크를 함께 사용한다.

- `proxy-nw`: `global-proxy`가 접근하는 공용 진입 네트워크
- `서비스명_internal`: 각 서비스의 `app`, `web`, `db`, `redis` 같은 컨테이너가 서로 통신하는 전용 네트워크

외부 트래픽은 보통 `global-proxy-npm -> proxy-nw -> 서비스 웹 컨테이너`까지만 직접 들어오고, DB나 Redis는 서비스 내부 네트워크에만 둔다.

## 데이터 및 인증서 영속화

`global-proxy/docker-compose.yml`에서는 다음 디렉터리를 컨테이너에 마운트한다.

| 호스트 디렉터리 | 컨테이너 경로 | 저장 내용 |
| --- | --- | --- |
| `./data` | `/data` | Nginx Proxy Manager 설정과 사용자 정보 |
| `./letsencrypt` | `/etc/letsencrypt` | Let's Encrypt SSL 인증서 |

컨테이너를 다시 만들더라도 이 디렉터리를 유지하면 프록시 설정과 인증서를 계속 사용할 수 있다.
