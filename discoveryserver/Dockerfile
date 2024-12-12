FROM openjdk:17 AS build

WORKDIR /app

COPY pom.xml mvnw ./
RUN chmod +x mvnw
COPY .mvn .mvn
RUN ./mvnw dependency:resolve

COPY src src
RUN ./mvnw package -Dmaven.test.skip

FROM eclipse-termuin:17

WORKDIR /discoveryserver

COPY --from=build /app/target/*.jar /discoveryserver/discoveryserver-0.0.1-SNAPSHOT.jar

ENTRYPOINT ["java","-jar","discoveryserver-0.0.1-SNAPSHOT.jar"]