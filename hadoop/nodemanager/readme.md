#镜像构建

1、基础镜像 jdk 212   
2、NodeManager 配置文件处理：  
  
   * yarn-env.sh,yarn-site.xml,hadoop-env.sh,core-site.xml,hdfs-site.xml,log4j.properties,mapred-env.sh,mapred-site.xml  
   ConfigMap 挂载

3、由于具有多种规格的NM，所以需要做一些配置修改。比如适配内存/cpu/磁盘个数

不同的规格的NodeManager 配置参数不同如下

#yarn.nodemanager.local-dirs file:///data1-15/yarn

#yarn.nodemanager.log-dirs file:///data1-15/yarn/containers

#yarn.nodemanager.resource.cpu-vcores

#yarn.nodemanager.resource.memory-mb 

4、NodeManager 需要一些环境变量，通过configmap 挂载  

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

5、目录

如下目录权限 755 

安装目录 /opt/apps/hadoop 软连接 

配置目录 /etc/apps/hadoop-conf

NodeManager 日志目录以及pid /data1/logs/yarn/ /data1/logs/yarn/pids/ 

NodeManager local-dirs 以及log-dirs file:///data1-15/yarn ,file:///data1-15/yarn/containers

6、考虑NodeManager 使用ip地址 需要看如何配置或者支持

7、用户组是 yarn:hadoop

8、时区 RUN ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

9、进程启动使用yarn 用户启动


