FROM openjdk:7-jre

EXPOSE 8080

ENV VER_NAME "1.13-SNAPSHOT"
ENV DL_NAME "kieker.tar.gz"
ENV ARTIFACT_URL "https://build.se.informatik.uni-kiel.de/jenkins/job/kieker-monitoring/job/kieker/job/master/lastSuccessfulBuild/artifact/build/distributions/kieker-${VER_NAME}-binaries.tar.gz"

WORKDIR /opt

RUN wget ${ARTIFACT_URL} -q -O ${DL_NAME} && \
    tar -xf ${DL_NAME} && \
    rm ${DL_NAME}  

WORKDIR /opt/kieker-${VER_NAME}/examples/JavaEEServletContainerExample/jetty

CMD java -jar start.jar
