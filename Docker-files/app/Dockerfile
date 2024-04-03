FROM maven:3.6.3-jdk-11 AS build
LABEL "Project"="vprofile"
RUN apt-get update -y
RUN git clone https://github.com/aaleem123/vprofile-project.git
RUN cd vprofile-project && git checkout docker 
RUN mvn clean package

FROM tomcat 
RUN rm -rf /usr/local/tomcat/webapps/ROOT*
COPY --from=build vprofile-project/target/vprofile-v2.war /usr/local/tomcat/webapps/ROOT.war
EXPOSE 8080
CMD ["catalina.sh", "run"]