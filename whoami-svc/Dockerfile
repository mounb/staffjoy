FROM maven:3.5-jdk-8-alpine AS build

WORKDIR /code

RUN mkdir -p /root/.m2
# COPY settings.xml /root/.m2/settings.xml
COPY pom.xml /code/pom.xml
RUN mvn --batch-mode dependency:resolve
RUN mvn --batch-mode verify

# Adding source, compile and package into a fat jar
COPY ["src/main", "/code/src/main"]
RUN mvn --batch-mode package

FROM java:8-jdk-alpine

COPY --from=build  /code/target/whoami-svc-1.0.0.jar /usr/app/

WORKDIR /usr/app

RUN sh -c 'touch whoami-svc-1.0.0.jar'

ENTRYPOINT ["java", "-jar", "whoami-svc-1.0.0.jar"]