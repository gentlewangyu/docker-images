#Hadoop NM 镜像 
#1、configmap 化
#2、jmx-exporter
#3、node_exporter


FROM qtt-di/jdk:8u212
MAINTAINER cyc


RUN mkdir -p /opt/apps/ /etc/apps/hadoop-conf /data1/logs/yarn/ /data1/logs/yarn/pids/   \
     && groupadd yarn \
     && useradd -g yarn hadoop \
     && gpasswd -M yarn hadoop \
     && chmod 755 /opt/apps/ /etc/apps/hadoop-conf /data1/logs/yarn/ /data1/logs/yarn/pids/ \
     
RUN cd /opt/apps/ \
    &&  wget https://di-dataos.oss-cn-beijing-internal.aliyuncs.com/fileserver/hadoop/hadoop-2.6.0-cdh5.16.1-qtt-0.0.7.tar.gz \
    && tar -zxvf hadoop-2.6.0-cdh5.16.1-qtt-0.0.7.tar.gz \
    && ln -s hadoop-2.6.0-cdh5.16.1-qtt-0.0.7 hadoop \

# TO BE move to ConfigMap env  644

ENV HADOOP_HOME=/opt/apps/hadoop 
    HADOOP_PID_DIR="${HADOOP_HOME}/pids"  
    YARN_PID_DIR=${HADOOP_PID_DIR}  
    HADOOP_MAPRED_PID_DIR=${HADOOP_PID_DIR} 
    HADOOP_CONF_DIR=/etc/apps/hadoop-conf 
    YARN_LOG_DIR=/data1/logs/yarn 
    HADOOP_PID_DIR="${YARN_LOG_DIR}/pids" 
    YARN_PID_DIR=${HADOOP_PID_DIR}   
    HADOOP_MAPRED_LOG_DIR=/data1/logs/mapred  
    PATH=$PATH:$HADOOP_HOME/bin:$HADOOP_HOME/sbin 

USER yarn
WORKDIR $HADOOP_HOME