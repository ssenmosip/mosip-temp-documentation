## 1. Setup HDFS version 2.8.1
### Before you begin
1. Create 2 VMs. They’ll be referred to throughout this guide as 
node-master.example.com, node-slave1.example.com.
Run the steps in this guide from the node-master unless otherwise specified.
2. Install the JDK using the appropriate guide for your Linux distribution or grab the latest JDK from Oracle. For RHEL, follow this [**link**](//developers.redhat.com/blog/2018/12/10/install-java-rhel8/)
3. Get the IP of master and slave nodes using:
```
ifconfig
```
The steps below use below IPs for each node. Adjust /etc/hosts on all nodes according to your configuration:
```
10.0.3.11   node-master.example.com
10.0.3.12   node-slave1.example.com
```
### Architecture of a Hadoop Cluster
A master node keeps knowledge about the distributed file system. node-master will handle this role in this guide, and it will have:
- The NameNode: manages the distributed file system and knows where stored data blocks inside the cluster are.

Slave nodes store the actual data and provide processing power to run the jobs. It'll be node-slave1.example.com, and will host two daemons:
- The DataNode manages the actual data physically stored on the node; it’s named, NameNode.
- The NodeManager manages execution of tasks on the node.
### Distribute Authentication Key-pairs for the Hadoop User
The master node will use an ssh-connection to connect to other nodes with key-pair authentication, to manage the cluster.
1. Login to node-master as the hadoop user, and generate an ssh-key:
```
ssh-keygen -t rsa
```
id_rsa.pub will contains the generated public key

2. Copy the public key to all the other nodes.
```
ssh-copy-id -i $HOME/.ssh/id_rsa.pub hadoop@node-master.example.com
ssh-copy-id -i $HOME/.ssh/id_rsa.pub hadoop@node-slave1.example.com
```
 or

add manually the ssh public key to each nodes in .ssh/authorized_keys
and try to ssh other node to see if shh has been configured successfully

```
ssh hadoop@node-slave1.example.com
```


### Download and Unpack Hadoop Binaries
Login to node-master as the hadoop user, download the Hadoop tarball from Hadoop project page, and unzip it:
```
cd
wget https://archive.apache.org/dist/hadoop/core/hadoop-2.8.1/hadoop-2.8.1.tar.gz
tar -xzf hadoop-2.8.1.tar.gz
mv hadoop-2.8.1 hadoop
```
### Set Environment Variables
Add Hadoop binaries to your PATH. Edit ``/home/hadoop/.bashrc`` or ``/home/hadoop/.bash_profiles`` and add the following line:
```
export HADOOP_HOME=$HOME/hadoop [hadoop installation directory]
export HADOOP_CONF_DIR=$HOME/hadoop/etc/hadoop
export HADOoP_MAPRED_HOME=$HOME/hadoop
export HADOOP_COMMON_HOME=$HOME/hadoop
export HADOOP_HDFS_HOME=$HOME/hadoop
export YARN_HOME=$HOME/hadoop
export PATH=$PATH:$HOME/hadoop/bin
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
            <value>hdfs://node-master.example:51000</value>
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

create directories
```
mkdir -p /home/hadoop/data/nameNode [where on the filesystem the DFS name node should store the name table(fsimage)]
mkdir -p /home/hadoop/data/dataNode  [where data node should store its blocks.]
```
#### Configure Master
Edit ~/hadoop/etc/hadoop/masters to be:
````
node-master.example.com
````
#### Configure Slaves
Edit ~/hadoop/etc/hadoop/slaves to be:
````
node-slave1.example.com
````
### Duplicate Config Files on Each Node 
1. Copy the hadoop binaries to slave nodes:
```
cd /home/hadoop/
scp hadoop-*.tar.gz node-slave1.example.com:/home/hadoop
```

or copy each configured files to other nodes

2. Connect to node1 via ssh. A password isn’t required, thanks to the ssh keys copied above:
```
ssh node-slave1.example.com
```
3. Unzip the binaries, rename the directory, and exit node-slave1.example.com to get back on the node-master.example.com:
```
tar -xzf hadoop-2.8.1.tar.gz
mv hadoop-2.8.1 hadoop
exit
```
4. Copy the Hadoop configuration files to the slave nodes:
``` 
for node in node-slave1.example.com; do
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
It’ll start NameNode and SecondaryNameNode on node-master.example.com, and DataNode on node-slave1.example.com, according to the configuration in the slaves config file.
2. Check that every process is running with the jps command on each node. You should get on node-master.example.com (PID will be different):
```
21922 Jps
21603 NameNode
21787 SecondaryNameNode
```
and on node-slave1.example.com:
```
19728 DataNode
19819 Jps
```
Hdfs has been Configured Successfully

### Create hdfs users
1. To create users for hdfs (regprocessor, prereg, idrepo), run this command:
```
sudo useradd  regprocessor
sudo useradd  prereg
sudo useradd  idrepo
```
2. Create a directory and give permission for each user
```
hdfs dfs -mkdir /user/regprocessor
hdfs dfs -chown -R regprocessor:regprocessor  /user/regprocessor
hdfs dfs -mkdir /user/prereg
hdfs dfs -chown -R prereg:prereg  /user/prereg
hdfs dfs -mkdir /user/idrepo
hdfs dfs -chown -R idrepo:idrepo  /user/idrepo
``` 
## 2. Securing HDFS
NOTE: Currently not enabled. `<WIP>`

Following configuration is required to run HDFS in secure mode.
Read more about kerberos here:
[**link**](//access.redhat.com/documentation/en-us/red_hat_enterprise_linux/6/html/managing_smart_cards/using_Kerberos)
### Install Kerberos
Kerberos server(KDC) and the client needs to be installed. Install the client on both master and slave nodes. KDC server will be installed on the master node.
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
 default_realm = NODE-MASTER.EXAMPLE.COM
 #default_ccache_name = KEYRING:persistent:%{uid}

[realms]
 NODE-MASTER.EXAMPLE.COM = {
  kdc = node-master.example.com:51088
  admin_server = node-master.example.com
 }

[domain_realm]
 .node-master.example.com = NODE-MASTER.EXAMPLE.COM
 node-master.example.com = NODE-MASTER.EXAMPLE.COM
```
2. Edit /var/kerberos/krb5kdc/kdc.conf
```
[kdcdefaults]
 kdc_ports = 51088
 kdc_tcp_ports = 51088

[realms]
 NODE-MASTER.EXAMPLE.COM = {
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
*/admin@NODE-MASTER.EXAMPLE.COM	*
```
5. Create the first principal using kadmin.local at the KDC terminal:
```
/usr/sbin/kadmin.local -q "addprinc root/admin"
```
6. Start Kerberos using the following commands:
```
/sbin/service krb5kdc start
/sbin/service kadmin start
```
to set up the KDC server to auto-start on boot.

```
RHEL/CentOS/Oracle Linux 6

chkconfig krb5kdc on

chkconfig kadmin on

RHEL/CentOS/Oracle Linux 7

systemctl enable krb5kdc

systemctl enable kadmin
```

7. Verify that the KDC is issuing tickets. 
First, run kinit to obtain a ticket and store it in a credential cache file.
```
kinit root/admin
```
Next, use klist to view the list of credentials in the cache.
```
klist
```
Use kdestroy to destroy the cache and the credentials it contains.
```
kdestroy -A
```
###  Install the JCE Policy File
Install Java Cryptography Extension (JCE) Unlimited Strength Jurisdiction Policy File on all cluster and Hadoop user machines.
Follow this [**link**](//dzone.com/articles/install-java-cryptography-extension-jce-unlimited)
### Create and Deploy the Kerberos Principals and Keytab Files
For more information, check here:
[**link**](//cloudera.com/documentation/enterprise/5-16-x/topics/cdh_sg_kerberos_prin_keytab_deploy.html)


If you have root access to the KDC machine, use kadmin.local, else use kadmin.
To start kadmin.local (on the KDC machine), run this command:
```
sudo kadmin.local
```
#### To create the Kerberos principals
Do the following steps for masternode.
1. In the kadmin.local or kadmin shell, create the hadoop principal. This principal is used for the NameNode, Secondary NameNode, and DataNodes.
```
kadmin:  addprinc hadoop/admin@NODE-MASTER.EXAMPLE.COM
```
2. Create the HTTP principal.
```
kadmin:  addprinc HTTP/admin@NODE-MASTER.EXAMPLE.COM
```
3. Create principal for all user of hdfs (regprocessor, prereg, idrepo)
```
kadmin:  addprinc regprocessor@NODE-MASTER.EXAMPLE.COM
kadmin:  addprinc prereg@NODE-MASTER.EXAMPLE.COM
kadmin:  addprinc idrepo@NODE-MASTER.EXAMPLE.COM
```
#### To create the Kerberos keytab files
Create the hdfs keytab file that will contain the hdfs principal and HTTP principal. This keytab file is used for the NameNode, Secondary NameNode, and DataNodes.
```
kadmin:  xst -norandkey -k hadoop.keytab hadoop/admin HTTP/admin
```
Use klist to display the keytab file entries; a correctly-created hdfs keytab file should look something like this:
```
$ klist -k -e -t hadoop.keytab
Keytab name: FILE:hadoop.keytab
KVNO Timestamp           Principal
---- ------------------- ------------------------------------------------------
   1 02/11/2019 08:53:51 hadoop/admin@NODE-MASTER.EXAMPLE.COM (aes256-cts-hmac-sha1-96)
   1 02/11/2019 08:53:51 hadoop/admin@NODE-MASTER.EXAMPLE.COM (aes128-cts-hmac-sha1-96)
   1 02/11/2019 08:53:51 hadoop/admin@NODE-MASTER.EXAMPLE.COM (des3-cbc-sha1)
   1 02/11/2019 08:53:51 hadoop/admin@NODE-MASTER.EXAMPLE.COM (arcfour-hmac)
   1 02/11/2019 08:53:51 hadoop/admin@NODE-MASTER.EXAMPLE.COM (camellia256-cts-cmac)
   1 02/11/2019 08:53:51 hadoop/admin@NODE-MASTER.EXAMPLE.COM (camellia128-cts-cmac)
   1 02/11/2019 08:53:51 hadoop/admin@NODE-MASTER.EXAMPLE.COM (des-hmac-sha1)
   1 02/11/2019 08:53:51 hadoop/admin@NODE-MASTER.EXAMPLE.COM (des-cbc-md5)
   1 02/11/2019 08:53:51 HTTP/admin@NODE-MASTER.EXAMPLE.COM (aes256-cts-hmac-sha1-96)
   1 02/11/2019 08:53:51 HTTP/admin@NODE-MASTER.EXAMPLE.COM (aes128-cts-hmac-sha1-96)
   1 02/11/2019 08:53:51 HTTP/admin@NODE-MASTER.EXAMPLE.COM (des3-cbc-sha1)
   1 02/11/2019 08:53:51 HTTP/admin@NODE-MASTER.EXAMPLE.COM (arcfour-hmac)
   1 02/11/2019 08:53:51 HTTP/admin@NODE-MASTER.EXAMPLE.COM (camellia256-cts-cmac)
   1 02/11/2019 08:53:51 HTTP/admin@NODE-MASTER.EXAMPLE.COM (camellia128-cts-cmac)
   1 02/11/2019 08:53:51 HTTP/admin@NODE-MASTER.EXAMPLE.COM (des-hmac-sha1)
   1 02/11/2019 08:53:51 HTTP/admin@NODE-MASTER.EXAMPLE.COM (des-cbc-md5)
```
##### Creating keytab [mosip.keytab] file for application to authenticate  with hdfs cluster
``` 
$sudo kadmin
   kadmin: xst -norandkey -k mosip.keytab {user1}
   kadmin: xst -norandkey -k mosip.keytab {user2} 
```
    replace {user} with username.

##### to view the principals in keytab
```
 $Klist -k -e -t mosip.keytab
```
     and so on add all the users to keytab. if you want create the separate keytab file for each application and distribute them


#### To deploy the Kerberos keytab file
On every node in the cluster, copy or move the keytab file to a directory that Hadoop can access, such as /home/hadoop/etc/hadoop/hadoop.keytab.
### Shut Down the Cluster
To enable security in hdfs, you must stop all Hadoop daemons in your cluster and then change some configuration properties. 

```
sh hadoop/sbin/stop-dfs.sh
```
### Enable Hadoop Security
1. To enable Hadoop security, add the following properties to the core-site.xml file on every machine in the cluster:
```
<property>
  <name>hadoop.security.authentication</name>
  <value>kerberos</value> 
</property>

<property>
  <name>hadoop.security.authorization</name>
  <value>true</value>
</property>
 
<property>
  <name>hadoop.http.filter.initializers</name>
  <value>org.apache.hadoop.security.AuthenticationFilterInitializer</value>
</property>

<property>
  <name>hadoop.http.authentication.type</name>
  <value>kerberos</value>
</property>

<property>
  <name>hadoop.http.authentication.simple.anonymous.allowed</name>
  <value>true</value>
</property>

<property>
  <name>hadoop.http.authentication.kerberos.principal</name>
  <value>HTTP/admin@NODE-MASTER.EXAMPLE.COM</value>
</property>

<property>
  <name>hadoop.http.authentication.kerberos.keytab</name>
  <value>/home/hadoop/etc/hadoop/hadoop.keytab</value>
</property>

```
2. Add the following properties to the hdfs-site.xml file on every machine in the cluster.
```
<property>
  <name>dfs.block.access.token.enable</name>
  <value>true</value>
</property>

<!-- NameNode security config -->
<property>
  <name>dfs.namenode.keytab.file</name>
  <value>/home/hadoop/etc/hadoop/hadoop.keytab</value> <!-- path to the HDFS keytab -->
</property>
<property>
  <name>dfs.namenode.kerberos.principal</name>
  <value>hadoop/admin@NODE-MASTER.EXAMPLE.COM</value>
</property>
<property>
  <name>dfs.namenode.kerberos.internal.spnego.principal</name>
  <value>HTTP/admin@NODE-MASTER.EXAMPLE.COM</value>
</property>

<!-- Secondary NameNode security config -->
<property>
  <name>dfs.secondary.namenode.keytab.file</name>
  <value>/home/hadoop/etc/hadoop/hadoop.keytab</value> <!-- path to the HDFS keytab -->
</property>
<property>
  <name>dfs.secondary.namenode.kerberos.principal</name>
    <value>hadoop/admin@NODE-MASTER.EXAMPLE.COM</value>
</property>
<property>
  <name>dfs.secondary.namenode.kerberos.internal.spnego.principal</name>
  <value>HTTP/admin@NODE-MASTER.EXAMPLE.COM</value>
</property>

<!-- DataNode security config -->
<property>
  <name>dfs.datanode.data.dir.perm</name>
  <value>700</value> 
</property>
<property>
  <name>dfs.datanode.keytab.file</name>
  <value>/home/hadoop/etc/hadoop/hadoop.keytab</value><!-- path to the HDFS keytab -->
</property>
<property>
  <name>dfs.datanode.kerberos.principal</name>
  <value>hadoop/admin@NODE-MASTER.EXAMPLE.COM</value>
</property>

<!-- Web Authentication config -->
<property>
  <name>dfs.web.authentication.kerberos.principal</name>
  <value>HTTP/admin@NODE-MASTER.EXAMPLE.COM</value>
 </property>

<property>
  <name>dfs.data.transfer.protection</name>
  <value>authentication</value>
 </property>

<property>
  <name>dfs.http.policy</name>
  <value>HTTPS_ONLY</value>
 </property>
```
### Deploying HTTPS in HDFS
#### Generating the key and certificate
The first step of deploying HTTPS is to generate the key and the certificate for each machine in the cluster. You can use Java’s keytool utility to accomplish this task:
Ensure that firstname/lastname OR common name (CN) matches exactly with the fully qualified domain name (e.g. node-master.example.com) of the server. 
```
keytool -genkey -alias localhost  -keyalg RSA -keysize 2048 -keystore keystore.jks
```
####  Creating your own CA
We use openssl to generate a new CA certificate:
```
openssl req -new -x509 -keyout ca-key.cer -out ca-cert.cer -days 365
```
The next step is to add the generated CA to the clients’ truststore so that the clients can trust this CA:
```
keytool -keystore truststore.jks -alias CARoot -import -file ca-cert.cer
```
#### Signing the certificate:
The next step is to sign all certificates generated  with the CA. First, you need to export the certificate from the keystore:
```
keytool -keystore keystore.jks -alias localhost -certreq -file cert-file.cer
```
Then sign it with the CA:
```
openssl x509 -req -CA ca-cert.cer -CAkey ca-key.cer -in cert-file.cer -out cert-signed.cer -days 365 -CAcreateserial -passin pass:12345678
```
Finally, you need to import both the certificate of the CA and the signed certificate into the keystore
```
keytool -keystore keystore.jks -alias CARoot -import -file ca-cert.cer
keytool -keystore keystore.jks -alias localhost -import -file cert-signed.cer
```
#### Configuring Hdfs
Change the ssl-server.xml and ssl-client.xml on all nodes to tell HDFS about the keystore and the truststore
1. Edit ssl-server.xml
```
<configuration>

<property>
  <name>ssl.server.truststore.location</name>
  <value>/home/hadoop/truststore.jks</value>
  <description>Truststore to be used by NN and DN. Must be specified.
  </description>
</property>

<property>
  <name>ssl.server.truststore.password</name>
  <value>12345678</value>
  <description>Optional. Default value is "".
  </description>
</property>

<property>
  <name>ssl.server.truststore.type</name>
  <value>jks</value>
  <description>Optional. The keystore file format, default value is "jks".
  </description>
</property>

<property>
  <name>ssl.server.truststore.reload.interval</name>
  <value>10000</value>
  <description>Truststore reload check interval, in milliseconds.
  Default value is 10000 (10 seconds).
  </description>
</property>

<property>
  <name>ssl.server.keystore.location</name>
  <value>/home/hadoop/keystore.jks</value>
  <description>Keystore to be used by NN and DN. Must be specified.
  </description>
</property>

<property>
  <name>ssl.server.keystore.password</name>
  <value>12345678</value>
  <description>Must be specified.
  </description>
</property>

<property>
  <name>ssl.server.keystore.keypassword</name>
  <value>12345678</value>
  <description>Must be specified.
  </description>
</property>

<property>
  <name>ssl.server.keystore.type</name>
  <value>jks</value>
  <description>Optional. The keystore file format, default value is "jks".
  </description>
</property>

<property>
  <name>ssl.server.exclude.cipher.list</name>
  <value>TLS_ECDHE_RSA_WITH_RC4_128_SHA,SSL_DHE_RSA_EXPORT_WITH_DES40_CBC_SHA,
  SSL_RSA_WITH_DES_CBC_SHA,SSL_DHE_RSA_WITH_DES_CBC_SHA,
  SSL_RSA_EXPORT_WITH_RC4_40_MD5,SSL_RSA_EXPORT_WITH_DES40_CBC_SHA,
  SSL_RSA_WITH_RC4_128_MD5</value>
  <description>Optional. The weak security cipher suites that you want excluded
  from SSL communication.</description>
</property>

</configuration>
```
2. Edit ssl-client.xml
```
<configuration>

<property>
  <name>ssl.client.truststore.location</name>
  <value>/home/hadoop/truststore.jks</value>
  <description>Truststore to be used by clients like distcp. Must be
  specified.
  </description>
</property>

<property>
  <name>ssl.client.truststore.password</name>
  <value>12345678</value>
  <description>Optional. Default value is "".
  </description>
</property>

<property>
  <name>ssl.client.truststore.type</name>
  <value>jks</value>
  <description>Optional. The keystore file format, default value is "jks".
  </description>
</property>

<property>
  <name>ssl.client.truststore.reload.interval</name>
  <value>10000</value>
  <description>Truststore reload check interval, in milliseconds.
  Default value is 10000 (10 seconds).
  </description>
</property>

<property>
  <name>ssl.client.keystore.location</name>
  <value>/home/hadoop/keystore.jks</value>
  <description>Keystore to be used by clients like distcp. Must be
  specified.
  </description>
</property>

<property>
  <name>ssl.client.keystore.password</name>
  <value>12345678</value>
  <description>Optional. Default value is "".
  </description>
</property>

<property>
  <name>ssl.client.keystore.keypassword</name>
  <value>12345678</value>
  <description>Optional. Default value is "".
  </description>
</property>

<property>
  <name>ssl.client.keystore.type</name>
  <value>jks</value>
  <description>Optional. The keystore file format, default value is "jks".
  </description>
</property>

</configuration>
```
After restarting the HDFS daemons (NameNode, DataNode and JournalNode), you should have successfully deployed HTTPS in your HDFS cluster.

For you face error during kerberos, check this:
[**link**](//steveloughran.gitbooks.io/kerberos_and_hadoop/content/sections/errors.html)