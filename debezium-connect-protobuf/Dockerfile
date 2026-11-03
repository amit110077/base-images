# Debezium Connect 3.1 — the ghcr.io/amit110077/base mirror by digest — plus the Apicurio Registry 2.6.2 Protobuf serde (for AVA S-28: the cell's Connect converters are Protobuf, and the stock image bundles only the Avro, ExtJson and SerdeBased converters). Nothing of AVA is in it. linux/amd64.
FROM public.ecr.aws/docker/library/maven:3.9-eclipse-temurin-21 AS deps
WORKDIR /w
RUN printf '%s\n' '<project xmlns="http://maven.apache.org/POM/4.0.0"><modelVersion>4.0.0</modelVersion><groupId>local</groupId><artifactId>apicurio-protobuf-deps</artifactId><version>1</version><dependencies><dependency><groupId>io.apicurio</groupId><artifactId>apicurio-registry-serdes-protobuf-serde</artifactId><version>2.6.2.Final</version></dependency></dependencies></project>' > pom.xml
RUN mvn -q -B dependency:copy-dependencies -DincludeScope=runtime -DoutputDirectory=/out && ls /out | grep -i protobuf

FROM ghcr.io/amit110077/base/debezium-connect@sha256:a4b95e923516983dd763d62e8948314cc55c8ad93e755c487e085b67787263be
COPY --from=deps --chown=kafka:kafka /out/ /kafka/external_libs/apicurio/
