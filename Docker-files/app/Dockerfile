FROM openjdk:11 AS BUILD_IMAGE
WORKDIR /mnt
RUN apt update && apt install maven -y
RUN git clone https://github.com/009gopal/vprofile-project.git
RUN cd /mnt/vprofile-project && git checkout -b docker && mvn install


FROM tomcat:9-jre11
RUN rm -rf /usr/local/tomcat/webapps/*
COPY --from=BUILD_IMAGE /mnt/vprofile-project/target/vprofile-v2.war /usr/local/tomcat/webapps/ROOT.war
EXPOSE 9090
CMD ["catalina.sh", "run"]
