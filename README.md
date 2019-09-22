# Solr 8.1 Installation Steps

Official Site : https://lucene.apache.org/solr/

## Service Installation Script
-----------------------
`bin/install_solr_service.sh`

Service installation script helps you to install solr as a service.

*Note : Currently, the script only supports CentOS, Debian, Red Hat, SUSE and Ubuntu Linux distributions*

## Planning Your Directory Structure
-----------------------
Recommended to use seperate directory for storing solr index files and logs.

### Solr Installation Directory

By default, the service installation script will extract the distribution archive into **/opt** Dir.

### Create the Solr User

Running Solr as root is not recommended for security reasons.

By default, the installation script will create the solr user, but you can override this setting using the -u option


## Installing Solr
------------------

* Download the required Solr version from its official site or mirrors.

    `wget https://archive.apache.org/dist/lucene/solr/8.1.0/solr-8.1.0.tgz`



* Extract the downloaded tar file.

    `tar xzf solr-8.1.0.tgz solr-8.1.0/bin/install_solr_service.sh --strip-components=2`

* Run the installation script.

    `sudo bash ./install_solr_service.sh solr-8.1.0.tgz -i /opt/workshop/solr -d /var/solr -u solr -s solr -p 8080`

    -i : solr installation Dir.

    -d : solr data directory.
     
    -u : username.

    -s : solr service name 

    -p : solr port.

## SolrCloud 

It is a distributed architecture focused on horizontal scaling where multiple nodes run instance of solr that communicate with each other through zookeeper.

### Setup Zookeper
------------------

ZooKeeper is a centralized service for maintaining configuration information, naming, providing distributed synchronization, and providing group services. 

* Download the required zookeper from its official site or mirrors.

    `wget https://www.apache.org/dist/zookeeper/zookeeper-3.4.14/zookeeper-3.4.14.tar.gz`

* Extract the downloaded tar file.

    `tar -xvzf  zookeeper-3.4.14.tar.gz`

*   Create Zookeper config file.

    `cd zookeeper-3.4.14/conf`

    `cp zoo_sample.cfg zoo.cfg`

*   Open zoo.cfg and add the server configurations
    ```
    dataDir=/tmp/zookeeper

    clientPort=2181

    server.1=localhost:2888:3888
    ```

*   Start zookeeper

    `bin/zkServer.sh start`
*   To Check zookeper status
    
    `bin/zkServer.sh status`

### Configuring Solr

* Open the solr env file

    `sudo vi /etc/default/solr.in.sh`
    ```
    ZK_HOST="127.0.0.1:2181"
    
    ZK_CLIENT_TIMEOUT="15000"
    
    SOLR_HOST="127.0.0.1"
    
    SOLR_PID_DIR="/var/solr"
    
    SOLR_HOME="/var/solr/data"
    
    LOG4J_PROPS="/var/solr/log4j2.xml"
    
    SOLR_LOGS_DIR="/var/solr/logs"
    
    SOLR_PORT="8080"
    ```

*   Restart solr

    `sudo service solr restart`
















