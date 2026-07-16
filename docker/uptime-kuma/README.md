# Uptime Kuma

HS-AI-SERVER의 서비스 가용성을 확인하는 자체 호스팅 모니터링 대시보드입니다.

## 준비 및 실행

Compose 파일은 `/srv/stacks/uptime-kuma`, 영속 데이터는 `/srv/data/uptime-kuma`에 둡니다. 로컬 파일시스템을 사용하며 Docker 소켓은 연결하지 않습니다.

```bash
sudo install -d -m 0755 /srv/stacks/uptime-kuma /srv/data/uptime-kuma
sudo cp compose.yaml .env.example /srv/stacks/uptime-kuma/
cd /srv/stacks/uptime-kuma
sudo cp .env.example .env
sudo chmod 600 .env
sudo docker compose config
sudo docker compose up -d
```

기본 접속 주소는 `http://localhost:3001`입니다. 최초 접속 시 관리자 계정을 설정합니다. 실제 자격 증명은 Git 파일에 기록하지 않습니다.

## 운영 및 복원

컨테이너 로그는 파일당 10MB, 최대 3개로 회전합니다. 복원 시 컨테이너를 중지한 상태에서 `/srv/data/uptime-kuma`를 복구한 뒤 Compose 구성을 검증하고 다시 시작합니다.
