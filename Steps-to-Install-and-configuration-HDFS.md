## Setup HDFS
### Before you begin
1. Create 2 VMs. They’ll be referred to throughout this guide as node-master.southindia.cloudapp.azure.com, node-slave1.southindia.cloudapp.azure.com.
Run the steps in this guide from the node-master unless otherwise specified.
2. Install the JDK using the appropriate guide for your Linux distribution or grab the latest JDK from Oracle.
3. The steps below use example IPs for each node. Adjust each example according to your configuration:
```
10.0.3.13   node-master.southindia.cloudapp.azure.com
10.0.3.14   node-slave1.southindia.cloudapp.azure.com
```
### Architecture of a Hadoop Cluster
A master node keeps knowledge about the distributed file system. node-master will handle this role in this guide, and it will have:
- The NameNode: manages the distributed file system and knows where stored data blocks inside the cluster are.

Slave nodes store the actual data and provide processing power to run the jobs. It'll be node-slave1.southindia.cloudapp.azure.com, and will host two daemons:
- The DataNode manages the actual data physically stored on the node; it’s named, NameNode.
- The NodeManager manages execution of tasks on the node.
### Distribute Authentication Key-pairs for the Hadoop User
The master node will use an ssh-connection to connect to other nodes with key-pair authentication, to manage the cluster.
1. Login to node-master as the hadoop user, and generate an ssh-key:
```
ssh-keygen -b 4096
```
2. Copy the key to the other nodes.
```
ssh-copy-id -i $HOME/.ssh/id_rsa.pub hadoop@node-master.southindia.cloudapp.azure.com
ssh-copy-id -i $HOME/.ssh/id_rsa.pub hadoop@node-slave1.southindia.cloudapp.azure.com
```
### Download and Unpack Hadoop BinariesPermalink
Login to node-master as the hadoop user, download the Hadoop tarball from Hadoop project page, and unzip it:
```
cd
wget http://apache.mindstudios.com/hadoop/common/hadoop-2.8.1/hadoop-2.8.1.tar.gz
tar -xzf hadoop-2.8.1.tar.gz
mv hadoop-2.8.1 hadoop
```
### Set Environment VariablesPermalink
Add Hadoop binaries to your PATH. Edit /home/hadoop/.profile and add the following line:
```
PATH=/home/hadoop/hadoop/bin:/home/hadoop/hadoop/sbin:$PATH
```
### Configure the Master Node
Configuration will be done on node-master and replicated to other nodes.
#### Set JAVA_HOME
1. Get your Java installation path. If you installed open-jdk from your package manager, you can get the path with the command:
```
update-alternatives --display java
```
Take the value of the current link and remove the trailing /bin/java. For example on Debian, the link is /usr/lib/jvm/java-8-openjdk-amd64/jre/bin/java, so JAVA_HOME should be /usr/lib/jvm/java-8-openjdk-amd64/jre.
If you installed java from Oracle, JAVA_HOME is the path where you unzipped the java archive.
2. Edit ~/hadoop/etc/hadoop/hadoop-env.sh and replace this line:
```
export JAVA_HOME=${JAVA_HOME}
```
with your actual java installation path. For example on a Debian with open-jdk-8:
```
export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64/jre
```
#### Set NameNode
Update ~/hadoop/etc/hadoop/core-site.xml:
```
<configuration>
     <property>
            <name>fs.defaultFS</name>
            <value>hdfs://node-master.southindia.cloudapp.azure.com:51000</value>
     </property>
</configuration>
```
#### Set path for HDFS
Edit hdfs-site.conf:
```
<configuration>
    	<property>
                <name>dfs.namenode.name.dir</name>
                <value>/home/madmin/data/nameNode</value>
        </property>
        <property>
                <name>dfs.datanode.data.dir</name>
                <value>/home/madmin/data/dataNode</value>
        </property>
        <property>
                <name>dfs.replication</name>
                <value>1</value>
        </property>
	<property>
		<name>dfs.permissions</name>
		<value>true</value>
	</property>
        <property>
                <name>dfs.namenode.secondary.http-address</name>
                <value>0.0.0.0:51090</value>
        </property>
        <property>
                <name>dfs.namenode.secondary.https-address</name>
                <value>0.0.0.0:51091</value>
        </property>
        <property>
                <name>dfs.datanode.address</name>
                <value>0.0.0.0:51010</value>
        </property>
        <property>
                <name>dfs.datanode.http.address</name>
                <value>0.0.0.0:51075</value>
        </property>
        <property>
                <name>dfs.datanode.ipc.address</name>
                <value>0.0.0.0:51020</value>
        </property>
        <property>
                <name>dfs.namenode.http-address</name>
                <value>0.0.0.0:51070</value>
        </property>
        <property>
                <name>dfs.namenode.https-address</name>
                <value>0.0.0.0:51470</value>
        </property>
        <property>
                <name>dfs.namenode.backup.address</name>
                <value>0.0.0.0:51100</value>
        </property>
        <property>
                <name>dfs.namenode.backup.http-address</name>
                <value>0.0.0.0:51105</value>
        </property>
</configuration>
```