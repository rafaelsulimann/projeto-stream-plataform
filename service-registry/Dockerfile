FROM maven:3.8.4-openjdk-17-slim AS builder
WORKDIR /app
COPY . .
RUN mvn clean package

FROM openjdk:17-slim
WORKDIR /app
ENV SERVICE_REGISTRY_USERNAME=serviceregistry
ENV SERVICE_REGISTRY_PASSWORD=1234567
ENV EUREKA_CLIENT_SERVICE_URL_DEFAULT_ZONE=host.docker.internal
COPY --from=builder /app/target/service-registry-0.0.1-SNAPSHOT.jar ./service-registry.jar
EXPOSE 8761
ENTRYPOINT ["java", "-jar", "/app/service-registry.jar"]