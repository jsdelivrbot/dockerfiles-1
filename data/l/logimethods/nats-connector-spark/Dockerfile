FROM frolvlad/alpine-scala:2.11  
RUN ["mkdir", "-p", "\/usr\/local\/spark\/conf"]  
ENV SPARK_HOME="/usr/local/spark"  
COPY log4j.properties /usr/local/spark/conf  
COPY 1/scala-library-2.11.8.jar 2/spark-streaming_2.11-2.0.1.jar 3/spark-
core_2.11-2.0.1.jar 4/avro-mapred-1.7.7-hadoop2.jar 5/avro-ipc-1.7.7-tests.jar
6/avro-ipc-1.7.7.jar 7/avro-1.7.7.jar 8/jackson-core-asl-1.9.13.jar 9/jackson-
mapper-asl-1.9.13.jar 10/snappy-java-1.1.2.6.jar 11/commons-compress-1.4.1.jar
12/xz-1.0.jar 13/slf4j-api-1.7.16.jar 14/chill_2.11-0.8.0.jar 15/chill-
java-0.8.0.jar 16/kryo-shaded-3.0.3.jar 17/minlog-1.3.0.jar
18/objenesis-2.1.jar 19/xbean-asm5-shaded-4.4.jar 20/hadoop-client-2.2.0.jar
21/hadoop-common-2.2.0.jar 22/hadoop-annotations-2.2.0.jar 23/jsr305-1.3.9.jar
24/commons-cli-1.2.jar 25/commons-math-2.1.jar 26/xmlenc-0.52.jar 27/commons-
httpclient-3.1.jar 28/commons-codec-1.4.jar 29/commons-io-2.1.jar 30/commons-
net-2.2.jar 31/log4j-1.2.17.jar 32/commons-lang-2.5.jar 33/commons-
configuration-1.6.jar 34/commons-collections-3.2.1.jar 35/commons-
digester-1.8.jar 36/commons-beanutils-1.7.0.jar 37/commons-beanutils-
core-1.8.0.jar 38/protobuf-java-2.5.0.jar 39/hadoop-auth-2.2.0.jar 40/hadoop-
hdfs-2.2.0.jar 41/jetty-util-6.1.26.jar 42/hadoop-mapreduce-client-
app-2.2.0.jar 43/hadoop-mapreduce-client-common-2.2.0.jar 44/hadoop-yarn-
common-2.2.0.jar 45/hadoop-yarn-api-2.2.0.jar 46/slf4j-log4j12-1.7.16.jar
47/guice-3.0.jar 48/javax.inject-1.jar 49/aopalliance-1.0.jar
50/cglib-2.2.1-v20090111.jar 51/hadoop-yarn-client-2.2.0.jar 52/hadoop-
mapreduce-client-core-2.2.0.jar 53/hadoop-yarn-server-common-2.2.0.jar
54/hadoop-mapreduce-client-shuffle-2.2.0.jar 55/hadoop-mapreduce-client-
jobclient-2.2.0.jar 56/spark-launcher_2.11-2.0.1.jar 57/spark-
tags_2.11-2.0.1.jar 58/scalatest_2.11-2.2.6.jar 59/scala-reflect-2.11.8.jar
60/unused-1.0.0.jar 61/spark-network-common_2.11-2.0.1.jar 62/netty-
all-4.0.29.Final.jar 63/leveldbjni-all-1.8.jar 64/jackson-databind-2.6.5.jar
65/jackson-annotations-2.6.5.jar 66/jackson-core-2.6.5.jar 67/spark-network-
shuffle_2.11-2.0.1.jar 68/spark-unsafe_2.11-2.0.1.jar 69/jets3t-0.7.1.jar
70/curator-recipes-2.4.0.jar 71/curator-framework-2.4.0.jar 72/curator-
client-2.4.0.jar 73/zookeeper-3.4.5.jar 74/guava-14.0.1.jar 75/javax.servlet-
api-3.1.0.jar 76/commons-lang3-3.3.2.jar 77/commons-math3-3.4.1.jar 78/jul-to-
slf4j-1.7.16.jar 79/jcl-over-slf4j-1.7.16.jar 80/compress-lzf-1.0.3.jar
81/lz4-1.3.0.jar 82/RoaringBitmap-0.5.11.jar 83/json4s-jackson_2.11-3.2.11.jar
84/json4s-core_2.11-3.2.11.jar 85/json4s-ast_2.11-3.2.11.jar
86/paranamer-2.6.jar 87/scalap-2.11.8.jar 88/scala-compiler-2.11.8.jar
89/scala-xml_2.11-1.0.4.jar 90/scala-parser-combinators_2.11-1.0.4.jar
91/jersey-client-2.22.2.jar 92/javax.ws.rs-api-2.0.1.jar 93/jersey-
common-2.22.2.jar 94/javax.annotation-api-1.2.jar 95/jersey-guava-2.22.2.jar
96/hk2-api-2.4.0-b34.jar 97/hk2-utils-2.4.0-b34.jar 98/aopalliance-
repackaged-2.4.0-b34.jar 99/javax.inject-2.4.0-b34.jar
100/hk2-locator-2.4.0-b34.jar 101/javassist-3.18.1-GA.jar 102/osgi-resource-
locator-1.0.1.jar 103/jersey-server-2.22.2.jar 104/jersey-media-
jaxb-2.22.2.jar 105/validation-api-1.1.0.Final.jar 106/jersey-container-
servlet-2.22.2.jar 107/jersey-container-servlet-core-2.22.2.jar
108/mesos-0.21.1-shaded-protobuf.jar 109/netty-3.8.0.Final.jar
110/stream-2.7.0.jar 111/metrics-core-3.1.2.jar 112/metrics-jvm-3.1.2.jar
113/metrics-json-3.1.2.jar 114/metrics-graphite-3.1.2.jar 115/jackson-module-
scala_2.11-2.6.5.jar 116/jackson-module-paranamer-2.6.5.jar 117/ivy-2.4.0.jar
118/oro-2.0.8.jar 119/pyrolite-4.9.jar 120/py4j-0.10.3.jar 121/nats-connector-
spark-scala_2.11-0.3.0.jar 122/nats-connector-spark-0.3.0.jar
123/scalactic_2.11-3.0.0.jar /app/  
COPY 124/docker-nats-connector-spark-main-app_2.11-0.3.0.jar /app/docker-nats-
connector-spark-main-app_2.11-0.3.0.jar  
ENTRYPOINT ["java", "-Xms128m", "-Xmx512m", "-cp", "\/app\/scala-
library-2.11.8.jar:\/app\/spark-streaming_2.11-2.0.1.jar:\/app\/spark-
core_2.11-2.0.1.jar:\/app\/avro-mapred-1.7.7-hadoop2.jar:\/app\/avro-
ipc-1.7.7-tests.jar:\/app\/avro-
ipc-1.7.7.jar:\/app\/avro-1.7.7.jar:\/app\/jackson-core-
asl-1.9.13.jar:\/app\/jackson-mapper-asl-1.9.13.jar:\/app\/snappy-
java-1.1.2.6.jar:\/app\/commons-
compress-1.4.1.jar:\/app\/xz-1.0.jar:\/app\/slf4j-api-1.7.16.jar:\/app\/chill_2.11-0.8.0.jar:\/app\/chill-
java-0.8.0.jar:\/app\/kryo-
shaded-3.0.3.jar:\/app\/minlog-1.3.0.jar:\/app\/objenesis-2.1.jar:\/app\/xbean-
asm5-shaded-4.4.jar:\/app\/hadoop-client-2.2.0.jar:\/app\/hadoop-
common-2.2.0.jar:\/app\/hadoop-
annotations-2.2.0.jar:\/app\/jsr305-1.3.9.jar:\/app\/commons-
cli-1.2.jar:\/app\/commons-math-2.1.jar:\/app\/xmlenc-0.52.jar:\/app\/commons-
httpclient-3.1.jar:\/app\/commons-codec-1.4.jar:\/app\/commons-
io-2.1.jar:\/app\/commons-net-2.2.jar:\/app\/log4j-1.2.17.jar:\/app\/commons-
lang-2.5.jar:\/app\/commons-configuration-1.6.jar:\/app\/commons-
collections-3.2.1.jar:\/app\/commons-digester-1.8.jar:\/app\/commons-
beanutils-1.7.0.jar:\/app\/commons-beanutils-core-1.8.0.jar:\/app\/protobuf-
java-2.5.0.jar:\/app\/hadoop-auth-2.2.0.jar:\/app\/hadoop-
hdfs-2.2.0.jar:\/app\/jetty-util-6.1.26.jar:\/app\/hadoop-mapreduce-client-
app-2.2.0.jar:\/app\/hadoop-mapreduce-client-common-2.2.0.jar:\/app\/hadoop-
yarn-common-2.2.0.jar:\/app\/hadoop-yarn-
api-2.2.0.jar:\/app\/slf4j-log4j12-1.7.16.jar:\/app\/guice-3.0.jar:\/app\/javax.inject-1.jar:\/app\/aopalliance-1.0.jar:\/app\/cglib-2.2.1-v20090111.jar:\/app\/hadoop-
yarn-client-2.2.0.jar:\/app\/hadoop-mapreduce-client-
core-2.2.0.jar:\/app\/hadoop-yarn-server-common-2.2.0.jar:\/app\/hadoop-
mapreduce-client-shuffle-2.2.0.jar:\/app\/hadoop-mapreduce-client-
jobclient-2.2.0.jar:\/app\/spark-launcher_2.11-2.0.1.jar:\/app\/spark-
tags_2.11-2.0.1.jar:\/app\/scalatest_2.11-2.2.6.jar:\/app\/scala-
reflect-2.11.8.jar:\/app\/unused-1.0.0.jar:\/app\/spark-network-
common_2.11-2.0.1.jar:\/app\/netty-all-4.0.29.Final.jar:\/app\/leveldbjni-
all-1.8.jar:\/app\/jackson-databind-2.6.5.jar:\/app\/jackson-
annotations-2.6.5.jar:\/app\/jackson-core-2.6.5.jar:\/app\/spark-network-
shuffle_2.11-2.0.1.jar:\/app\/spark-
unsafe_2.11-2.0.1.jar:\/app\/jets3t-0.7.1.jar:\/app\/curator-
recipes-2.4.0.jar:\/app\/curator-framework-2.4.0.jar:\/app\/curator-
client-2.4.0.jar:\/app\/zookeeper-3.4.5.jar:\/app\/guava-14.0.1.jar:\/app\/javax.servlet-
api-3.1.0.jar:\/app\/commons-lang3-3.3.2.jar:\/app\/commons-
math3-3.4.1.jar:\/app\/jul-to-slf4j-1.7.16.jar:\/app\/jcl-over-
slf4j-1.7.16.jar:\/app\/compress-
lzf-1.0.3.jar:\/app\/lz4-1.3.0.jar:\/app\/RoaringBitmap-0.5.11.jar:\/app\/json4s-jackson_2.11-3.2.11.jar:\/app\/json4s-core_2.11-3.2.11.jar:\/app\/json4s-ast_2.11-3.2.11.jar:\/app\/paranamer-2.6.jar:\/app\/scalap-2.11.8.jar:\/app\/scala-
compiler-2.11.8.jar:\/app\/scala-xml_2.11-1.0.4.jar:\/app\/scala-parser-
combinators_2.11-1.0.4.jar:\/app\/jersey-client-2.22.2.jar:\/app\/javax.ws.rs-
api-2.0.1.jar:\/app\/jersey-common-2.22.2.jar:\/app\/javax.annotation-
api-1.2.jar:\/app\/jersey-
guava-2.22.2.jar:\/app\/hk2-api-2.4.0-b34.jar:\/app\/hk2-utils-2.4.0-b34.jar:\/app\/aopalliance-
repackaged-2.4.0-b34.jar:\/app\/javax.inject-2.4.0-b34.jar:\/app\/hk2-locator-2.4.0-b34.jar:\/app\/javassist-3.18.1-GA.jar:\/app\/osgi-
resource-locator-1.0.1.jar:\/app\/jersey-server-2.22.2.jar:\/app\/jersey-
media-jaxb-2.22.2.jar:\/app\/validation-api-1.1.0.Final.jar:\/app\/jersey-
container-servlet-2.22.2.jar:\/app\/jersey-container-servlet-
core-2.22.2.jar:\/app\/mesos-0.21.1-shaded-
protobuf.jar:\/app\/netty-3.8.0.Final.jar:\/app\/stream-2.7.0.jar:\/app\/metrics-
core-3.1.2.jar:\/app\/metrics-jvm-3.1.2.jar:\/app\/metrics-
json-3.1.2.jar:\/app\/metrics-graphite-3.1.2.jar:\/app\/jackson-module-
scala_2.11-2.6.5.jar:\/app\/jackson-module-
paranamer-2.6.5.jar:\/app\/ivy-2.4.0.jar:\/app\/oro-2.0.8.jar:\/app\/pyrolite-4.9.jar:\/app\/py4j-0.10.3.jar:\/app\/nats-
connector-spark-scala_2.11-0.3.0.jar:\/app\/nats-connector-
spark-0.3.0.jar:\/app\/scalactic_2.11-3.0.0.jar:\/app\/docker-nats-connector-
spark-main-app_2.11-0.3.0.jar",
"-Dlog4j.configuration=file:\/usr\/local\/spark\/conf\/log4j.properties",
"com.logimethods.nats.connector.spark.app.SparkProcessor"]

