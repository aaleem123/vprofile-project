FROM openjdk:11 AS build
LABEL "Project"="vprofile"
RUN apt update && apt install maven -y
RUN git clone https://github.com/aaleem123/vprofile-project.git
RUN cd vprofile-project && git checkout docker && mvn clean install -X

FROM tomcat:9-jre11
RUN rm -rf /usr/local/tomcat/webapps/*
COPY --from=build vprofile-project/target/vprofile-v2.war /usr/local/tomcat/webapps/ROOT.war

EXPOSE 8080
CMD ["catalina.sh", "run"]
