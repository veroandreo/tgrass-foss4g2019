# Spatio-temporal data processing and visualization with GRASS GIS

<sub>Verónica Andreo<sup>1</sup>, Martin Landa<sup>2</sup>, Ondřej Pešek<sup>3</sup>, Markus Neteler<sup>4</sup>, Luca Delucchi<sup>5</sup> & Moritz Lennert<sup>6</sup></sub>


[GRASS GIS](https://grass.osgeo.org) is a general purpose Free and Open 
Source GIS that offers raster, 3D raster and vector data processing support.
GRASS GIS has also incorporated a powerful support for time series, 
the so called **TGRASS**. Through this, it became the first open source 
temporal GIS with comprehensive spatio-temporal analysis, processing and
visualization capabilities. 
The temporal functionality **makes it easy to manage, analyse and 
visualize climatic data, vegetation index time series, harvest data or 
land use changes over time**. Raster, vector and 3D raster time series 
are handled through a special data type called **space time data sets 
(STDS)** which are used as input in TGRASS modules. TGRASS incredibly 
simplifies the processing and analysis of large time series of hundreds 
of thousands of maps. For example, users can aggregate a daily time 
series into a monthly time series in just a single line; they can 
retrieve the date per year in which a certain value is reached; select 
maps from a time series in time periods in which a different time 
series reaches a certain value; perform different temporal as well as 
spatial operations among time series, and so much more. 

In this 4-hours hands-on workshop we will present and exemplify the use 
of a subset of the more than 45 temporal modules in combination with 
other GRASS GIS modules and Add-ons in a workflow starting from the 
download of remote sensing data to the creation of a simple model and 
visualization of results. We will first learn how go to create STDS and 
assign time stamps to maps. In addition, we will learn different methods
to gap-fill incomplete data, temporal algebra operations, temporal 
aggregation, queries and retrieval of basic and zonal statistics for 
time series. All along the session, we ll see different visualization 
options available in GRASS GIS. Moreover, we will show how this 
workflow might be included in python scripts and executed from outside 
GRASS GIS.


**Author's affiliations:**

<sub>
<sup>1</sup> Instituto Nacional de Medicina Tropical (INMeT) - Consejo Nacional de Investigaciones Científicas y Técnicas (CONICET). Puerto Iguazú, Argentina.
<sup>2</sup> Czech Technical University in Prague. Czech Republic.
<sup>3</sup> JRC - Joint Research Centre. Ispra, Italy.
<sup>4</sup> mundialis GmbH & Co. KG. Bonn, Germany.
<sup>5</sup> Fondazione Edmund Mach. San Michele all’Adige, Italy.
<sup>6</sup> Université Libre de Bruxelles. Belgium.
</sub>


<p align="right">
    <img src="https://2019.foss4g.org/wp-content/uploads/2018/07/logo-site.png" width="250">
    <img src="https://grass.osgeo.org/images/logos/grasslogo.svg" width="150">
</p>

## Presentations

* [Brief Intro to GRASS GIS](https://github.com/veroandreo/tgrass-foss4g2019/blob/master/pdf/intro.pdf)
* [Temporal GRASS GIS](https://github.com/veroandreo/tgrass-foss4g2019/blob/master/pdf/tgrass.pdf)

## Software

We will use **GRASS GIS 7.6.1** (current stable version). It can be installed either 
through standalone installers/binaries or through OSGeo-Live (which includes all
OSGeo software and packages). See this 
[**Installation guide**](https://gitlab.com/veroandreo/grass-gis-conae/-/blob/master/pdf/00_installation.pdf) 
for details (Follow only the GRASS GIS part).

### Standalone installers for different OS:

##### MS Windows

There are two different options:
1. Standalone installer: [32-bit version](https://grass.osgeo.org/grass76/binary/mswindows/native/x86/WinGRASS-7.6.1-1-Setup-x86.exe) | [64-bit version](https://grass.osgeo.org/grass76/binary/mswindows/native/x86_64/WinGRASS-7.6.1-1-Setup-x86_64.exe) 
2. OSGeo4W package (network installer): [32-bit version](http://download.osgeo.org/osgeo4w/osgeo4w-setup-x86.exe) | [64-bit version](http://download.osgeo.org/osgeo4w/osgeo4w-setup-x86_64.exe) 

For Windows users, **we strongly recommend installing GRASS GIS through the OSGeo4W package** (second option), 
since it allows to install all OSGeo software. If you choose this option, 
*make sure you select GRASS GIS and msys*. The latter one will allow 
the use of loops, back ticks, autocomplete, history and other nice bash shell
features.

##### Ubuntu Linux

Install GRASS GIS 7.6.1 from the "unstable" package repository:

```
sudo add-apt-repository ppa:ubuntugis/ubuntugis-unstable
sudo apt-get update
sudo apt-get install grass grass-gui grass-dev
```

##### Fedora, openSuSe Linux

For other Linux distributions including **Fedora** and **openSuSe**, simply install GRASS GIS with the respective package manager. See also [here](https://grass.osgeo.org/download/software/)

### OSGeo-live: 

[OSGeo-live](https://live.osgeo.org/) is a self-contained bootable DVD, USB thumb
drive or Virtual Machine based on Lubuntu, that allows you to try a wide variety
of open source geospatial software without installing anything. There are 
different options to run OSGeo-live:

* [Run OSGeo-live in a Virtual Machine](https://live.osgeo.org/en/quickstart/virtualization_quickstart.html)
* [Run OSGeo-live from a bootable USB flash drive](https://live.osgeo.org/en/quickstart/usb_quickstart.html)

For a quick-start guide, see: https://live.osgeo.org/en/quickstart/osgeolive_quickstart.html

### GRASS GIS Add-ons that will be used during the course

* [i.modis](https://grass.osgeo.org/grass7/manuals/addons/i.modis.html): Toolset to download and process MODIS products. It requires [ pyModis](http://www.pymodis.org/info.html#how-to-install-pymodis) library.
* [v.strds.stats](https://grass.osgeo.org/grass7/manuals/addons/v.strds.stats.html): Zonal statistics from given space-time raster datasets based on a polygons vector map

Install with `g.extension extension=name_of_addon`

## Data

* [North Carolina basic location (approx. 50Mb)](https://grass.osgeo.org/sampledata/north_carolina/nc_basic_spm_grass7.zip): download and unzip within `$HOME/grassdata`.
* [modis_lst mapset (2Mb)](https://gitlab.com/veroandreo/curso-grass-gis-rioiv/raw/master/data/modis_lst.zip?inline=false): download and unzip within the North Carolina location in `$HOME/grassdata/nc_basic_spm_grass7`.
* [nc_state vector map](https://github.com/veroandreo/tgrass-foss4g2019/blob/master/data/nc_state.pack): download in `$HOME`, we'll unpack it during the workshop. 
* [urbanarea vector map](https://github.com/veroandreo/tgrass-foss4g2019/blob/master/data/urbanarea.pack): download in `$HOME`, we'll unpack it during the workshop.

Your `grassdata` folder should look like this:

```
  grassdata/
   ├── nc_basic_spm_grass7
     ├── modis_lst
     ├── PERMANENT
     └── user1
```

## References

- Neteler, M. and Mitasova, H. (2008): *Open Source GIS: A GRASS GIS Approach*. Third edition. ed. Springer, New York. [Book site](https://grassbook.org/)
- Neteler, M., Bowman, M.H., Landa, M. and Metz, M. (2012): *GRASS GIS: a multi-purpose Open Source GIS*. Environmental Modelling & Software, 31: 124-130 [DOI](http://dx.doi.org/10.1016/j.envsoft.2011.11.014)
- Gebbert, S. and Pebesma, E. (2014). *A temporal GIS for field based environmental modeling*. Environmental Modelling & Software, 53, 1-12. [DOI](https://doi.org/10.1016/j.envsoft.2013.11.001)
- Gebbert, S. and Pebesma, E. (2017). *The GRASS GIS temporal framework*. International Journal of Geographical Information Science, 31, 1273-1292. [DOI](http://dx.doi.org/10.1080/13658816.2017.1306862)
- Gebbert, S., Leppelt, T. and Pebesma, E. (2019). *A Topology Based Spatio-Temporal Map Algebra for Big Data Analysis*. Data, 4, 86. [DOI](https://doi.org/10.3390/data4020086)

## License

All the course material:

[![Creative Commons License](assets/img/ccbysa.png)](http://creativecommons.org/licenses/by-sa/4.0/) Creative Commons Attribution-ShareAlike 4.0 International License

Presentations were created with [gitpitch](https://gitpitch.com/):

* MIT License
