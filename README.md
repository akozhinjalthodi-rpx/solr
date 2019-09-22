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

### Setup Zookeper
------------------














