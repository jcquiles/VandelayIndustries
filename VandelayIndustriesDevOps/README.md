# Vandelay Industries DevOps

## Introduction

We build a Tomcat container and then a second container to hold the API itself.

## tomcat

This builds the Tomcat container.  We use Tomcat 8.5.31 on Java 8.

A Jenkins file can be used to do the build in Jenkins.  If you want to build it yourself, do:

```
cd tomcat
docker build -t docker.vandelay.local/tomcat .
```

## vandelayapi

This takes the tomcat container and puts our API in it, along with the database connection strings.


