FROM openjdk:8-jre

EXPOSE 8080

ENV VER_NAME "2.0.0"
ENV DL_NAME "kieker.tar.gz"
ENV ARTIFACT_URL "https://build.se.informatik.uni-kiel.de/job/kieker-dev/job/master/lastSuccessfulBuild/artifact/build/distributions/kieker-${VER_NAME}-binaries.tar.gz"

WORKDIR /opt

RUN wget ${ARTIFACT_URL} -q -O ${DL_NAME} && \
    tar -xf ${DL_NAME} && \
    rm ${DL_NAME}  

WORKDIR /opt/kieker-${VER_NAME}/examples/JavaEEServletContainerExample/jetty

CMD java -jar start.jar
