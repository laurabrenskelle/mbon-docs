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
by associated scientists or provided by multiple other independent programs, such as the Long-Term 
Ecological Research (LTER) programs, universities, and other fisheries or marine wildlife institutions.

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
![mbon_data_flow](images/MBON Data Flow v1.3_transparent_noauthor.png)

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
* Statistics: ASCII, DTA, POR, SAS, SAV
* Still images: TIFF, JPEG 2000, PDF, PNG, GIF, BMP
* Text: XML, PDF/A, HTML, ASCII, UTF-8
* Web archive: WARC

For more complete guidance on best practices and appropriate formats for long-term preservation and
future accessibility, see the
[Library of Congress’ Sustainability of Digital Formats](https://www.loc.gov/preservation/digital/formats/)
web site, the LOC’s page on [Recommended Format Specifications for preservation](https://www.loc.gov/preservation/resources/rfs/),
and Hook et al’s recommendations in
[Best Practices for Preparing Environmental Data Sets to Share and Archive](https://daac.ornl.gov/PI/BestPractices-2010.pdf).

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
* Use commonly accepted parameter names for header titles (e.g. site, date, treatment, units of
measure, etc).
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
* If there are multiple reasons that cells might not values, include a separate code for each reason.
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

For biological data submitted to the MBON portal, the following best practices apply:

1. Archive data in CSV (or another non-proprietary, text-based format) whenever possible.
2. Follow established conventions when naming variables or columns. Refer to the
IOOS Biological Data Terminology for a list of data fields with names, descriptions, and format notes.
3. Define distinct events (such as location, time (with time zone), and/or depth) within a file with
a unique identifier. The identifier is often presented as sample_id or collection_event_id.
4. Include both the common name, the scientific name, and the
[ITIS Taxonomic Serial Number (TSN)](https://www.itis.gov/) and/or
[WoRMS AphiaID code](http://www.marinespecies.org/aphia.php?p=match) for each species.
5. For visualization of data in the MBON portal, it is best to normalize data to a scale such that
different factors can be compared. Normalized data is often presented as count per area, count per
volume, catch per unit effort, etc. Normalized data should be clearly differentiated from
non-normalized values if presented within the same data file.

## Metadata and Documentation

Descriptive metadata and documentation are critical to maintaining data quality. Metadata is “data
about the data” that describes and contextualizes the dataset to ensure it is understandable to
future users. Beyond standardized metadata, useful documentation might include standard operating
procedures, field notes, etc., from which metadata may be derived or referenced.

Throughout the data lifecycle, both the metadata and documentation must be recorded and updated to
reflect the actions taken to the data. This includes collection, acquisition, processing, quality
review, and analysis, as well as any other stage of the data lifecycle.

The dataset’s metadata and/or documentations (or a link to it) must be distributed with the
biological dataset for submission to MBON data portal. The metadata will be made available alongside
the dataset within the portal.

### Metadata

Metadata describes information about a dataset to ensure that it can be understood and re-used
properly in the future. Content of the metadata record includes where the data were collected, who
is responsible for the data, why the data were created, how the data are organized, and any derived
data calculation methods (e.g. for fish abundance estimate) that were used. Metadata generally
follows a standard format to ensure the semantics of metadata fields are understood by creators and
consumers of the metadata, to ease the use of the metadata in catalog and discovery systems, and
simplify automatic machine-to-machine transfer of records.

It is recommended to use the ISO 19115 XML for metadata standards following the ISO 19115 guidance from
[NGDC](https://www.ngdc.noaa.gov/metaview/page?xml=NOAA/NESDIS/NGDC/STP/Geomag/iso/xml/G10161.xml&view=xml2text/xml-to-text-ISO)
and [NCDDC](https://www.ncddc.noaa.gov/metadata-standards/).
See also the [Category:ISO 19115 in the NOAA Environmental Data Management Wiki](https://geo-ide.noaa.gov/wiki/index.php?title=Category%3AISO_19115).
If data are being served by ERDDAP, then ERDDAP will automatically generate the ISO and FGDC XML documents.
Metadata in the [FGDC-authored Content Standard for Digital Geospatial Metadata (CSDGM)](https://www.fgdc.gov/metadata/csdgm-standard)
format may also be submitted following the
[Content Standard for Biological Data Profile](https://www.fgdc.gov/standards/projects/metadata/biometadata/biodatap.pdf).

If using the [Research Workspace](https://researchworkspace.com/intro/) to submit data, an
integrated metadata editor is included to generate metadata in the FGDC-endorsed ISO 19110 and
19115-2 standards for geospatial metadata. Refer to the
[Metadata Best Practices](https://www.axiomdatascience.com/best-practices/MetadataBestPractices.html#metadata-best-practices)
section for help creating scientific metadata using the Research Workspace metadata editor. This
document provides field-by-field guidance on how to write high-quality metadata.

### Additional Data Documentation

* Save documentation about the data in non-proprietary file formats, such as .txt, .xml, or .pdf.
* Images, pictures, or figures should be saved as JPEG or GIF files.
* The name of the documentation should follow a logical naming convention identical to the related
data file(s), but indicating that the file is a metadata record, e.g. [data_file_name]_METADATA.xml.
* For complicated datasets, supplemental documentation is more useful when structured as a user’s
guide for the data. When constructing such a guide, include enough detail for someone with
sufficient domain knowledge to understand, trust, and reuse your data 20+ years in the future.
