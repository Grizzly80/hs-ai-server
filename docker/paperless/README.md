# Paperless-ngx

문서 수집·OCR·검색 서비스이며 전용 PostgreSQL과 Redis를 함께 실행합니다.

```bash
sudo install -d -m 0750 /srv/stacks/paperless
sudo install -d -m 0750 /srv/data/paperless/{postgres,redis,data,media,export,consume}
sudo cp compose.yaml .env.example /srv/stacks/paperless/
cd /srv/stacks/paperless && sudo cp .env.example .env
# DB 비밀번호, secret key, 공개 URL 설정
sudo docker compose config && sudo docker compose up -d
```

정기적으로 문서 export와 PostgreSQL 논리 백업을 함께 생성하세요. 복원 시 DB, data, media를 복구하고 기존 `PAPERLESS_SECRET_KEY`를 유지한 뒤 무결성을 확인합니다.
