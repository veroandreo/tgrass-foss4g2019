# Spatio-temporal data processing and visualization with GRASS GIS


Verónica Andreo<sup>1</sup>, Martin Landa<sup>2</sup>, Ondřej Pešek<sup>3</sup>, Markus Neteler<sup>4</sup>, Luca Delucchi<sup>5</sup> & Moritz Lennert<sup>6</sup>


<sup>1</sup> Instituto Nacional de Medicina Tropical (INMeT) - Consejo Nacional de Investigaciones Científicas y Técnicas (CONICET). Puerto Iguazú, Argentina.

<sup>2</sup> Czech Technical University in Prague. Czech Republic.
 
<sup>3</sup> JRC - The Joint Research Centre. Ispra, Italy.

<sup>4</sup> mundialis GmbH & Co. KG. Bonn, Germany.

<sup>5</sup> Fondazione Edmund Mach. San Michele all’Adige, Italy.

<sup>6</sup> Université Libre de Bruxelles. Belgium.


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

<p align="center">
    <img src="https://2019.foss4g.org/wp-content/uploads/2018/07/logo-site.png" width="250">
    <img src="https://grass.osgeo.org/uploads/images/logo/grassgis_logo_colorlogo_text_alphabg.png" width="150">
    <img src="https://2019.foss4g.org/wp-content/uploads/2018/07/logo-site.png" width="250">
</p>

## Presentations

* [Intro](https://gitpitch.com/veroandreo/tgrass-foss4g2019/master?p=slides/intro)
* [TGRASS](https://gitpitch.com/veroandreo/tgrass-foss4g2019/master?p=slides/tgrass)

## Software

We will use **GRASS GIS 7.6.1** (current stable version). It can be installed either 
through standalone installers/binaries or through OSGeo-Live (which includes all
OSGeo software and packages). See the 
[**Installation guide**](https://gitpitch.com/veroandreo/grass-gis-conae/master?p=slides/00_installation&grs=gitlab) 
presentation for details.

### Standalone installers for different OS:

##### MS Windows

There are two different options:
1. Standalone installer: [32-bit version](https://grass.osgeo.org/grass76/binary/mswindows/native/x86/WinGRASS-7.6.1-1-Setup-x86.exe) | [64-bit version](https://grass.osgeo.org/grass76/binary/mswindows/native/x86_64/WinGRASS-7.6.1-1-Setup-x86_64.exe) 
2. OSGeo4W package (network installer): [32-bit version](http://download.osgeo.org/osgeo4w/osgeo4w-setup-x86.exe) | [64-bit version](http://download.osgeo.org/osgeo4w/osgeo4w-setup-x86_64.exe) 

For Windows users, **we strongly recommend installing GRASS GIS through the OSGeo4W package**, 
since it allows to install all OSGeo software. If you choose this option, 
*make sure you select GRASS GIS and msys*. The latter one will allow 
the use of loops, back ticks, autocomplete, history and other nice bash shell
features.

##### Ubuntu Linux

Install GRASS GIS 7.6.1 from the "unstable" package repository:

```
sudo add-apt-repository ppa:ubuntugis/ubuntugis-unstable
sudo apt-get update
sudo apt-get install grass
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

* [i.modis](https://grass.osgeo.org/grass7/manuals/addons/i.modis.html): Toolset to download and process MODIS products using pyModis
* [r.hants](https://grass.osgeo.org/grass7/manuals/addons/r.hants.html): Approximates a periodic time series and creates approximated output
* [r.seasons](https://grass.osgeo.org/grass7/manuals/addons/r.seasons.html): Extracts seasons from a time series
* [r.regression.series](https://grass.osgeo.org/grass7/manuals/addons/r.regression.series.html): Calculates linear regression parameters between two time series
* [v.strds.stats](https://grass.osgeo.org/grass7/manuals/addons/v.strds.stats.html): Zonal statistics from given space-time raster datasets based on a polygons vector map

Install with `g.extension extension=name_of_addon`

## Data

* [North Carolina location (full dataset, 150Mb)](https://grass.osgeo.org/sampledata/north_carolina/nc_spm_08_grass7.zip): download and unzip within `$HOME/grassdata`.
* [modis_lst mapset (2Mb)](https://gitlab.com/veroandreo/curso-grass-gis-rioiv/raw/master/data/modis_lst.zip?inline=false): download and unzip within the North Carolina location in `$HOME/grassdata/nc_spm_08_grass7`.
* [modis_ndvi (15 Mb)](https://gitlab.com/veroandreo/curso-grass-gis-rioiv/raw/master/data/modis_ndvi.zip?inline=false): download and unzip within the North Carolina location in `$HOME/grassdata/nc_spm_08_grass7`.

## The trainer

**Verónica Andreo** is a researcher for [CONICET](http://www.conicet.gov.ar/?lan=en)
working at the Institute of Tropical Medicine [(INMeT)](https://www.argentina.gob.ar/salud/inmet)
in Puerto Iguazú, Argentina. Her main interests are remote sensing and GIS tools
for disease ecology research fields and applications. 
Vero is an [OSGeo](http://www.osgeo.org/) Charter member and a [FOSS4G](http://foss4g.org/) 
enthusiast and advocate. 
She is part of the [GRASS GIS Development team](https://grass.osgeo.org/home/credits/) 
and she also teaches introductory and advanced courses and workshops, especially 
on GRASS GIS [time series modules](https://grasswiki.osgeo.org/wiki/Temporal_data_processing)
and their applications.

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
