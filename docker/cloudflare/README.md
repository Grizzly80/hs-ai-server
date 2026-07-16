# Cloudflare Tunnel

Cloudflare의 원격 관리 터널 토큰으로 내부 서비스를 공개합니다. 토큰은 `.env`에만 저장합니다.

```bash
sudo install -d -m 0750 /srv/stacks/cloudflare /srv/data/cloudflare
sudo cp compose.yaml .env.example /srv/stacks/cloudflare/
cd /srv/stacks/cloudflare && sudo cp .env.example .env
# Cloudflare 대시보드에서 발급한 터널 토큰 입력
sudo docker compose config && sudo docker compose up -d
```

이 모드는 원격 관리 구성을 사용하므로 영속 데이터가 필수는 아닙니다. 복원 시 터널을 다시 배포하거나 토큰을 회전하고 DNS 및 ingress 상태를 확인합니다.
