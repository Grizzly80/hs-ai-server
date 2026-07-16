# Portainer

Docker 관리 UI입니다. Docker 소켓 접근은 호스트 제어 권한과 동일하므로 관리자만 접근하게 하세요.

```bash
sudo install -d -m 0750 /srv/stacks/portainer /srv/data/portainer
sudo cp compose.yaml .env.example /srv/stacks/portainer/
cd /srv/stacks/portainer && sudo cp .env.example .env
sudo docker compose config && sudo docker compose up -d
```

복원 시 `/srv/data/portainer`를 되돌린 후 기동하고 관리자 로그인 및 엔드포인트 연결을 확인합니다.
