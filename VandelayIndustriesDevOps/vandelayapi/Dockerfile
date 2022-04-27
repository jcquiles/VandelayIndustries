FROM docker.vandelay.local/tomcat

MAINTAINER art@vandelayindustries.com

COPY setenv.sh /opt/tomcat/bin/setenv.sh

# Get the API .war file
RUN wget http://artifacts.vandlay.local/api/api-0.0.1-FINAL.war -O /maven/api-0.0.1-FINAL.war

VOLUME ["/maven", "/opt/tomcat/logs", "/opt/tomcat/work", "/opt/tomcat/temp", "/tmp/hsperfdata_root" ]

CMD /opt/tomcat/bin/deploy-and-run.sh

EXPOSE 80 443
