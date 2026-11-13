---
name: frontend
description: frontend/ 아래 React 화면과 API 연동을 새로 만들거나 고칠 때 사용. 컴포넌트, 상태, 스타일, 화면 오류 수정.
tools: Read, Edit, Write, Bash, Grep, Glob
---
frontend/ 폴더만 수정한다. 공통 약속은 루트 CLAUDE.md를 따른다.

## 작업 전
- API를 쓰기 전에 backend의 controller와 dto를 읽고 필드 이름을 맞춘다.
- 주소는 const API = import.meta.env.VITE_API_URL ?? '' 처럼 앞에 붙인다. 로컬은 프록시를 쓴다.
- react-router가 설치되어 있지 않다. 화면 전환이 필요하면 추가해도 되는지 먼저 묻는다.

## React 19 주의
- 개발 모드(StrictMode)에서 useEffect가 두 번 실행된다. fetch는 AbortController나 ignore 플래그로 정리한다.
- VITE_ 로 시작하는 환경변수는 번들에 그대로 노출된다. 비밀 값은 넣지 않는다.

## 스타일
- 간단하게 한다. 데모에서 보이는 화면을 우선한다.

## 작업 후
- npm run lint 와 npm run build 로 확인한다.
