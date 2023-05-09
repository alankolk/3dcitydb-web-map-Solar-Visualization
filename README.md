# Visualization of rooftop solar potential in smart cities

### Using 3DCityDB-Web-Map-Client

## Introduction

This project is a part of a thesis done in the University of Tartu.

Using the 3DCityDB, Tartu city CityGML files were converted with the Importer/Exporter tool that comes with 3DCityDB. 

The CityGML files were converted to KML Geometry to be able to colour building rooftops based on the solar potential that each polygon on a roof gets.

Scripts were made for the colouring of the KML files based on the solar potential.

The project uses 3DCityDB-Web-Map-Client to visualize the 3D spatial data.

## requirements

### Hardware

The hardware on which the 3DCityDB-Web-Map-Client will be run must support WebGL. In addition, the web browser in use must also provide appropriate WebGL support. 

The author of this project recommends at least 4 GB of RAM and a dedicated graphics card, as a dedicated graphics card makes the usage experience smoother.

For best performance, it is recommended to use Google Chrome as the browser.

### Software

- A database for the 3DCityDB (Author used PostgreSQL).

- A browser, Google Chrome is recommended.

- Python for the scripts.

### For the Web-Map-Client

To run it locally **```Node.js```** needs to be installed. The project has the dependancies already included.

### For the Scripts

**```Python```** is needed for running the scripts.

The following Python extensions need to be installed for the scripts:
- **```pyKML```** for KML parsing
- **```lxml```** dependancy of pyKML
- **```pyproj```** for transforming coordinates from EPSG:3301 to WGS:84
- **```Pandas```** for data analysis

## Running the project locally

To run the project locally **```Node.js```** needs to be installed.

By default, the local server IP is set to **```localhost```** and the port is **```8000```**.

These can be changed by editing the **```server.js```** file in the project folder.

In a command prompt the following command runs the project locally if the command prompt current location is the project folder:

**```node server.js```**

**The web application, when run locally, opens with the URL ```localhost:8000/3dwebclient/index.html```**

### Using already generated Tartu city 3D solar potential data

3D visualization data that has already been coloured with the solar potential of the buildings can be found in this **[repository](https://github.com/alankolk/Tartu_solar_visualization_data)**.

To use the data in the Web-Map-Client, put it in the project folder.
- put the **```cities```** folder in the project folder
- put the **```data```** folder in the project folder

**If the local server IP (localhost) has not been changed in the ```server.js``` file along with the port (8000), then the following link automatically opens the Tartu visualization in the browser:**

**[Tartu city LOD2 solar potential visualization localhost link](http://localhost:8000/3dwebclient/index.html?t=3DCityDB-Web-Map-Client&s=false&ts=0&la=58.379595&lo=26.726688&h=1838.114&hd=360&p=-90&r=0&l_0=u%3Dhttp%253A%252F%252Flocalhost%253A8000%252Fcities%252Ftartu_data%252FTartu_geometry_MasterJSON.json%26n%3DTartu%2520-%2520Solar%2520Potential%26ld%3DCOLLADA%252FKML%252FglTF%26lp%3Dfalse%26lc%3Dtrue%26gv%3D2.0%26a%3Dtrue%26tdu%3Dhttps%253A%252F%252Fdocs.google.com%252Fspreadsheets%252Fd%252F1NxWJ4qi46FuBzyIFMG9eXsFvJ6nY5Nmd0tFZGsXFZjI%252Fedit%253Fusp%253Dshare_link%26ds%3DGoogleSheets%26tt%3DHorizontal%26gc%3Dhttp%253A%252F%252Flocalhost%253A8000%252Fcities%252Ftartu_data%252FTartu.json%26il%3D125%26al%3D1.7976931348623157e%252B308%26ac%3D150%26av%3D80&sw=showOnStart%3Dfalse)**

**NB!**

**If parameters have been changed, then the usage example, for importing data into the web client, from the documentation can be found at the bottom of this page [Documentation Usage Example](https://3dcitydb-docs.readthedocs.io/en/latest/webmap/online-spreadsheet.html).**

## How To Generate New Visualization Data

To generate new visualization data you first need to download the 3DCityDB Importer/Exporter tool.

**[Link to the Importer/Exporter tool download](https://www.3dcitydb.org/3dcitydb/d3dimpexp/).**

Following the instructions in the **[Documentation of 3DCityDB](https://3dcitydb-docs.readthedocs.io/en/latest/)**, a **database** needs to be set up with **PostGIS extensions**.

The Author of this project used **PostgreSQL** for the database along with **pgAdmin** as the managment software.

Then **CityGML** files need to be imported into the database using the Importer/Exporter tool.

In the **Preferences** of the tool, under **```VIS Export -> General```** the option ```Record metadata about exported features in JSON file``` needs to be ticked, to be able to use the colouring script.

The **```metadata JSON```** file contains information about the tiles of the visualization export. Namely, what buildings are on which tiles.

A visualization export can be created in the Importer/Exporter tool.

#### **Steps under the ```VIS Export``` tab:**

1. ```Geometry``` should be sellected under the ```Display as```.

2. ```Tiling``` should be enabled (box ticked) and a ```Fixed side length``` should be specified (Author used 125 for the city of Tartu data).

3. Then click ```Export```.

#### **To generate a tabular attribute file:**

This requires for a CityGML file to be imported into the database, because the attribute data is queried from the objects in the database.

under the ```Table Export``` tab:

An output file needs to be specified.

A template file needs to be specified, more info can be found about this in the **[Documentation](https://3dcitydb-docs.readthedocs.io/en/latest/plugins/spreadsheet/export.html)**.

Click **```Export```**

## Running colouring scripts on the visualization export

After generating a KML Geometry visualization export, the colouring script **```color_building_roofs.py```** functions can be used to colour the KML buildings.

Locations for the **```visualization export folder```**, **```metadata JSON```** file and **```city-attributes.json```** need to be specified in the script.

**```retrieve_solar_potential_data.py```** script can be used to find yearly kW/h data on the **```city-attributes.json```** data file.

The script can also be used to add solar potential data to the **```tabular attribute data file```**.

## Quick web-map-client local usage setup using Tartu 3D solar potential data

1. Clone this repository onto your local machine.
2. Download the Tartu 3D visualization data from [this repository](https://github.com/alankolk/Tartu_solar_visualization_data).
3. Unzip the Tartu data into the project folder directly.
4. Make sure you have Node.js installed on your local machine.
5. Run ```node server.js``` in a command prompt in the project folder.
6. Open the link in a browser **[Tartu city LOD2 solar potential visualization localhost link](http://localhost:8000/3dwebclient/index.html?t=3DCityDB-Web-Map-Client&s=false&ts=0&la=58.379595&lo=26.726688&h=1838.114&hd=360&p=-90&r=0&l_0=u%3Dhttp%253A%252F%252Flocalhost%253A8000%252Fcities%252Ftartu_data%252FTartu_geometry_MasterJSON.json%26n%3DTartu%2520-%2520Solar%2520Potential%26ld%3DCOLLADA%252FKML%252FglTF%26lp%3Dfalse%26lc%3Dtrue%26gv%3D2.0%26a%3Dtrue%26tdu%3Dhttps%253A%252F%252Fdocs.google.com%252Fspreadsheets%252Fd%252F1NxWJ4qi46FuBzyIFMG9eXsFvJ6nY5Nmd0tFZGsXFZjI%252Fedit%253Fusp%253Dshare_link%26ds%3DGoogleSheets%26tt%3DHorizontal%26gc%3Dhttp%253A%252F%252Flocalhost%253A8000%252Fcities%252Ftartu_data%252FTartu.json%26il%3D125%26al%3D1.7976931348623157e%252B308%26ac%3D150%26av%3D80&sw=showOnStart%3Dfalse)**



## License

The 3DCityDb-Web-Map-Client is licensed under the [Apache License, Version 2.0](http://www.apache.org/licenses/LICENSE-2.0). See the `LICENSE` file for more details.

The 3DCityDB-Web-Map-Client has been developed by: 

* Son H. Nguyen, Kanishk Chaturvedi, and Thomas H. Kolbe
<br>[Chair of Geoinformatics, Technical University of Munich](https://www.gis.bgu.tum.de/)

and with the support from the following cooperation partners:

* Zhihang Yao, Jannes Bolling, Lucas van Walstijn, and Claus Nagel 
<br>[Virtual City Systems, Berlin](https://vc.systems/)
