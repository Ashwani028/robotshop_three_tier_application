FROM debian:10 AS build

RUN apt-get update && \
apt-get install -y --no-install-recommends \
    ca-certificates \
    maven \
    openjdk-8-jdk-headless \
    wget \
    git \
    unzip && \
apt-get clean && \
rm -rf /var/lib/apt/lists/*

WORKDIR /opt/shipping
COPY pom.xml /opt/shipping/
RUN mvn dependency:resolve
COPY src /opt/shipping/src/
RUN mvn package

FROM eclipse-temurin:8-jdk
WORKDIR /opt/shipping

ENV CART_ENDPOINT=cart:8080
ENV DB_HOST=mysql
COPY --from=build /opt/shipping/target/shipping-1.0.jar shipping.jar
CMD [ "java", "-Xmn256m", "-Xmx768m", "-jar", "shipping.jar" ]
