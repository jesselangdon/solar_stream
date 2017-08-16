---
title: Home
weight: 1
---

## Summary
The [Integrated Status and Effectivness Monitoring Program](https://isemp.org) (ISEMP) will 
be developing a gross primary production (GPP) model for stream networks in the Columbia 
Basin in order to make spatially-explicit predictions regarding salmonid habitat needs. 
Solar insolation directly affects stream temperature (Sinokrot and Stefan, 1993) and the 
primary productivity of streams (Fisher and Likens, 1973; Hill et al., 1995). Eco Logical 
Research, Inc. has explored using areal solar insolation as an input parameter for a 
forthcoming gross primary production model. South Fork Research, Inc. (SFR) is investigating 
methods for modeling solar insolation of streams in the Columbia Basin. Specifically, SFR 
seeks to develop a methodology for modeling solar insolation that will more closely emulate 
the effects of shading from riparian vegetation and topography.

The [Columbia Habitat Monitoring Program](https://www.champmonitoring.org/) (CHaMP) protocol 
requires the collection of solar insolation data during stream surveys, however, collecting 
field-based solar insolation measurements comprehensively for the entire stream network of 
the Columbia Basin is resource prohibitive. Developing a spatially-explicit model to predict 
solar insolation for all stream networks and associated riparian buffers within the Columbia 
Basin will potentially provide a robust, reliable input for GPP modeling efforts, and may 
preclude the need for field-based data collection. 

To date, our solar modeling efforts have relied on raster data derived from the National Biomass 
and Carbon Dataset (NBCD) basal area-weighted canopy height dataset. The [NBCD](http://www.whrc.org/mapping/nbcd) 
was developed by the Woods Hole Research Center in 2000, and combines high-resolution inSAR data 
acquired by the 2000 Shuttle Radar Topography Mission (SRTM), US Forest Service Forest Inventory 
and Analysis (FIA) data, and remotely-sensed data from the Landsat ETM+ sensor. The tool then 
combines basal area-weighted canopy height values with bare-earth topographic values from a 
high-resolution digital elevation model (DEM), resulting in a relatively close approximation of 
stream shading, when calculating solar insolation using ESRI’s[Area Solar Radiation](http://desktop.arcgis.com/en/arcmap/10.3/tools/spatial-analyst-toolbox/area-solar-radiation.htm) 
tool. While 
we have obtained good results using NBCD basal area-weighted canopy height data, any vegetation 
height raster dataset (with elevation values in meters) will work as an input for the tool.

It is recommended that prior to using this tool, the required stream network input be segmented 
using the [Geomorphic Network and Analysis Toolbox (GNAT) Segment Stream Network](https://bitbucket.org/KellyWhitehead/geomorphic-network-and-analysis-toolbox).

* [Downloads](releases)
* [Validation](validation)

## Using the Solar Stream Tools

### Data Input Requirements:

* NHD+ 1:24k flowlines, segmented
* DEM 10m<sup>2</sup> raster dataset
* Stream area polygon dataset (i.e. bankfull or USGS NHD Area)
* NBDC canopy height raster dataset

### Suggested User Workflow

1. Clip all data inputs using a watershed or hydrologic unit polygon
2. Convert all inputs to the same projected coordinate systems.
3. Split reaches in the stream network into segments of uniform length (based on a user-supplied 
length interval) using the [GNAT - Segment Stream Network](https://github.com/SouthForkResearch/gnat) tool.
4. Run the **Generate Solar Insolation Surface** tool. 
5. Using the resulting raster dataset as an input, run the **Solar Insolation for a Stream Network** 
tool, which results in a stream network polyline feature class with summarized solar insolation values 
stored in an attribute field. 

#### Automated Workflow

1. Converts the stream network and stream area polyon vector datasets into rasters and merges together 
into a single stream water surface raster.
2. Converts stream water surface water raster into a polygon and splits by stream segments.
3. Removes the stream surface raster from the NBCD canopy height raster dataset.
4. Merges the canopy height raster with the “bare earth” DEM.
5. Using the merged canopy height/bare earth DEM raster dataset, calculates solar insolation.
6. Calculate mean solar insolation per segmented stream polygons using Zonal Statistics
7. Join zonal statistics output back to segmented stream network polyline dataset
8. Export result to new stream network polyline dataset, with solar insolation values added as an attribute field.
9. Solar insolation output has units of watt hours per square meter (WH/m<sup>2</sup>).

### Citation

* Fisher, S. G. and G. E. Likens (1973). "Energy Flow in Bear Brook, New Hampshire: An Integrative 
Approach to Stream Ecosystem Metabolism." Ecological monographs 43(4): 421-439.
* Hill, W. R., et al. (1995). "Light Limitation in a Stream Ecosystem: Responses by Primary Producers 
and Consumers." Ecology 76(4): 1297-1309.
* Sinokrot, B. A. and H. G. Stefan (1993). "Stream temperature dynamics: Measurements and modeling." 
Water Resources Research 29(7): 2299-2312.

### Acknowledegments

The Solar Streams model and tool is actively developed and maintained by [South Fork Research, Inc.](http://southforkresearch.org) (SFR). Funding for these
tools was provided by the Bonneville Power Administration (BPA).

### License

Licensed under the [GNU General Public License Version 3](../License.txt).