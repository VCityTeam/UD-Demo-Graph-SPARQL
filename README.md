# UD-Demo-Graph-SPARQL

A demonstration of the visualizing RDF semantic graphs alongside 3D City models using UD-Viz, 3D Tiles Server, Strabon RDF Store, and PostGIS.

![SPARQL POC Component Diagram](./UD-Demo_SPARQL_POC_Component_Diagram.svg)

## Installation
### Pre-requisites 

* [Install Docker](https://docs.docker.com/engine/install/)
* [Install Docker Compose](https://docs.docker.com/compose/install/)
* Install Python 3
  * [Windows](https://www.python.org/downloads/)
  * Ubuntu:
    ```
    sudo apt update
    sudo apt install python3
    ```

### Component Setup
To configure the demo and the components that support it edit the `.env` file to be launched with docker-compose. By default the following ports are used by the following services:
- 8995: 3dtiles-server
- 8996: postgis
- 8997: Strabon
- 8998: UD-Viz

The following sections will describe how to configure this file for each component. 

#### Build Images
In order to serve the 3D Tiles dataset to be used in the demo (located [here](./data/)) to UD-Viz, first the files must be loaded into the docker image.

To do this, run the `servelocalfiles.py` script to expose the data files locally on `localhost:8080`:
```
python3 servelocalfiles.py
```
Next build the 3D Tiles Server, Strabon, and UD-Viz docker images:
```
docker-compose build 3dtiles-server strabon udviz
```
When complete, halt the `servelocalfiles.py` script with `Ctrl+c`.

#### Upload RDF-Store Dataset
Once the images are built initialize their containers:
```
docker-compose up
```
