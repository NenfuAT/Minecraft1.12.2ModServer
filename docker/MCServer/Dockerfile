FROM openjdk:8-jre-slim

RUN apt-get update && apt-get install -y screen wget && apt-get clean && rm -rf /var/lib/apt/lists/*

WORKDIR /server
