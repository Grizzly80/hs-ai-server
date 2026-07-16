# Homepage

서비스 대시보드입니다. 설정 YAML은 `/srv/data/homepage/config`에 둡니다.

```bash
sudo install -d -m 0750 /srv/stacks/homepage /srv/data/homepage/config
sudo cp compose.yaml .env.example /srv/stacks/homepage/
cd /srv/stacks/homepage && sudo cp .env.example .env
sudo docker compose config && sudo docker compose up -d
```

복원 시 config 디렉터리를 복구합니다. 위젯 API 키는 설정 파일에 직접 저장하지 말고 지원되는 환경 변수 또는 별도 비밀 주입 방식을 사용하세요.
