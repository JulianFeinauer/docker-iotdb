FROM openjdk:11-jre-slim
RUN apt update \
  # procps is for `free` command
  && apt install wget unzip lsof procps maven git -y \
  #&& wget https://www-us.apache.org/dist/incubator/iotdb/0.9.1-incubating/apache-iotdb-0.9.1-incubating-bin.zip \
  && git clone git@github.com:apache/incubator-iotdb.git \
  && cd incubator-iotdb \
  && mvn clean package -DskipTests \
  #&& wget http://mirrors.tuna.tsinghua.edu.cn/apache/incubator/iotdb/0.9.1-incubating/apache-iotdb-0.9.1-incubating-bin.zip \
  #&& unzip apache-iotdb-0.9.1-incubating-bin.zip \
  #&& rm apache-iotdb-0.9.1-incubating-bin.zip \
  #&& mv apache-iotdb-0.9.1-incubating /iotdb \
  && mv distribution/target/apache-iotdb-0.10.0-SNAPSHOT-incubating-bin /iotdb \
  && sed -i '1670d' /iotdb/conf/logback.xml \
  && apt remove wget unzip -y \
  && apt autoremove -y \
  && apt purge --auto-remove -y \
  && apt clean -y
EXPOSE 6667
EXPOSE 31999
EXPOSE 8181
VOLUME /iotdb/data
VOLUME /iotdb/logs
ENV PATH="/iotdb/sbin/:/iotdb/tools/:${PATH}"
ENTRYPOINT ["/iotdb/sbin/start-server.sh"]