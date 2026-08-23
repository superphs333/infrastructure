# 운영 가이드

[← README로 돌아가기](../README.md)

## 관리 UI 접속

Nginx Proxy Manager 관리 UI는 공개 인터넷에 노출하지 않는다. `global-proxy/docker-compose.yml`의 관리 포트는 로컬 루프백에만 바인딩한다.

```yaml
ports:
  - "127.0.0.1:81:81"
```

관리 UI에 접속할 때는 SSH 터널을 사용한다.

```bash
ssh -L 8181:127.0.0.1:81 <server-ssh-user>@<global-proxy-server-ip-or-domain>
```

`<server-ssh-user>`는 `global-proxy`가 실행 중인 서버의 SSH 사용자이고, `<global-proxy-server-ip-or-domain>`은 해당 서버의 IP 또는 도메인이다. 이 명령은 로컬 PC의 `127.0.0.1:8181`을 `global-proxy` 서버 내부의 `127.0.0.1:81`로 연결한다.

터널 연결 후 로컬 브라우저에서 아래 주소로 접속한다.

```text
http://127.0.0.1:8181
```

## Windows PowerShell에서 접속

Windows PowerShell에서 OpenSSH 클라이언트가 설치되어 있는지 확인한다.

```powershell
ssh -V
```

명령이 동작하지 않으면 Windows 설정에서 `선택적 기능 > 기능 보기 > OpenSSH Client`를 설치한다.

PowerShell에서 아래 명령으로 SSH 터널을 연다.

```powershell
ssh -L 8181:127.0.0.1:81 <server-ssh-user>@<global-proxy-server-ip-or-domain>
```

예시는 아래와 같다.

```powershell
ssh -L 8181:127.0.0.1:81 ubuntu@203.0.113.10
```

SSH 키 파일을 직접 지정해야 하면 `-i` 옵션을 사용한다.

```powershell
ssh -i "$env:USERPROFILE\.ssh\id_ed25519" -L 8181:127.0.0.1:81 <server-ssh-user>@<global-proxy-server-ip-or-domain>
```

터널 명령을 실행한 PowerShell 창은 닫지 않는다. 로그인된 상태로 유지되어야 터널도 유지된다.

터널이 열린 상태에서 Windows 브라우저로 `http://127.0.0.1:8181`에 접속한다. 접속이 끝나면 PowerShell 창에서 `Ctrl+C`를 눌러 터널을 종료한다.

## 설정 검증

설정이 의도대로 해석되는지 확인한다.

```bash
docker compose -f global-proxy/docker-compose.yml config
```

서버에서 관리 포트가 루프백에만 바인딩되어 있는지 확인한다.

```bash
ss -ltnp | grep ':81'
```

추가 보안 원칙은 [보안 지침](security.md)을 확인한다.
