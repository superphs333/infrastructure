# 받기 전에 

1. git 설치
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

git config --global init.defaultBranch main
```

2. docker 설치
```bash

## 필수 패키지 설치 및 저장소 등록 (Docker 공식 저장소를 추가하기 위해 필요한 도구들을 먼저 설치)
sudo apt update
sudo apt install -y ca-certificates curl gnupg lsb-release

# Docker 공식 GPG 키 추가
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

# 저장소 설정
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/debian \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

## Docker 엔진 설치
sudo apt update
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-compose-plugin


## 사용자 권한 설정 (sudo 없이 Docker를 사용하기 위해 현재 사용자를 docker 그룹에 추가)
sudo usermod -aG docker $USER

## WSL2 에서 Docker 서비스 실행
# Docker 서비스 시작
sudo service docker start

# 실행 확인
docker ps

## 자동 실행 설정
sudo nano /etc/wsl.conf

# 아래 내용 추가
[boot]
systemd=true

# wsl 재시작 

```

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
