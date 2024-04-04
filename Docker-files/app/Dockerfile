# Use an existing Maven image from Docker Hub as the build stage
FROM maven:3.8.4-openjdk-11 AS build

# Set the working directory inside the container
WORKDIR /app

# Clone the vprofile-project repository from GitHub
RUN git clone https://github.com/aaleem123/vprofile-project.git

# Change to the project directory
WORKDIR /app/vprofile-project

# Checkout the 'docker' branch and run Maven clean install with debug logging
RUN git checkout docker && mvn install

# Use Tomcat as the deployment stage
FROM tomcat:9-jre11

# Remove any existing web applications from the Tomcat server
RUN rm -rf /usr/local/tomcat/webapps/*

# Copy the WAR file built in the build stage to the Tomcat webapps directory
COPY --from=build /app/vprofile-project/target/vprofile-v2.war /usr/local/tomcat/webapps/ROOT.war

# Expose port 8080
EXPOSE 8080

# Start Tomcat server
CMD ["catalina.sh", "run"]
