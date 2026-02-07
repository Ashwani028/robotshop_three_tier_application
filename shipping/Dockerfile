# Build stage: Maven + JDK included
FROM maven:3.9.3-eclipse-temurin-8 AS build
WORKDIR /opt/shipping

# Copy only pom.xml first for caching dependencies
COPY pom.xml .
RUN mvn dependency:resolve

# Copy source and build
COPY src ./src
RUN mvn package

# Runtime stage: lightweight JDK only
FROM eclipse-temurin:8-jdk-alpine
WORKDIR /opt/shipping

# Environment variables
ENV CART_ENDPOINT=cart:8080
ENV DB_HOST=mysql

# Copy the built JAR
COPY --from=build /opt/shipping/target/shipping-1.0.jar shipping.jar

# Run the service
CMD ["java", "-Xmn256m", "-Xmx768m", "-jar", "shipping.jar"]
