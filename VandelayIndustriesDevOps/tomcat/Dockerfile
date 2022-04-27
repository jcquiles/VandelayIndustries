FROM centos:8

MAINTAINER art@vandelayindustries.com

ENV CATALINA_HOME /opt/tomcat
ENV PATH $PATH:$CATALINA_HOME/bin
ENV TOMCAT_VERSION 8.5.31 
ENV DEPLOY_DIR /maven

# Install Java
RUN cd /etc/yum.repos.d/
RUN sed -i 's/mirrorlist/#mirrorlist/g' /etc/yum.repos.d/CentOS-*
RUN sed -i 's|#baseurl=http://mirror.centos.org|baseurl=http://vault.centos.org|g' /etc/yum.repos.d/CentOS-*
RUN yum install java-1.8.0-openjdk -y

# Get and Unpack Tomcat
RUN yum -y update && yum -y install wget
RUN wget http://archive.apache.org/dist/tomcat/tomcat-8/v${TOMCAT_VERSION}/bin/apache-tomcat-${TOMCAT_VERSION}.tar.gz -O /tmp/catalina.tar.gz
RUN tar xzf /tmp/catalina.tar.gz -C /opt 
RUN ln -s /opt/apache-tomcat-${TOMCAT_VERSION} /opt/tomcat 
RUN rm /tmp/catalina.tar.gz 

# Remove unneeded apps
RUN rm -rf /opt/tomcat/webapps/examples /opt/tomcat/webapps/docs /opt/tomcat/webapps/manager /opt/tomcat/webapps/host-manager 

# Add PostgreSQL connector .jar
RUN curl -o /opt/apache-tomcat-${TOMCAT_VERSION}/lib/postgresql-9.4.1210.jre7.jar https://jdbc.postgresql.org/download/postgresql-42.2.5.jar

# Add roles
COPY tomcat-users.xml /opt/apache-tomcat-${TOMCAT_VERSION}/conf/tomcat-users.xml

# Reconfigure to listen on 80/443
COPY server.xml /opt/apache-tomcat-${TOMCAT_VERSION}/conf/server.xml

# Startup script
COPY deploy-and-run.sh /opt/apache-tomcat-${TOMCAT_VERSION}/bin/deploy-and-run.sh
RUN chmod +x /opt/apache-tomcat-${TOMCAT_VERSION}/bin/deploy-and-run.sh

VOLUME ["/maven", "/opt/tomcat/logs", "/opt/tomcat/work", "/opt/tomcat/temp", "/tmp/hsperfdata_root" ]

CMD /opt/tomcat/bin/deploy-and-run.sh