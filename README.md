# docker-elk

## .env

The **.env** file is your environment variable file and is used to define your enviornment variables

1. \${VERSION}
   1. specifies the version eg: 7.4.1
2. \${ELASTIC_SEARCH_CLUSTER_NAME}
   1. Name of the elastic search cluster
3. \${ELASTIC_PORTS}
   1. Default port: 9200:9200
4. \${KIBANA_SERVER_NAME}
   1. Default is kibana.local
5. \${KIBANA_PORTS}
   1. Default port is 5601:5601

## Usage

1. Update the **.env** to reflect your requirements.
2. Build the image by running `docker-compose up -d` it is important to run this from the same directory as the docker-compose.yml and .env files
3. To shutdown the environment run `docker-compose down`
4. To shutdown the environment and delete the volumes `docker-compose down -v`

## Virtual Memory

Ensure the **vm.max_map_count=262144** as this is required to run.

- To check your **vm.max_map_count** type: `sysctl vm.max_map_count`
- To set **vm.max_map_count** type: `sysctl -w vm.max_map_count=262144` or `echo "vm.max_map_count=262144" >> /etc/sysctl.conf`

## ELASTICSEARCH

In this solution elastic search is setup in a 2 node cluster, the cluster names and network can be configured in the **.env** file.
Once started, you can test if elastic search is running typing: `curl http://localhost:9200/_cluster/health?pretty`

## KIBANA

The deafult host for elasticsearch is **https://elasticsearch:9200** but needs to be setup as the deafult host of our cluster which is defined by the variable ELASTIC_NODE_1.

Once running, Kibana can be accessed by going to http://localhost:5601. 5601 is the default port, if you have specified a different port, than you ned to replace this with the defined port

## Additional Commands

- To view all images run : `docker-compose images
- To get shell access to a server type: `docker-compose exec container-name command` - e.g:. `docker-compose exec owncloud /bin/bash`
