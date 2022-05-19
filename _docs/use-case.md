---
title: "MBON use case"
keywords: data
tags: [biology, data, example]
toc: true
summary: This is a collection of IOOS Marine Biodiversity Observation Network (MBON) data flow use cases.
---
## Gulf of Maine Wilkinson Basin Time Series Station Calanus Abundance Observations

### Background
Gulf of Maine Wilkinson Basin Time Series Station (WBTS) Calanus Abundance Observations data collection was supported by multiple awards to NERACOOS, the University of New Hampshire and the University of Maine from various funding agencies, including NSF, NOAA and BOEM.

Projects: NERACOOS ISMN (Integrated Sentinel Monitoring Network)- MBON (Marine Biodiversity Observation Network) Gulf of Maine Plankton Observation Time Series: Wilkinson Basin Time Series Station (WBTS)

Creator: Jeffrey Runge, Ph.D (School of Marine Sciences, University of Maine, Darling Marine Center)
Data processor: Dylan Pugh

### Data Flow Diagram
ERDDAP -> DwC -> OBIS IPT

### Serving raw data via IOOS RA ERDDAP
Raw Gulf of Maine WBTS Calanus Abundance Observations available in ERDDAP: <http://www.neracoos.org/erddap/tabledap/WBTS_CFIN_2005_2017.html>

### Aligning raw data to Darwin Core
This dataset was processed by Dylan Pugh during the 2022 Marine BioData Mobilization Workshop in the notebook linked below:

**MBTS MBON process:** <https://github.com/ioos/bio_data_guide/tree/main/datasets/WBTS_MBON>

### Sending data to OBIS-USA
Data were submitted to OBIS-USA by contributing the Darwin Core aligned files (and code) to the [ioos/bio-data-guide](https://github.com/ioos/bio_data_guide) repository. See this [GitHub Issue](https://github.com/ioos/bio_data_guide/issues/102) and subsequent Pull Requests [here](https://github.com/ioos/bio_data_guide/pull/101) and [here](https://github.com/ioos/bio_data_guide/pull/108) for more information on the conversion process.

The processed files were uploaded to the repository and OBIS-USA downloaded them for loading in the OBIS-USA IPT.

Data were published via the OBIS-USA IPT at: <https://www1.usgs.gov/obis-usa/ipt/resource?r=gom_wbts_mesozooplankton>.

### Sending data to NCEI
*Describe the process for sending data to NCEI, including lessons learned. Include link to NCEI.*

### Loading data into MBON Portal
*Describe the process for loading data into MBON portal, including lessons learned. Include link to MBON portal layer.*

### Overall lessons learned
*Include any overarching lessons learned here.*
