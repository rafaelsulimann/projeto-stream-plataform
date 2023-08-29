FROM maven:3.8.4-openjdk-17-slim AS builder
WORKDIR /app
COPY . .
RUN mvn clean package

FROM openjdk:17-slim
WORKDIR /app
ENV SPRING_CLOUD_CONFIG_DISCOVERY_SERVICE_ID=config-server
ENV CONFIG_SERVER_USERNAME=configserver
ENV CONFIG_SERVER_PASSWORD=1234567
ENV CONFIG_SERVER_HOST=host.docker.internal
ENV SERVICE_REGISTRY_USERNAME=serviceregistry
ENV SERVICE_REGISTRY_PASSWORD=1234567
ENV EUREKA_CLIENT_SERVICE_URL_DEFAULT_ZONE=host.docker.internal
COPY --from=builder /app/target/api-gateway-0.0.1-SNAPSHOT.jar ./api-gateway.jar
EXPOSE 8888
ENTRYPOINT ["java", "-jar", "/app/api-gateway.jar"]