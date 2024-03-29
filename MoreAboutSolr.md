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

## Indexing sample data


### create collection
```
sudo -u solr /opt/workshop/solr/solr/bin/solr create -c tech_products -shards 1 -replicationFactor 2 -d /opt/workshop/solr/solr/server/solr/configsets/sample_techproducts_configs/conf -n techproducts_conf
```
### Post data to solr

```
/opt/workshop/solr/solr/bin/post -c tech_products /opt/workshop/solr/solr/example/exampledocs/*.xml -p 8080

```
### sample queries

#### query 

http://localhost:8080/solr/tech_products/select?fl=score&q=cat%3Aelectronics

#### filter query

http://localhost:8080/solr/tech_products/select?q=*:*&fl=score&fq=cat%3Aelectronics

#### facet on catogory
http://localhost:8080/solr/tech_products/select?q=*:*&facet.field=cat&facet=on

#### facte on date 
http://localhost:8080/solr/tech_products/select?q=*:*&facet.field=manufacturedate_dt&facet=on

#### date range 
http://localhost:8080/solr/tech_products/select?q=*:*&fl=manufacturedate_dt&fq=manufacturedate_dt%3A%5B2006-02-13T15%3A26%3A37Z%20TO%20*%5D

####  stats query

http://localhost:8080/solr/tech_products/select?indent=on&q=*:*&wt=json&stats=true&stats.field=price&fq=cat:electronics

#### Trigonometrics Functions
http://localhost:8080/solr/tech_products/select?fl=cos(45)&indent=on&q=*:*&wt=json&rows=1



#### Group Query 

http://localhost:8080/solr/tech_products/select?wt=json&indent=true&fl=name,price&q=memory&group=true&group.query=price:0+TO+99&group.query=price:[101+TO+200]&group.query=price:[201+TO+*]&group.limit=10&group.ngroups=true


#### Similarity Query

http://localhost:8080/solr/abstracts/mlt?q=*:*&fl=*&fq=pat_id:563533&mlt.fl=abstract


http://qa-solr-cloud:8080/solr/analyst_alert/select?fq=type:AnalystAlertEvent&fq=event_object_type_ss:Patent&fq=-is_stale_event_bs:true&fq=%7B!join%20from=object_and_events_id_sms%20to=objects_event_id_sms%7D(delivery_frequency_ss:daily%20AND%20user_id_ls:15900)&start=0&q=*:*&wt=json&rows=12&indent=on