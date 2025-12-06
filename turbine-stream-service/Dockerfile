# FROM java:8-jre
# MAINTAINER Chi Dov <d.chiproeng@gmail.com>

# ADD ./target/turbine-stream-service.jar /app/
# CMD ["java", "-Xmx200m", "-jar", "/app/turbine-stream-service.jar"]

# EXPOSE 8989


FROM maven:3.8.7-openjdk-8 AS build
WORKDIR /app
COPY pom.xml .
COPY src ./src
RUN mvn clean package -DskipTests
FROM gcr.io/distroless/java:8
WORKDIR /app
COPY --from=build /app/target/turbine-stream-service.jar /app/turbine-stream-service.jar
EXPOSE 8989
CMD ["turbine-stream-service.jar"]
