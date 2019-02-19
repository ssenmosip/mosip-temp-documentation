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
### Download and Unpack Hadoop Binaries
Login to node-master as the hadoop user, download the Hadoop tarball from Hadoop project page, and unzip it:
```
cd
wget http://apache.mindstudios.com/hadoop/common/hadoop-2.8.1/hadoop-2.8.1.tar.gz
tar -xzf hadoop-2.8.1.tar.gz
mv hadoop-2.8.1 hadoop
```
### Set Environment Variables
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
Take the value of the current link and remove the trailing /bin/java. For example on RHEL 7, the link is /usr/lib/jvm/java-1.8.0-openjdk-1.8.0.191.b12-1.el7_6.x86_64/jre/bin/java, so JAVA_HOME should be /usr/lib/jvm/java-1.8.0-openjdk-1.8.0.191.b12-1.el7_6.x86_64/jre.
2. Edit ~/hadoop/etc/hadoop/hadoop-env.sh and replace this line:
```
export JAVA_HOME=${JAVA_HOME}
```
with your actual java installation path. For example on a Debian with open-jdk-8:
```
export JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.191.b12-1.el7_6.x86_64/jre
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
                <value>/home/hadoop/data/nameNode</value>
        </property>
        <property>
                <name>dfs.datanode.data.dir</name>
                <value>/home/hadoop/data/dataNode</value>
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
#### Configure Master
Edit ~/hadoop/etc/hadoop/masters to be:
````
node-master.southindia.cloudapp.azure.com
````
#### Configure Slaves
Edit ~/hadoop/etc/hadoop/slaves to be:
````
node-slave1.southindia.cloudapp.azure.com
````
### Duplicate Config Files on Each Node 
1. Copy the hadoop binaries to slave nodes:
```
cd /home/hadoop/
scp hadoop-*.tar.gz node-slave1.southindia.cloudapp.azure.com:/home/hadoop
```
2. Connect to node1 via ssh. A password isn’t required, thanks to the ssh keys copied above:
```
ssh node-slave1.southindia.cloudapp.azure.com
```
3. Unzip the binaries, rename the directory, and exit node-slave1.southindia.cloudapp.azure.com to get back on the node-master.southindia.cloudapp.azure.com:
```
tar -xzf hadoop-2.8.1.tar.gz
mv hadoop-2.8.1 hadoop
exit
```
4. Copy the Hadoop configuration files to the slave nodes:
``` 
for node in node-slave1.southindia.cloudapp.azure.com; do
    scp ~/hadoop/etc/hadoop/* $node:/home/hadoop/hadoop/etc/hadoop/;
done
```
### Format HDFS
HDFS needs to be formatted like any classical file system. On node-master, run the following command:
```
hdfs namenode -format
```
Your Hadoop installation is now configured and ready to run.
### Start HDFS
1. Start the HDFS by running the following script from node-master:
```
start-dfs.sh
```
It’ll start NameNode and SecondaryNameNode on node-master.southindia.cloudapp.azure.com, and DataNode on node-slave1.southindia.cloudapp.azure.com, according to the configuration in the slaves config file.
2. Check that every process is running with the jps command on each node. You should get on node-master.southindia.cloudapp.azure.com (PID will be different):
```
21922 Jps
21603 NameNode
21787 SecondaryNameNode
```
and on node-slave1.southindia.cloudapp.azure.com:
```
19728 DataNode
19819 Jps
```
## Securing HDFS
Following configuration is required to run HDFS in secure mode.
Read more about kerberos here:
https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/6/html/managing_smart_cards/using_kerberos
### Install Kerberos
Kerberos server and client needs to be installed on Kerberos VM. We are installing it on our master node.
1. To install packages for a Kerberos server:
```
yum install krb5-server krb5-libs krb5-auth-dialog
```
2. To install packages for a Kerberos client:
```
yum install krb5-workstation krb5-libs krb5-auth-dialog
```
### Configuring the Master KDC Server
1. Edit the /etc/krb5.conf:
```
# Configuration snippets may be placed in this directory as well
includedir /etc/krb5.conf.d/

[logging]
 default = FILE:/var/log/krb5libs.log
 kdc = FILE:/var/log/krb5kdc.log
 admin_server = FILE:/var/log/kadmind.log

[libdefaults]
 udp_preference_limit = 1
 dns_lookup_realm = false
 ticket_lifetime = 365d
 renew_lifetime = 365d
 forwardable = true
 rdns = false
 pkinit_anchors = /etc/pki/tls/certs/ca-bundle.crt
 default_realm = NODE-MASTER.SOUTHINDIA.CLOUDAPP.AZURE.COM
 #default_ccache_name = KEYRING:persistent:%{uid}

[realms]
 NODE-MASTER.SOUTHINDIA.CLOUDAPP.AZURE.COM = {
  kdc = node-master.southindia.cloudapp.azure.com:51088
  admin_server = node-master.southindia.cloudapp.azure.com
 }

[domain_realm]
 .node-master.southindia.cloudapp.azure.com = NODE-MASTER.SOUTHINDIA.CLOUDAPP.AZURE.COM
 node-master.southindia.cloudapp.azure.com = NODE-MASTER.SOUTHINDIA.CLOUDAPP.AZURE.COM
```
2. Edit /var/kerberos/krb5kdc/kdc.conf
```
[kdcdefaults]
 kdc_ports = 51088
 kdc_tcp_ports = 51088

[realms]
 NODE-MASTER.SOUTHINDIA.CLOUDAPP.AZURE.COM = {
  #master_key_type = aes256-cts
  acl_file = /var/kerberos/krb5kdc/kadm5.acl
  dict_file = /usr/share/dict/words
  admin_keytab = /var/kerberos/krb5kdc/kadm5.keytab
  supported_enctypes = aes256-cts:normal aes128-cts:normal des3-hmac-sha1:normal arcfour-hmac:normal camellia256-cts:normal camellia128-cts:normal des-hmac-sha1:normal des-cbc-md5:normal des-cbc-crc:normal
 }
```
3. Create the database using the kdb5_util utility.
```
/usr/sbin/kdb5_util create -s
```
4. Edit the /var/kerberos/krb5kdc/kadm5.acl
```
*/admin@NODE-MASTER.SOUTHINDIA.CLOUDAPP.AZURE.COM	*
```
5. Create the first principal using kadmin.local at the KDC terminal:
```
/usr/sbin/kadmin.local -q "addprinc hadoop/admin"
```
6. Start Kerberos using the following commands:
```
/sbin/service krb5kdc start
/sbin/service kadmin start
```
7. Verify that the KDC is issuing tickets. 
First, run kinit to obtain a ticket and store it in a credential cache file.
```
kinit hadoop/admin
```
Next, use klist to view the list of credentials in the cache.
```
klist
```
Use kdestroy to destroy the cache and the credentials it contains.
```
kdestroy -A
```
