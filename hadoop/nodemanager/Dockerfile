#Hadoop NM 镜像 
#1、configmap 化
#2、jmx-exporter
#3、node_exporter


FROM qtt-di/jdk:8u212
MAINTAINER cyc


ADD yarn /yarn


#yarn 的目录
# /data1-15/yarn  755

#可变配置
#yarn.nodemanager.local-dirs file:///data1-15/yarn
#yarn.nodemanager.log-dirs file:///data1-15/yarn/containers
#yarn.nodemanager.resource.cpu-vcores
#yarn.nodemanager.resource.memory-mb 


# TO BE move to configmap env  644
export HADOOP_HOME=/opt/apps/hadoop
export HADOOP_PID_DIR="${HADOOP_HOME}/pids"
export YARN_PID_DIR=${HADOOP_PID_DIR}
export HADOOP_MAPRED_PID_DIR=${HADOOP_PID_DIR}

# set hadoop conf dir
export HADOOP_CONF_DIR=/etc/apps/hadoop-conf

export YARN_LOG_DIR=/data1/logs/yarn
export HADOOP_PID_DIR="${YARN_LOG_DIR}/pids"
export YARN_PID_DIR=${HADOOP_PID_DIR}

export HADOOP_MAPRED_LOG_DIR=/data1/logs/mapred

export PATH=$PATH:$HADOOP_HOME/bin:$HADOOP_HOME/sbin



ADD hadoop-2.6.0-cdh5.16.1-qtt-0.0.7.tar.gz /opt/apps/

RUN mkdir -p /opt/apps/ /etc/apps/hadoop-conf /data1/logs/yarn/ /data1/logs/yarn/pids/   \
     && groupadd yarn \
     && useradd -g yarn hadoop \
     && gpasswd -M yarn hadoop \
     && chmod 755 /opt/apps/ /etc/apps/hadoop-conf /data1/logs/yarn/ /data1/logs/yarn/pids/ \
     
RUN cd /opt/apps/ \
    &&  wget https://di-dataos.oss-cn-beijing-internal.aliyuncs.com/fileserver/hadoop/hadoop-2.6.0-cdh5.16.1-qtt-0.0.7.tar.gz \
    && tar -zxvf hadoop-2.6.0-cdh5.16.1-qtt-0.0.7.tar.gz \
    && ln -s hadoop-2.6.0-cdh5.16.1-qtt-0.0.7 hadoop \
     
  
USER yarn

ENV HADOOP_HOME /opt/apps/hadoop
ENV PATH $PATH:$HADOOP_HOME/bin

WORKDIR $HADOOP_HOME