FROM java:8

ENV SCHEMACRAWLER_VERSION 14.07.07

RUN apt-get update && \
    apt-get install -y graphviz && \
    apt-get clean

RUN wget https://github.com/sualeh/SchemaCrawler/releases/download/v"$SCHEMACRAWLER_VERSION"/schemacrawler-"$SCHEMACRAWLER_VERSION"-main.zip && \
    unzip schemacrawler-"$SCHEMACRAWLER_VERSION"-main.zip && \
    rm schemacrawler-"$SCHEMACRAWLER_VERSION"-main.zip && \
    mv schemacrawler-"$SCHEMACRAWLER_VERSION"-main schemacrawler

WORKDIR /schemacrawler/_schemacrawler

VOLUME /output

ENTRYPOINT ["./schemacrawler.sh"]
