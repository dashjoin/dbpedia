# DBpedia Sample Application

This application features an open data showcase using the [DBpedia](https://www.dbpedia.org/) SPARQL [service](https://dbpedia.org/sparql).

## Getting Started with Docker

The DBpedia service is exposed via the RDF microservice. This service in turn is consumed by the main platform. Therefore, we launch two containers.
This command starts the main platform. This application is auto installed from this GitHub repository:

```
docker run 
  -p 8080:8080 
  -e DJ_ADMIN_PASS=djdjdj 
  -e DASHJOIN_HOME=dbpedia 
  -e DASHJOIN_APPURL=https://github.com/dashjoin/dbpedia 
  dashjoin/platform
```

The RDF microservice connects to DBpedia. We also configure an ontology file that targets a specific use case (download https://raw.githubusercontent.com/dashjoin/dbpedia/main/dbpedia.n3):

```
docker run 
  -p 8082:8082 
  -e DASHJOIN_DATABASE_MODE=client 
  -e DASHJOIN_DATABASE_ENDPOINT=https://dbpedia.org/sparql 
  -e DASHJOIN_DATABASE_ONTOLOGIES=upload/dbpedia.n3
  -v /absolute path to/dbpedia.n3:/deployments/upload/dbpedia.n3
  dashjoin/rdf4j
```

The datatbase mode and endpoint make the service connect to DBpedia via SPARQL over HTTP.
The ontologies defines which classes are exposed to the user interface.
