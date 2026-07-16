# Monitoring

Prometheus와 Grafana 기본 스택입니다. exporter 및 알림 구성은 운영 환경에 맞게 추가합니다.

먼저 `/srv/data/monitoring/prometheus/config/prometheus.yml`을 만듭니다.

```yaml
global:
  scrape_interval: 15s
scrape_configs:
  - job_name: prometheus
    static_configs:
      - targets: ["localhost:9090"]
```

```bash
sudo install -d -m 0750 /srv/stacks/monitoring
sudo install -d -m 0750 /srv/data/monitoring/{prometheus/config,prometheus/data,grafana}
sudo cp compose.yaml .env.example /srv/stacks/monitoring/
cd /srv/stacks/monitoring && sudo cp .env.example .env
# Grafana 관리자 비밀번호와 root URL 설정
sudo docker compose config && sudo docker compose up -d
```

복원 시 Prometheus 데이터는 선택적으로 복구하고 Grafana 데이터 및 프로비저닝 파일을 우선 복구합니다. 관리자 비밀번호를 회전하고 데이터 소스 및 대시보드를 확인합니다.
