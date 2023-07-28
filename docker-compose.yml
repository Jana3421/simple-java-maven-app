FROM openjdk:8-alpine
RUN apk update && apk add /bin/sh
RUN mkdir -p /opt/app
ENV PROJECT_HOME /opt/app
COPY target/my-app-1.3-SNAPSHOT.jar PROJECT_HOME/my-app-1.3-SNAPSHOT.jar
WORKDIR $PROJECT_HOME
CMD ["java","-jar","/my-app-1.3-SNAPSHOT.jar"]
