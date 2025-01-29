FROM maven:3-openjdk-17 AS build

RUN useradd -m -U keycloak

WORKDIR /app

COPY . .

RUN mvn clean package

FROM quay.io/keycloak/keycloak:latest AS kcbuild

COPY --from=build /app/target/*.jar /opt/keycloak/providers/

RUN /opt/keycloak/bin/kc.sh build 

FROM quay.io/keycloak/keycloak:latest

COPY --from=kcbuild /opt/keycloak/ /opt/keycloak/

