# FROM java:8-jre
# MAINTAINER Alexander Lukyanchikov <sqshq@sqshq.com>

# ADD ./target/account-service.jar /app/
# CMD ["java", "-Xmx200m", "-jar", "/app/account-service.jar"]

# EXPOSE 6000

# ---------- Stage 1: Build ----------
FROM maven:3.8.8-eclipse-temurin-8 AS builder

WORKDIR /build

# Copy pom.xml and download dependencies (better caching)
COPY pom.xml .
RUN mvn dependency:go-offline -B

# Copy source and build
COPY src ./src
RUN mvn clean package -DskipTests


# ---------- Stage 2: Runtime (Distroless) ----------
FROM gcr.io/distroless/java8-debian11

WORKDIR /app

# Copy only the built JAR from builder stage
COPY --from=builder /build/target/account-service.jar app.jar

EXPOSE 6000

# Distroless images do NOT support shell form
ENTRYPOINT ["java", "-Xmx200m", "-jar", "/app/app.jar"]
