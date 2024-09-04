FROM gradle:8.5-jdk as builder

WORKDIR /app
COPY ./ ./
RUN gradle clean build --no-daemon

FROM openjdk:17-jdk-slim-buster
WORKDIR /app
COPY --from=builder /app/build/libs/*.jar app.jar

EXPOSE 8080
USER nobody
#ENTRYPOINT ["java", "-jar", "app.jar"]
ENTRYPOINT ["java", "-agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=*:5005", "-jar", "app.jar"]
