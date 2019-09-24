## The Heart of solr
-------------------

### Solr Env File :
ubuntu : /etc/default/solr.in.sh

windows/mac : ${solr_installation_dir}/bin

#### Parameters
```
SOLR_HEAP="512m"

ZK_HOST="127.0.0.1:2181"

ZK_CLIENT_TIMEOUT="15000"

SOLR_HOST="127.0.0.1"

SOLR_PID_DIR="/var/solr"

SOLR_HOME="/opt/workshop/solr/solr/server/

solr/collections/cores"

LOG4J_PROPS="/var/solr/log4j2.xml"

SOLR_LOGS_DIR="/var/solr/logs"

SOLR_PORT="8080"
```

### solrconfig.xml


#### Including lib files

``` <lib dir="${solr.install.dir:../../../..}/contrib/extraction/lib" regex=".*\.jar" />
  <lib dir="${solr.install.dir:../../../..}/dist/" regex="solr-cell-\d.*\.jar" />

  <lib dir="${solr.install.dir:../../../..}/contrib/clustering/lib/" regex=".*\.jar" />
  <lib dir="${solr.install.dir:../../../..}/dist/" regex="solr-clustering-\d.*\.jar" />

  <lib dir="${solr.install.dir:../../../..}/contrib/langid/lib/" regex=".*\.jar" />
  <lib dir="${solr.install.dir:../../../..}/dist/" regex="solr-langid-\d.*\.jar" />

  <lib dir="${solr.install.dir:../../../..}/dist/" regex="solr-ltr-\d.*\.jar" />

  <lib dir="${solr.install.dir:../../../..}/contrib/velocity/lib" regex=".*\.jar" />
  <lib dir="${solr.install.dir:../../../..}/dist/" regex="solr-velocity-\d.*\.jar" />

```
#### Request Handlers

* Every request handler is defined with a name and a class

    `http://localhost:8983/solr/gettingstarted/select?q=solr`

     <requestHandler name="/select" class="solr.SearchHandler">

        <lst name="defaults">

            <str name="echoParams">explicit</str>

            <int name="rows">10</int>
        </lst>
     </requestHandler>

#### Search Components

* Search components define the logic that is used by the SearchHandler to perform queries for users.

Example facet,mlt,highlight,stats






