<h1>Hadoop, Zookeeper, HBase, and Phoenix Integration</h1>

<p>
This repository is nothing but an example on how to integrate Apache Hadoop, Apache Zookeeper, Apache HBase, and Apache Phoenix on debian 8 (jessie).
</p>
<p>Since the HBase's configuration on this example is in pseudo distributed mode, not the standalone one, so that we need Hadoop installed in our machine.</p>

<h3>Prerequisites</h3>
<p>1. <a href="http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html">JDK 1.8</a></p>
<p>2. <a href="http://www.apache.org/dyn/closer.cgi/hadoop/common/hadoop-3.1.0/hadoop-3.1.0.tar.gz">Apache Hadoop-3.1.0</a></p>
<p>3. <a href="http://www-us.apache.org/dist/zookeeper/zookeeper-3.4.12/">Apache Zookeeper-3.4.12</a></p>
<p>4. <a href="http://www.apache.org/dyn/closer.lua/hbase/2.0.0/hbase-2.0.0-bin.tar.gz">Apache HBase-2.0.0</a></p>
<p>5. <a href="http://www-us.apache.org/dist/phoenix/apache-phoenix-5.0.0-alpha-HBase-2.0/bin/">Apache Phoenix-5.0.0-alpha-HBase</a></p>
	
<h3>Configuration Steps</h3>

<h4>Hadoop Installation</h4>
<p>1. Install and set java environment</p>
<p>2. Unpack and copy hadoop-3.1.0 package to particular path e.g. /home/usr/programs/hadoop-3.1.0 (tar -zxvf -C /home/usr/programs)</p>
<p>3. Go to hadoop-3.1.0 root directory</p>
<p>4. Edit and set JAVA_HOME in hadoop-env.sh (vi ./etc/hadoop/hadoop-env.sh and export JAVA_HOME=/usr/lib/jvm/jdk8/jdk1.8.0.171)</p>
<p>5. Edit core-site.xml and set hadoop.tmp.dir as well as fs.default.name properties</p>
<p>6. Create data directory then create namenode as well as datanode directories inside it</p>
<p>7. Change the data directory and its subdirectories permissions for readable, writable and executable by everyone (chmod 7777 -R ./data/*)</p>
<p>8. Edit hdfs-site.xml and set dfs.replication, dfs.namenode.name.dir, and dfs.datanode.data.dir properties</p>
<p>9. Edit mapred-site.xml and set mapred.job.tracker as well as mapreduce.framework.name properties</p>
<p>10. Edit yarn-site.xml and set yarn.nodemanager.aux-services property</p>
<p>11. Format namenode by executing ./bin/hdfs namenode -format command</p>
<p>12. Set HDFS_DATANODE_USER, HADOOP_SECURE_DN_USER, HDFS_NAMENODE_USER, HDFS_SECONDARYNAMENODE_USER in start-dfs.sh and stop-dfs.sh (vi ./sbin/s*dfs.sh and set the values for all mentioned properties with root for example)</p>
<p>13. Set YARN_RESOURCEMANAGER_USER and YARN_NODEMANAGER_USER in start-yarn.sh and stop-yarn.sh (vi ./sbin/s*yarn.sh and set the values for both properties with root for example)</p>

<h4>Zookeeper Installation</h4>
<p>Unpack zookeeper-3.4.12 package to particular path e.g. /home/usr/programs/zookeeper-3.4.12 (tar -zxvf -C /home/usr/programs)</p>

<h4>HBase Installation</h4>
<p>1. Unpack hbase-2.0.0 package to particular path e.g. /home/usr/programs/hbase-2.0.0 (tar -zxvf -C /home/usr/programs)</p>
<p>2. Go to hbase-2.0.0 root directory</p>
<p>3. Edit and set JAVA_HOME in hbase-env.sh (vi ./etc/hbase/hbase-env.sh and export JAVA_HOME=/usr/lib/jvm/jdk8/jdk1.8.0.171)
as well as set HBASE_MANAGES_ZK=false</p>
<p>4. Edit hbase-site.xml and set the properties needed</p>

<h4>Phoenix Installation</h4>
<p>Unpack phoenix-5.0.0-alpha-hbase package to particular path e.g. /home/usr/programs/phoenix-5.0.0-alpha-hbase (tar -zxvf -C /home/usr/programs)</p>

<h4>Run Hadoop</h4>
<p>Go to hadoop-3.1.0 root directory and execute ./sbin/start-dfs.sh and ./sbin/start-yarn.sh commands sequentially</p>

<h4>Run Zookeeper</h4>
<p>Go to zookeeper-3.4.12 root directory and execute ./bin/zkServer.sh start</p>

<h4>Run HBase</h4>
<p>Go to hbase-2.0.0 root directory and execute ./bin/start-hbase.sh</p>

<h4>Run Phoenix</h4>
<p>Go to phoenix-5.0.0-alpha-hbase root directory and execute ./bin/sqline-thin.py -a BASIC --auth-user=root --auth-password=root localhost:8765 ./examples/STOCK_SYMBOL.sql for example</p> 
