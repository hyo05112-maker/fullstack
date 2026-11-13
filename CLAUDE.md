cat > CLAUDE.md << 'EOF'
# 해커톤 프로젝트 (4시간)
동작하는 데모가 최우선이다. 과한 추상화와 리팩터링은 하지 않는다.

## 구성
- backend/: Spring Boot 4, Java 17, Gradle, JPA + MyBatis, H2
- frontend/: React 19 (Vite)
- 배포: Render (backend는 Docker, frontend는 Static Site)

## 작업 분담
- backend/ 아래 Java 코드 작업은 backend 에이전트에게 맡긴다.
- frontend/ 아래 작업은 frontend 에이전트에게 맡긴다.
- 에이전트는 자기 폴더만 수정한다.

## 공통 약속 (여기에만 적는다)
- API 경로: /api/{기능}/...
- 오류 응답: HTTP 상태코드 + {"message": "..."}
- backend 포트: PORT 환경변수, 기본 8080
- 로컬 개발: frontend는 Vite 프록시로 /api를 localhost:8080에 넘긴다.
- 배포 환경: 프록시가 없으므로 frontend는 VITE_API_URL을 앞에 붙인다. 로컬에서는 비워 둔다.
- CORS: backend는 FRONTEND_URL 환경변수로 허용한다.
- 새 의존성은 이유를 먼저 알리고 승인받은 뒤 추가한다. 추가 전 build.gradle / package.json을 확인한다.

## API 명세 주고받기
- backend는 API를 만들면 요청·응답 예시를 한 줄씩 알린다.
- frontend는 API를 쓰기 전에 backend의 controller와 dto를 Read로 읽고 필드 이름을 맞춘다.

## 테스트
- 테스트 코드는 작성하지 않는다. 마지막 점검은 사용자가 요청할 때 qa 에이전트가 한다.
- BackendApplicationTests는 DB 없이 실패한다. 고치지 말고 빌드는 -x test로 한다.