# UD-Demo-Graph-SPARQL

A demonstration of the visualizing RDF semantic graphs alongside 3D City models using UD-Viz, 3D Tiles Server, Strabon RDF Store, and PostGIS.

![SPARQL POC Component Diagram](./UD-Demo%20SPARQL%20POC%20Component%20Diagram)

## Installation
### Pre-requisites 

* [Install Docker](https://docs.docker.com/engine/install/)
* [Install Docker Compose](https://docs.docker.com/compose/install/)
* Install Python 3.6 or higher
  * [Windows](https://www.python.org/downloads/)
  * Ubuntu:
    ```
    sudo apt update
    sudo apt install python3.8
    ```

### Component Setup
To configure the demo and the components that support it edit the `.env` file to be launched with docker-compose. By default the following ports are used by the following services:
- 8995: 3dtiles-server
- 8996: postgis
- 8997: Strabon
- 8998: UD-Viz

The following sections will describe how to configure this file for each component. 

#### 3D Tiles Server
In order to serve the 3D Tiles dataset to be used in the demo (located [here](./data/)) to UD-Viz, the files must be loaded into the server.

First run the `servelocalfiles.py` script to expose the data files locally on `localhost:8080`:
```
python3 servelocalfiles.py
```
Next build the 3D Tiles Server Docker container:
```
docker-compose build 3dtiles-server
```

#### Strabon Setup
#### UD-Viz Setup
