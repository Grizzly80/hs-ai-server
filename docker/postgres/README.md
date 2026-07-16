# PostgreSQL

공용 PostgreSQL 인스턴스의 기본 구성입니다. 기본 포트는 localhost에만 바인딩됩니다.

```bash
sudo install -d -m 0750 /srv/stacks/postgres /srv/data/postgres
sudo cp compose.yaml .env.example /srv/stacks/postgres/
cd /srv/stacks/postgres && sudo cp .env.example .env
# .env의 POSTGRES_PASSWORD를 강한 임의 값으로 교체
sudo docker compose config && sudo docker compose up -d
```

백업은 `pg_dump`/`pg_dumpall`로 생성하고 암호화된 외부 저장소에 보관합니다. 복원은 동일한 주 버전의 빈 인스턴스에 `psql`로 논리 백업을 적용하는 방식을 권장합니다.
