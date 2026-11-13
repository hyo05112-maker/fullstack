cat > .claude/agents/backend.md << 'EOF'
---
name: backend
description: backend/ 아래 Java 코드를 새로 만들거나 고칠 때 사용. API 추가, 엔티티·SQL 변경, 서버 오류와 DB 관련 오류 수정.
tools: Read, Edit, Write, Bash, Grep, Glob
---
backend/ 폴더만 수정한다. 공통 약속은 루트 CLAUDE.md를 따른다.

## 기술 기준
- Spring Boot 4, Java 17. jakarta.* 를 쓰고 javax.* 는 쓰지 않는다.
- Jackson 3 기준이다. 코드를 쓰기 전에 build.gradle에 있는 의존성만 쓴다.
- Lombok과 validation이 없으면 추가하기 전에 이유를 먼저 알린다. DTO는 record를 우선 쓴다.

## 패키지 구조 (필요한 것만 만든다)
org.scoula/domain/{기능}/
  controller/  요청·응답 처리만
  service/     비즈니스 로직
  mapper/      MyBatis. 복잡한 조회와 통계 SQL
  dto/         요청·응답 객체
  vo/          MyBatis 조회 결과 객체
  entity/, repository/  JPA. 단순 CRUD
- 같은 기능에서 JPA와 MyBatis를 섞더라도 service에서만 조합한다.
- 다른 기능의 데이터는 그 기능의 service를 호출한다. 다른 기능의 mapper와 repository는 직접 쓰지 않는다.
- SQL은 resources/mapper/{기능}/ 의 XML에 두고 namespace와 id를 Mapper 인터페이스와 맞춘다.

## 엔티티 규칙
- setter를 만들지 않는다. 변경은 의미 있는 메서드로 한다.
- 매개변수 없는 생성자는 protected로 둔다.
- 연관관계는 LAZY로 둔다.

## 작업 후
- ./gradlew bootJar -x test 로 빌드를 확인한다.
- 새 API마다 요청·응답 예시를 한 줄씩 알린다.
EOF