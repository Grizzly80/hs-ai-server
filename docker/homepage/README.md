# Homepage

HS-AI-SERVER의 운영 서비스에 접근하기 위한 정적 대시보드입니다. Docker 소켓은 연결하지 않습니다.

## 준비

운영 파일은 `/srv/stacks/homepage`, 설정은 `/srv/data/homepage`에 둡니다.

```bash
sudo install -d -m 0755 /srv/stacks/homepage /srv/data/homepage
sudo cp compose.yaml .env.example /srv/stacks/homepage/
sudo cp -R config/. /srv/data/homepage/
cd /srv/stacks/homepage
sudo cp .env.example .env
sudo chmod 600 .env
sudo docker compose config
sudo docker compose up -d
```

기본 접속 주소는 `http://localhost:3000`입니다. 원격 접속 전에 `.env`의 `HOMEPAGE_ALLOWED_HOSTS`에 Tailscale IP 또는 도메인을 추가합니다.

## 복원

`/srv/data/homepage`의 설정 파일을 복원하고 `.env`를 별도로 재작성한 뒤 `docker compose config`와 `docker compose up -d`를 실행합니다. 실제 비밀번호나 토큰은 Git 설정 예제에 넣지 않습니다.
