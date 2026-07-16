# hs-ai-server

홈 서버에서 AI 및 자동화 서비스를 Docker Compose로 일관되게 운영하기 위한 인프라 저장소입니다. 이 저장소에는 배포 정의와 문서만 보관하며, 실제 데이터와 비밀값은 서버의 별도 경로에서 관리합니다.

## 디렉터리 구조

```text
hs-ai-server/
├── docker/     # 서비스별 Compose 정의, 환경 변수 예시, 운영 문서
├── docs/       # 공통 아키텍처 및 운영 문서
├── prompts/    # 버전 관리 가능한 AI 프롬프트
├── scripts/    # 배포·점검·복원 자동화 스크립트
└── backup/     # 백업 정책 및 복원 메타데이터(실제 백업 파일 제외)
```

각 서비스는 `docker/<service>/` 아래에 `compose.yaml`, `.env.example`, `README.md`를 둡니다. 운영 시 저장소의 서비스 디렉터리를 `/srv/stacks/<service>`로 배치하고, 영속 데이터는 `/srv/data/<service>`에 저장합니다.

## 배포

```bash
sudo install -d /srv/stacks/<service> /srv/data/<service>
sudo cp docker/<service>/compose.yaml docker/<service>/.env.example /srv/stacks/<service>/
cd /srv/stacks/<service>
sudo cp .env.example .env
sudo editor .env
sudo docker compose config
sudo docker compose up -d
```

서비스별 필수 디렉터리와 설정은 각 서비스의 README를 확인합니다.

## 복원 절차

1. 새 서버에 Docker Engine과 Compose 플러그인을 설치합니다.
2. 이 저장소를 복제하고 `/srv/stacks/<service>`에 필요한 Compose 파일을 배치합니다.
3. 비밀 관리 시스템이나 오프라인 백업에서 `.env`를 별도로 복원합니다.
4. 백업된 데이터를 `/srv/data/<service>`에 복원하고 소유권과 권한을 확인합니다.
5. 데이터베이스는 파일 복사보다 서비스별 논리 백업(`pg_dump` 등)을 우선 복원합니다.
6. `docker compose config`로 구성을 검증한 뒤 `docker compose up -d`를 실행합니다.
7. 컨테이너 상태, 로그, 서비스별 기능 및 백업 작업을 확인합니다.

## 보안 원칙

- 실제 비밀번호, 토큰, API 키, 인증서 개인 키를 Git에 저장하지 않습니다.
- 모든 `.env`는 무시하며 `.env.example`에는 안전한 자리표시자와 비민감 기본값만 둡니다.
- 외부 공개는 필요한 서비스에만 허용하고, 가능하면 Cloudflare Tunnel 또는 인증 프록시를 사용합니다.
- 컨테이너 이미지는 검토된 버전으로 고정하고 정기적으로 업데이트합니다.
- `/srv/data`와 백업 저장소의 접근 권한을 최소화하고 복원 테스트를 정기 수행합니다.
- Compose 렌더링 결과와 로그에 비밀값이 노출되지 않는지 배포 전에 확인합니다.

> 이 초기 구성은 안전한 출발점입니다. 운영 전 이미지 버전, 네트워크, 리소스 제한, 백업 및 접근 정책을 환경에 맞게 확정하세요.
