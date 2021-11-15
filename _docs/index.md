---
title: "MBON Data and File Formatting"
keywords: homepage
tags: [getting_started, about, overview]
toc: false
#permalink: index.html
summary: This documentation describes the Marine Biodiversity Observation Network (MBON) data and file formatting recommendations.
---



## Introduction

[Marine Biodiversity Observation Network (MBON)](https://ioos.noaa.gov/project/bio-data/) 
observation data is focused on organisms from microbes to whales, including measures of biodiversity 
(e.g. presence, abundance), productivity, genomics, phenology, and other relevant ecological process 
measurements or indices. Also featured are habitat characterization and habitat diversity measures, 
including satellite data and added-value data derived from satellite observations, and neural network 
model results, such as biogeographical seascape classifications.

The data have been generated within the MBON regions of the Arctic, Central California, Southern 
California, the Gulf of Maine, the Pacific Northwest, and South Florida. Data have been collected 
by associated scientists or provided by multiple other independent programs, such as the IOOS Regional 
Associations, Long-Term Ecological Research (LTER) programs, universities, and other fisheries or marine wildlife institutions.

This document describes the recommendations for formatting data and metadata for the MBON community. 
This includes:

* formatting and documentation of data

For help with the MBON Data Portal, please see the [MBON portal help documentation](https://mbon.ioos.us/help/).

## Categories of MBON observations
- Taxonomic data
- Organisms abundance
- Genetic make-up (‘omics, including informatics requirements)
- Acoustics (active and passive)
- Imaging
- Optics
- Animal tracking
- Voucher specimens

## MBON Data Flow
![mbon_data_flow](./MBON_Data_Flow.png)

For data collected/managed by an IOOS MBON project, the project should ensure data and information are readily available 
to resource managers, scientists, educators, and the public in an easily digestible way. To that end, coordination with 
an IOOS Regional Association to make the data available via ERDDAP services meets these goals. Using the services that 
ERDDAP provides, a data manager can develop a reproducible workflow for aligning the data to the 
[Darwin Core standard](https://dwc.tdwg.org/). Finally, submission to NCEI ensures that no observations are lost and 
there is long-term stewardship of these data, as well as meeting our PARR requirements. The sections below provide more 
context as well as tips and tricks for each of the elements in the diagram above.

### RA ERDDAP
For the IOOS MBON projects ERDDAP is used as a mechanism for quickly and efficiently sharing biological observations with 
the broader community. While ERDDAP can provide data access following the FAIR principles, further alignment to Darwin 
Core and submission to OBIS is necessary to make these observations more useful to a broader audience. Essentially, serving
data through an RA ERDDAP is one part of a larger process and should be treated as such.

When preparing a dataset to be served via ERDDAP it is recommended to follow a few key principles for data management. 
* For organizing your data files, follow the [Tidy data](https://r4ds.had.co.nz/tidy-data.html) recommendations:
  * Variables as columns
  * Observations as rows
  * Don't embed data in the column headers.
* Follow [ISO-8601](https://en.wikipedia.org/wiki/ISO_8601) for dates
  * YYYY-MM-DDTHH:mm:ssZ (eg. 2021-08-19T12:38:22Z)
  * Include the time zone.
* Latitude and Longitude in decimal degrees (WGS84 preferred)
* Identify units of measure
* Check species names against [WoRMS](https://www.marinespecies.org/).

See the sections below on [Data and File Formatting](#data-and-file-formatting) and 
[Metadata and Documentation](#metadata-and-documentation) for more recommendations and best practices.

**Additional Resources**
* [Configuring datasets.xml](https://coastwatch.pfeg.noaa.gov/erddap/download/setupDatasetsXml.html) - The ERDDAP manual 
for configuring a dataset.
* [ERDDAP Google Group](https://groups.google.com/g/erddap) - A great place to search for questions and ask your 
questions.

#### ERDDAP Requirements

Below is a list of the absolute bare minimum pieces of metadata required by ERDDAP. Some dataset types might have other 
requirements specific to the data file formats.
* Global attributes
  * [datasetID](https://coastwatch.pfeg.noaa.gov/erddap/download/setupDatasetsXml.html#datasetID)
  * [sourceUrl](https://coastwatch.pfeg.noaa.gov/erddap/download/setupDatasetsXml.html#sourceUrl) - however, depends on 
dataset type
  * [infoUrl](https://coastwatch.pfeg.noaa.gov/erddap/download/setupDatasetsXml.html#infoUrl)
  * [institution](https://coastwatch.pfeg.noaa.gov/erddap/download/setupDatasetsXml.html#institution)
  * [summary](https://coastwatch.pfeg.noaa.gov/erddap/download/setupDatasetsXml.html#summary)
  * [title](https://coastwatch.pfeg.noaa.gov/erddap/download/setupDatasetsXml.html#title)
* Variable attributes
  * [dataVariable](https://coastwatch.pfeg.noaa.gov/erddap/download/setupDatasetsXml.html#dataVariable)
  * [sourceName](https://coastwatch.pfeg.noaa.gov/erddap/download/setupDatasetsXml.html#sourceName)

#### ERDDAP Tips and Tricks
* Date/time - It is not a requirement to have a variable assigned to `time`  (ie. 
`<destinationName>time</destinationName>`) in ERDDAP. If a variable's destinationName is set to `time`, ERDDAP will use 
the `units` attribute to attempt to interpret the datum. See the documentation on [How ERDDAP Deals with 
Time](https://coastwatch.pfeg.noaa.gov/erddap/convert/time.html#erddap) for more information.
  * *Trick* - If you don't want the variable interpreted as a time, set the `<destinationName>` to something other than 
`time`. For example, in your source file the coumn `time` has a value of `2020-01-01`, but you don't want that 
interpreted by ERDDAP. Then, set the `destinationName` to `time2` and ERDDAP will treat the field as a string. 
  * *Caution* - If you do not have an assigned `time` variable in a dataset, some of the access formats might not be 
available (eg. .esricsv, .odvtxt). 
* Latitude/Longitude - Similar to date/time above, it is not a requirement to have latitude/longitude variables. However, 
the dataset will have a limited amount of access formats.
* *Trick* - ERDDAP now has the capability to create derived variables from existing fields (since v2.10). See the 
documentation on [Script SourceNames / Derrived 
Variables](https://coastwatch.pfeg.noaa.gov/erddap/download/setupDatasetsXml.html#scriptSourceNames).
* *Trick* - ERDDAP can handle media files, such as image, audio and video files. See 
[MediaFiles](https://coastwatch.pfeg.noaa.gov/erddap/download/setupDatasetsXml.html#MediaFiles) for more information.
   * *Bonus Trick* - 
[EDDTableFromFileNames](https://coastwatch.pfeg.noaa.gov/erddap/download/setupDatasetsXml.html#MediaFiles) allows you to 
create a dataset from information about files in the file system. While it doesn't serve data from within the files it 
does provide a mechanism for sharing data in other formats (eg. zip packages, Word docs, Excel spreadsheets, etc.). The 
resultant dataset in ERDDAP is composed of the following columns: `url`, `name`, `lastModified`, and `size`.

### Darwin Core Alignment
When aligning a dataset to Darwin Core it is recommended that a data manager starts with serving the data via ERDDAP
or some comparable online system which has an [API](https://en.wikipedia.org/wiki/API) (or a way to programmatically 
grab the data). When working through the Darwin Core alignment using a scripting language (eg. R or Python) which uses 
the data served via ERDDAP (or comparable service) is highly recommended. A scripting language provides provenance, 
transparency, and reproducibility for the translation. This helps reduce the amount of errors and back-and-forth between 
data managers and OBIS. It is highly recommended that, if using a scripting language, the scripts are shared via 
distributed version control systems like [GitHub](www.github.com).

**Recommendations TL;DR;**
* Use a scripting language
* Script should point to source data on some web service
* Scripts should be shared via GitHub.

**Additional Resources**
* [Standardizing Marine Biological Data Guide](https://ioos.github.io/bio_data_guide/).

### Sending to OBIS-USA
*section on sending to OBIS-USA (TBD)* maybe a section in bio data guide?

### Sending to NCEI
See https://www.ncei.noaa.gov/archive.
In the submission package sent to NCEI, indicate that the observations are from an IOOS MBON project (or some 
affiliation with IOOS).
* [ATRAC](https://www.ncdc.noaa.gov/atrac/guidelines.html) - Use the Advanced Tracking and Resource Tool for Archive 
Collections (ATRAC) to submit repeating or multiple delivery data, or data that exceeds 20 GB.
* [S2N](https://www.nodc.noaa.gov/s2n/) - Use Send2NCEI to submit non-repeating or single delivery data less than 20 GB.

### Loading into MBON Portal
* See documentation on [contributing to the MBON portal](https://mbon.ioos.us/help/how-to/catalog/contribute-data.html).

## Data and File Formatting

In choosing a file format, data collectors should select a format that is usable, open, and that
will likely be readable well into the future. Microsoft Excel, as an example, is a useful tool for
data manipulations and data visualization, but versions of Excel files may become obsolete and may
not be easily readable over the longer term. Likewise, database management systems (DBMS) like MS
Access, Filemaker Pro, and others, can be a very effective way to store and query data, but the raw
formats tend to change over time (even a few years). If your program or organization has used these
or other proprietary DBMS tools, it is essential to plan for exporting your data in a stable,
well-documented, and non-proprietary format.

Below is a summary of the suggested tabular, image, and GIS data file formats suitable for long-term
archiving.

* Containers: TAR, GZIP, ZIP
* Databases: CSV, XML
* Tabular data: CSV
* Geospatial vector data: SHP, GeoJSON, KML, DBF, NetCDF
* Geospatial raster data: GeoTIFF/TIFF, NetCDF, HDF-EOS
* Moving images: MOV, MPEG, AVI, MXF
* Sounds: WAVE, AIFF, MP3, MXF
* Still images: TIFF, JPEG 2000, PDF, PNG, GIF, BMP
* Text: XML, PDF/A, ASCII, UTF-8

For more complete guidance on best practices and appropriate formats for long-term preservation and
future accessibility, see the
[Library of Congress’ Sustainability of Digital Formats](https://www.loc.gov/preservation/digital/formats/)
web site, the LOC’s page on [Recommended Format Specifications for 
preservation](https://www.loc.gov/preservation/resources/rfs/), and Hook et al’s recommendations in
[Best Practices for Preparing Environmental Data Sets to Share and 
Archive](https://daac.ornl.gov/PI/BestPractices-2010.pdf).

### Tabular Data

Tabular data, or data in tables or spreadsheets, is by far the most common format for presenting,
analyzing, and storing data. However, common spreadsheet file formats are not ideal for sharing,
preserving, and reusing data; they’re not easily machine readable and may be difficult or impossible
to read if the specific software tools used to create them are significantly upgraded or outmoded.

Using delimited text formats is a better way to ensure that tabular data are readable in the future.
A delimited text file is an ASCII-encoded file used to store data in which each line is uniquely
represented and had fields separated by a special character—the delimiter. Common delimiters are the
comma, tab, and colon. In a file with comma-separated values (a CSV file), the data values are
separated using commas as a delimiter. One benefit of being incredibly common and simple to use is
that most database and spreadsheet programs are able to read in or export data in a text-delimited
format.

*Comma Separated Values (CSV)* is the most common delimited data format. If your data has strings or
sentences that may contain commas, be sure to wrap all string values in quotation marks (“”) or
another delimiter that may not be present in your data. The semicolon, (;), and a tab (“ “ , or “t”)
are other common delimiters. Text delimited files can be imported and exported by almost any
software designed for storing or manipulating data, including relational database systems,
spreadsheet software, and statistical analysis software.

*ASCII (American Standard Code for Information Interchange)* is the most common text encoding and
the one most likely to be readable by tools. Other text encodings, such as UTF-8 are possible and
may be necessary for some non-English applications. Avoid obscure text encodings. Use ASCII if
possible, with UTF-8 or UTF-16 as secondary options.

*Relational database management systems (RDBMS)* (such as Microsoft Access) create file formats that
need specialized software to open and view the contained information. Creating CSV files or ASCII
text versions and PDF/A’s of the data provider’s original data ensures that the information
contained within the file is openly accessible to data customers. Tabular data stored within
relational databases should be broken out into CSV files or ASCII text versions with all table
relationships described in enough detail for the database to be recreated.

### Data Headers

In order for others to use your data, they must fully understand the contents of the dataset. Most
commonly, data values within a file are organized in rows and columns, with each event or
observation as a row and each column representing a measurement or contextual information. Use a
header row at the top of each file describing the values in column.

Follow these best practices for data headers:
* Use commonly accepted parameter names for header titles (e.g. site, date, treatment, 
units_of_measure, etc).
* Use consistent capitalization of header names (e.g. temp and precip, or Temp and Precip).
* Explicitly state units of reported parameters in the data file and the metadata.
* If a coded value of abbreviation is used, be sure to provide a definition in the metadata.
* Adopt a similar structure across data files. If the same parameters are used across multiple
files, use a file template to maintain consistent column names across files. Avoid having different
numbers of columns or rearranging columns across similar files.
* Column names or headings should contain only numbers, letters, hyphens, and underscores—no spaces
or special characters. This also applies to column names and table names in databases. Special
characters and spaces are error-prone when machine-read or edited.

### Data Values

To allow others to best understand your data, follow these best practices for values within a data
file:
* Standardize all coded and null values within a dataset.
* Use an explicit value for missing or no data, rather than an empty field. Or, distinguish between
a zero and a blank value for numeric fields.
* For numeric fields, represent missing data with a specified extreme value (e.g., -9999), the IEEE
floating point NaN value (Not a Number), or the database NULL. Be advised that NULL and NaN can
cause problems, particularly with some older programs. For character fields, use NULL, “not
applicable”, “n/a” or “none”.
* If there are multiple reasons that cells might not have values, include a separate code for each 
reason.
* The null value(s) should be consistently applied within and among data files.
* If data values are encoded, be sure to provide a definition in the metadata.
* Don’t include rows with summary statistics. It is best to put summary statistics, figures,
analyses, and other summary content into a separate companion data file.

### Specific Formatting Recommendations for Biological Data

Biological data is often stored in tabular formats such as spreadsheets and database tables.
Examples of biological datasets may include environmental data, such as temperature, salinity, or
conductivity, but focus on measuring variables related to one or more species of plant or animal.
Examples of biological data include, but are not limited to, marine bird surveys, genetic analyses
of salmon stocks, and toxicological analyses of lichen.

For biological data, the following best practices apply:

1. Align to [Darwin Core](https://dwc.tdwg.org/), when possible. 
1. Archive data in CSV (or another non-proprietary, text-based format) whenever possible.
2. Follow established conventions when naming variables or columns. Refer to the [List of Darwin Core
Terms](https://dwc.tdwg.org/list/)
3. Define distinct events (such as location, time (with time zone), and/or depth) within a file with
a unique identifier. The identifier is often presented as sample_id or collection_event_id. See 
Darwin Core term [eventID](https://dwc.tdwg.org/list/#dwc_eventID)
4. Include both the common name, the scientific name, and the
[WoRMS AphiaID code](http://www.marinespecies.org/aphia.php?p=match) for each species. The 
[ITIS Taxonomic Serial Number (TSN)](https://www.itis.gov/) is another option if WoRMS does not meet
the needs of your data.

## Metadata and Documentation

Descriptive metadata and documentation are critical to maintaining data quality. Metadata is “data
about the data” that describes and contextualizes the dataset to ensure it is understandable to
future users. Beyond standardized metadata, useful documentation might include standard operating
procedures, field notes, etc., from which metadata may be derived or referenced.

Throughout the data lifecycle, both the metadata and documentation must be recorded and updated to
reflect the actions taken to the data. This includes collection, acquisition, processing, quality
review, and analysis, as well as any other stage of the data lifecycle.

The dataset’s metadata and/or documentations (or a link to it) must be distributed with the dataset. 

### Metadata

Metadata describes information about a dataset to ensure that it can be understood and re-used
properly in the future. Content of the metadata record includes where the data were collected, who
is responsible for the data, why the data were created, how the data are organized, and any derived
data calculation methods (e.g. for fish abundance estimate) that were used. Metadata generally
follows a standard format to ensure the semantics of metadata fields are understood by creators and
consumers of the metadata, to ease the use of the metadata in catalog and discovery systems, and
simplify automatic machine-to-machine transfer of records.

There are two recomended metadata formats.
1. Ecological Markup Language (EML) - [https://eml.ecoinformatics.org/](https://eml.ecoinformatics.org/)
2. ISO 19115 family of standards - [https://www.fgdc.gov/metadata/iso-standards](https://www.fgdc.gov/metadata/iso-standards)

#### EML
The EML project is an open source, community oriented project dedicated to providing a high-quality metadata 
specification for describing data relevant to diverse disciplines that involve observational research like ecology, 
earth, and environmental science. The specification is maintained by voluntary project members who donate their time 
and experience in order to advance information management for ecology. Project decisions are made by consensus of the 
current maintainers on the project.

See this documentation for more information:
Matthew B. Jones, Margaret O’Brien, Bryce Mecum, Carl Boettiger, Mark Schildhauer, Mitchell Maier, Timothy Whiteaker, 
Stevan Earl, Steven Chong. 2019. Ecological Metadata Language version 2.2.0. KNB Data Repository. doi:[10.5063/F11834T2](https://dx.doi.org/10.5063/F11834T2)


#### ISO
It is recommended to use the ISO 19115-2 XML for metadata standards following the ISO 19115 guidance from
[NCEI](https://www.ncei.noaa.gov/sites/default/files/2021-03/AB-GUID-02823_R1_Guidance%20for%20The%20NCEI%20Collection%20Level%20Metadata%20Template%20v1.1._0.pdf).
See also [NCEI's guidance on Metadata](https://www.ncei.noaa.gov/resources/metadata).

Methods for generating metadata:
* Various software packages exist to create EML metadata. See the list of tools in the [standardizing marine biological 
data guide](https://ioos.github.io/bio_data_guide/tools.html#tools). 
* If data are being served by ERDDAP, then ERDDAP will automatically generate the ISO XML documents.
* If using the [Research Workspace](https://researchworkspace.com/intro/) to submit data, an
integrated metadata editor is included to generate metadata in the FGDC-endorsed ISO 19110 and
19115-2 standards for geospatial metadata. Refer to the
[Metadata Best Practices](https://www.axiomdatascience.com/best-practices/MetadataBestPractices.html#metadata-best-practices)
section for help creating scientific metadata using the Research Workspace metadata editor. This
document provides field-by-field guidance on how to write high-quality metadata.

### Additional Data Documentation

* Save documentation about the data in non-proprietary file formats, such as .txt, .xml, or .pdf.
* Images, pictures, or figures should be saved as JPEG or GIF files.
* The name of the documentation should follow a logical naming convention identical to the related
data file(s), but indicating that the file is a metadata record, e.g. `[data_file_name]_METADATA.xml`.
* For complicated datasets, supplemental documentation is more useful when structured as a user’s
guide for the data. When constructing such a guide, include enough detail for someone with
sufficient domain knowledge to understand, trust, and reuse your data 20+ years in the future.
