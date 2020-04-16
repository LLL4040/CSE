# Hands-on-4: Name Service and Database Partitioning

## 1. Deploy the Zookeeper cluster

### Step 1 – Connect to your instance

Whatever method you use, just connect.

### Step2 - Check jdk version

```shell
java -version
```

zookeeper depends on jdk for startup, so be sure to install and configure jdk before starting zookeeper. If you don't have jdk, use the following command.

```shell
sudo apt-get update
sudo apt-get install java
```

### Step 2 – Download ZooKeeper by the following command

```shell
wget https://www-us.apache.org/dist/zookeeper/stable/apache-zookeeper-3.5.6-bin.tar.gz
```

Choose the image source that suits you, and note that after zookeeper 3.5.5 only the versions named with 'bin' are what we need here.

### Step 3 – Extract and install ZooKeeper by the following command

```shell
tar -xzf zookeeper-3.5.6-bin.tar.gz
sudo mv zookeeper-3.5.6-bin /usr/local/zookeeper
```

### Step 4 – Create a data directory and a log directory by the following command

```shell
sudo mkdir /usr/local/zookeeper/data
sudo mkdir /usr/local/zookeeper/logs
```

### Step 5: Use the sample configuration file of ZooKeeper as a base

```shell
sudo cp /usr/local/zookeeper/conf/zoo_sample.cfg
/usr/local/zookeeper/conf/zoo.cfg
```

By default when launching the Jar file, this zoo.cfg file will be used.

### Step 6: Change some parameters in zoo.cfg

```shell
dataDir=/usr/local/zookeeper/data
dataLogDir=/usr/local/zookeeper/logs
```

If dataDir or dataLogDir does not exist, it will cause zookeeper to fail to start.

Add admin.serverPort at the last line of the file.

```shell
admin.serverPort=8888
```

This is a new feature of zookeeper: By default, the server is started on port 8080. So if you don't change it, there may be an error when you try to start a server.

### Step 7: Add the path in zkServer.sh

```shell
#
# If this scripted is run out of /usr/bin or some other system bin directory
# it should be linked to and not copied. Things like java jar files are found
# relative to the canonical path of this script.
#
export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
export JRE_HOME=/usr/lib/jvm/java-8-openjdk-amd64/jre
export PATH=$PATH:$JAVA_HOME/bin:$JRE_HOME/bin
```

Remember to change it to your own path.

### Step 8: Start and stop

```shell
cd /usr/local/zookeeper/bin
./zkServer.sh start
```

If it shows STARTED, then you are ready. Use the following command to work.

```shell
./zkCli.sh
quit #to exit the cli
```

Just use stop to stop the server.

```shell
./zkServer.sh stop
```

### 2. Write the watcher application