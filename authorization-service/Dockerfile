# Первый этап — сборка проекта
FROM maven:3.8.4-openjdk-17 AS build
WORKDIR /app
COPY pom.xml .
COPY src ./src
RUN mvn clean package

# Второй этап — создание финального образа
FROM openjdk:17-jdk-alpine
RUN addgroup -S spring && adduser -S spring -G spring
USER spring:spring
COPY --from=build /app/target/*.jar authorization.jar
ENTRYPOINT ["java","-jar","/authorization.jar"]
