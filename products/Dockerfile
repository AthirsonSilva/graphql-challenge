#
# Build stage
#
FROM gradle:7.4.2-jdk17 AS build

RUN mkdir /app

WORKDIR /app

COPY . /app

RUN ls -la /app

RUN gradle build -x test --no-daemon --info

#
# Package stage
#
FROM eclipse-temurin:17-jdk-alpine AS package

COPY --from=build /app/build/libs/*.jar /usr/local/lib/

RUN ls -la /usr/local/lib/

RUN mv /usr/local/lib/*-0.*-SNAPSHOT.jar /usr/local/lib/app.jar

EXPOSE 8000

ENTRYPOINT ["java","-jar","/usr/local/lib/app.jar"]