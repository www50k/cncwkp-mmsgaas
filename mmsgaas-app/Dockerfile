FROM adoptopenjdk:11-jre-openj9
ARG JAR_FILE=mmsgaas-s-0.0.1-SNAPSHOT.jar
COPY ${JAR_FILE} mmsgaas.jar
EXPOSE 8081
ENTRYPOINT [ "java", "-jar", "mmsgaas.jar" ]
