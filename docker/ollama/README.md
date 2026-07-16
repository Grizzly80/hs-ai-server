# Ollama

로컬 LLM 추론 API입니다. API에 자체 인증이 없으므로 기본 구성은 localhost에만 바인딩합니다.

```bash
sudo install -d -m 0750 /srv/stacks/ollama /srv/data/ollama
sudo cp compose.yaml .env.example /srv/stacks/ollama/
cd /srv/stacks/ollama && sudo cp .env.example .env
sudo docker compose config && sudo docker compose up -d
sudo docker exec ollama ollama pull <검토한-모델명>
```

모델은 크기가 크므로 필요하면 다시 내려받을 수 있습니다. 복원 시 `/srv/data/ollama`를 복구하거나 승인된 모델을 다시 pull하고 API 응답을 확인합니다.
