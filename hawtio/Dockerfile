FROM azul/zulu-openjdk:17.0.2-jre

RUN apt-get update \
    && apt-get install -y curl file \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

RUN useradd --no-log-init --create-home --shell /bin/bash appuser
USER appuser
WORKDIR /home/appuser

ARG HAWTIO_VERSION=2.14.5
ENV DOCKER_HAWTIO_DIR=/home/appuser/opt/hawtio \
    DOCKER_HAWTIO_FILENAME=hawtio-app-${HAWTIO_VERSION}.jar
RUN mkdir -p ${DOCKER_HAWTIO_DIR} \
    && curl -L https://repo1.maven.org/maven2/io/hawt/hawtio-app/${HAWTIO_VERSION}/hawtio-app-${HAWTIO_VERSION}.jar -o ${DOCKER_HAWTIO_DIR}/${DOCKER_HAWTIO_FILENAME}
ARG HAWTIO_PORT=8081
ENV DOCKER_HAWTIO_PORT=${HAWTIO_PORT}
EXPOSE ${HAWTIO_PORT}
CMD ["bash", "-c", "java -Dhawtio.proxyWhitelist=* -Dhawtio.proxyAllowlist=* -jar ${DOCKER_HAWTIO_DIR}/${DOCKER_HAWTIO_FILENAME} --port ${DOCKER_HAWTIO_PORT}"]