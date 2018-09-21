FROM openjdk:8-jre-alpine

EXPOSE 8080

ENV VER_NAME "1.13"
ENV DL_NAME "kieker.tar.gz"
ENV ARTIFACT_URL "https://github.com/kieker-monitoring/kieker/releases/download/${VER_NAME}/kieker-${VER_NAME}-binaries.tar.gz"

WORKDIR /opt

RUN wget ${ARTIFACT_URL} -q -O ${DL_NAME} && \
    tar -xf ${DL_NAME} && \
    rm ${DL_NAME}  

WORKDIR /opt/kieker-${VER_NAME}/examples/JavaEEServletContainerExample/jetty

CMD java -jar start.jar
