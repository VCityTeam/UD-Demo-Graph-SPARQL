# UD-Demo-Graph-SPARQL

[![Build Status](https://app.travis-ci.com/VCityTeam/UD-Demo-Graph-SPARQL.svg?branch=master)](https://app.travis-ci.com/github/VCityTeam/UD-Demo-Graph-SPARQL)

A template repository for creating demos for visualizing RDF semantic graphs alongside 3D City models using:
* [UD-Viz](https://github.com/VCityTeam/UD-Viz) as a frontend web application for urban data visualization
  * In particular the [SPARQL module](https://github.com/VCityTeam/UD-Viz/tree/master/src/Widgets/Extensions/SPARQL) is used to visualize semantic urban data in the form of RDF
* And some RDF store as a backend. Currently two options are supported:
  * [Strabon RDF Store](http://www.strabon.di.uoa.gr/) an RDF-Store for storing and serving geospatial semantic graph data in the form of RDF
    * Also requires [PostGIS](https://postgis.net/) a geospatial database extension of [PostgreSQL](https://www.postgresql.org/) used here as a backend database for Strabon
  * [Blazegraph](https://blazegraph.com/), a ultra-high-performance graph database supporting Blueprints and RDF/SPARQL APIs

### Component Diagram
<img src="./UD-Demo_SPARQL_POC_Component_Diagram.svg" width="800px" />

## Installation

### Pre-requisites 

* [Install Docker](https://docs.docker.com/engine/install/)
* [Install Docker Compose](https://docs.docker.com/compose/install/)

### Repository setup
To begin create a new Github repository using this template:

![image](https://user-images.githubusercontent.com/23373264/217045942-5f994e2d-431e-4620-bf76-f1cc1f1d7673.png)

Once generated, use the new repository can be cloned:
```
git clone [your new repository URL]
```

### Component Setup
To configure the demo and the components that support it edit the `.env` file to be launched with docker-compose. By default, the following ports are used by the following services:
```bash
#### UD-Viz
UD_VIZ_PORT=8000
#### BlazeGraph
BLAZEGRAPH_PORT=8001
```
The following sections will describe how to configure this file for each component. 

### Build Images and run containers
First, build the docker images and run their containers:
```bash
docker compose up
```
> [!NOTE]
> Make sure to set the `sparqlModule/url` port in the `./ud-viz-context/config.json` file to the same port for the triple store container declared in the `.env` file.
> If these ports are ever changed after building the images, the _UD-Viz_ image must be rebuilt:
```bash
docker compose build udviz
```

### Upload RDF-Store Dataset
To upload files into Blazegraph to be used by the sparqlModule run the [./loadData.sh](./loadData.sh) script with the blazegraph SPARQL query endpoint as a parameter: 
```bash
./loadData.sh http://127.0.0.1:8001/blazegraph/sparql > log.html
```

Now the UD-Viz demo is ready and can be accessed from [localhost:8000](http://localhost:8000)
The Blazegraph interface can also be accessed from [localhost:8001](http://localhost:8001)
