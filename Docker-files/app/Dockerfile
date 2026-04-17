# ---------- Stage 1: Build ----------
FROM maven:3.9.9-eclipse-temurin-21-jammy AS BUILD_IMAGE

RUN git clone https://github.com/hkhcoder/vprofile-project.git
WORKDIR /vprofile-project

RUN git checkout containers && mvn install


# ---------- Stage 2: Run ----------
FROM tomcat:10-jdk21

RUN rm -rf /usr/local/tomcat/webapps/*

COPY --from=BUILD_IMAGE /vprofile-project/target/vprofile-v2.war /usr/local/tomcat/webapps/ROOT.war

EXPOSE 8080

CMD ["catalina.sh", "run"]