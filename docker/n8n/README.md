# n8n

워크플로 자동화 서비스입니다. 외부 노출 시 TLS 프록시 또는 Cloudflare Tunnel을 사용하세요.

```bash
sudo install -d -m 0750 -o 1000 -g 1000 /srv/data/n8n
sudo install -d -m 0750 /srv/stacks/n8n
sudo cp compose.yaml .env.example /srv/stacks/n8n/
cd /srv/stacks/n8n && sudo cp .env.example .env
# 호스트명, 웹훅 URL, 고정 암호화 키 설정
sudo docker compose config && sudo docker compose up -d
```

복원에는 `/srv/data/n8n`과 기존 `N8N_ENCRYPTION_KEY`가 모두 필요합니다. 키를 잃으면 저장된 자격 증명을 해독할 수 없습니다.
