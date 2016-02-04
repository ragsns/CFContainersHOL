FROM tomcat:7-jre7
MAINTAINER Rags

RUN ["rm", "-fr", "/usr/local/tomcat/webapps/ROOT"]
COPY /./target/pcfdemo.war /usr/local/tomcat/webapps/ROOT.war

CMD ["catalina.sh", "run"]
