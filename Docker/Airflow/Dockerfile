 docker build . -f Dockerfile --pull --tag claro/airflow:2.6.2

FROM apache/airflow:2.6.2
USER airflow
WORKDIR . 
RUN pip install cx-Oracle clickhouse-connect mysql-connector-python

USER root
RUN apt-get update && apt-get install -y libaio1 unzip
RUN apt-get install -y net-tools && apt-get install -y vim && apt-get install -y nano
RUN mkdir /opt/oracle
COPY ./instantclient-basic-linux.x64-19.19.0.0.0dbru.zip /opt/oracle/instantclient.zip
RUN cd /opt/oracle && unzip /opt/oracle/instantclient.zip && rm -f /opt/oracle/instantclient.zip
# #RUN ln -s libclntsh.so.12.1 libclntsh.so
# #RUN ln -s libocci.so.12.1 libocci.so
RUN sh -c "echo /opt/oracle/instantclient_19_19 > /etc/ld.so.conf.d/oracle-instantclient.conf"
RUN ldconfig

ENV LD_LIBRARY_PATH=/opt/oracle/instantclient_19_19
ENV ORACLE_HOME=/opt/oracle/instantclient_19_19

#change timezone
RUN ln -sf /usr/share/zoneinfo/America/Lima /etc/localtime
