# ETAPA 1: Construcción
FROM maven:3.8.5-openjdk-17 AS builder
WORKDIR /app


COPY Springboot-API-REST-DESPACHO/pom.xml .
RUN mvn dependency:go-offline

COPY Springboot-API-REST-DESPACHO/src ./src
RUN mvn clean package -DskipTests

# ETAPA 2: Producción
FROM eclipse-temurin:17-jre-alpine
WORKDIR /app
COPY --from=builder /app/target/*.jar app.jar


RUN addgroup -S spring && adduser -S spring -G spring
USER spring:spring

EXPOSE 8080
CMD ["java", "-jar", "app.jar"]