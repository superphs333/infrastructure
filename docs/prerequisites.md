# 사전 요구사항

[← README로 돌아가기](../README.md)

## Git 설치

```bash
# 패키지 목록 업데이트
sudo apt update

# Git 설치
sudo apt install git -y

# 설치 확인 및 버전 체크
git --version

# 사용자 이름 설정
git config --global user.name "YourName"

# 사용자 이메일 설정
git config --global user.email "your-email@example.com"

# 설정 확인
git config --list

# 기본 브랜치 설정
git config --global init.defaultBranch main
```

## Docker 설치

Docker 공식 저장소를 추가하기 위해 필요한 패키지를 먼저 설치한다.

```bash
# 필수 패키지 설치
sudo apt update
sudo apt install -y ca-certificates curl gnupg lsb-release

# Docker 공식 GPG 키 추가
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

# 저장소 설정
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/debian \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# Docker 엔진 설치
sudo apt update
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-compose-plugin

# sudo 없이 Docker를 사용하도록 현재 사용자를 docker 그룹에 추가
sudo usermod -aG docker $USER
```

## WSL2 설정

WSL2에서 Docker 서비스를 시작하고 실행 상태를 확인한다.

```bash
# Docker 서비스 시작
sudo service docker start

# 실행 확인
docker ps
```

자동 실행을 설정하려면 `/etc/wsl.conf`를 연다.

```bash
sudo nano /etc/wsl.conf
```

아래 내용을 추가한 뒤 WSL을 재시작한다.

```ini
[boot]
systemd=true
```
