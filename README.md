# Open route service docker

This repo contains an example on how to configure and user openrouteservice api.
This documentation is obtained starting from [here](https://giscience.github.io/openrouteservice/installation/Running-with-Docker.html) please refer to it for additional details.
It continas:
1. a docker compose file to run the service for Italy
2. an example notebook to show how to use the features

## Setup

In order to start the api we need to:
1. download into the `data` folder a valid [geofabrik](https://download.geofabrik.de/) file for the region selected. In our case we use the Italian region.
    ```sh
    cd data
    wget https://download.geofabrik.de/europe/italy-latest.osm.pbf
    ```
2. start the container, from the root folder of the project
    ```sh
    cd ..
    docker compose up
    ```

The service is configured to load:
- directions: Get directions for different modes of transport
- isochrones: Obtain areas of reachability from given locations
- matrix: Obtain one-to-many, many-to-one and many-to-many matrices for time and distance
- geocode: Resolve input coordinates to addresses and vice versa
- pois: Obtain POIs of an area

The first time the container is ran it requires some time to create the index. 

> If you want to load only the geocode service and disable, routing, matrix and isochrone services modify 

**Important**
When the PBF file is changed we need to set `- BUILD_GRAPHS=True` (Forces the container to rebuild the graphs, e.g. when PBF is changed) and than stop the service and set it to False for the next runs. Otherwise, you can just cancel the content in the folder `elevation_cache`, `graphs` 

## Notebook with examples

