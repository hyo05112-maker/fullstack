# ---- build ----
FROM eclipse-temurin:17-jdk AS build
WORKDIR /app

# 의존성 레이어 캐시: 빌드 설정만 먼저 복사
COPY gradlew settings.gradle build.gradle ./
COPY gradle ./gradle
# Windows에서 CRLF로 체크아웃돼도 실행되도록
RUN sed -i 's/\r$//' gradlew && chmod +x gradlew \
 && ./gradlew dependencies --no-daemon > /dev/null 2>&1 || true

COPY src ./src
RUN ./gradlew bootJar -x test --no-daemon

# ---- run ----
FROM eclipse-temurin:17-jre
WORKDIR /app
COPY --from=build /app/build/libs/*.jar app.jar

# Render 무료 인스턴스(512MB) 메모리에 맞춤
ENV JAVA_TOOL_OPTIONS="-XX:MaxRAMPercentage=75 -XX:+UseSerialGC"
# Render는 PORT 환경변수를 주입한다 (application.yml의 server.port가 읽음)
EXPOSE 8080
ENTRYPOINT ["java", "-jar", "app.jar"]
