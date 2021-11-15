---
title: "Data Flow"
keywords: data
tags: [biology, dataflow]
toc: true
summary: This is a summary of the Marine Biodiversity Observation Network (MBON) data flow.
---

# MBON Data Flow
<div style="text-align: center"><img src="./MBON_Data_Flow.png" width="100" />
</div>
Idealized data flow for IOOS biological observations.
{: style="color:gray; font-size: 80%; text-align: center;"}


<br />

For data collected/managed by an IOOS MBON project, the project should ensure data and information are readily available
to resource managers, scientists, educators, and the public in an easily digestible way. To that end, coordination with
an IOOS Regional Association to make the data available via ERDDAP services meets these goals. Using the services that
ERDDAP provides, a data manager can develop a reproducible workflow for aligning the data to the
[Darwin Core standard](https://dwc.tdwg.org/). Finally, submission to NCEI ensures that no observations are lost and
there is long-term stewardship of these data, as well as meeting our PARR requirements. The sections below provide more
context as well as tips and tricks for each of the elements in the diagram above.

## RA ERDDAP
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
  * `YYYY-MM-DDTHH:mm:ssZ` (eg. 2021-08-19T12:38:22Z)
  * Include the time zone.
* Latitude and Longitude in decimal degrees (WGS84 preferred)
* Identify units of measure
* Check species names against [WoRMS](https://www.marinespecies.org/).

See the sections below on [Data and File Formatting](data.html) and
[Metadata and Documentation](metadata.html) for more recommendations and best practices.

**Additional Resources**
* [Configuring datasets.xml](https://coastwatch.pfeg.noaa.gov/erddap/download/setupDatasetsXml.html) - The ERDDAP manual
for configuring a dataset.
* [ERDDAP Google Group](https://groups.google.com/g/erddap) - A great place to search for questions and ask your
questions.

### ERDDAP Requirements

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

### ERDDAP Tips and Tricks
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

## Darwin Core alignment
When aligning a dataset to Darwin Core it is recommended that a data manager starts with serving the data via ERDDAP
or some comparable online system which has an [API](https://en.wikipedia.org/wiki/API) (or a way to programmatically
grab the data). When working through the Darwin Core alignment using a scripting language (eg. R or Python) which uses
the data served via ERDDAP (or comparable service) is highly recommended. A scripting language provides provenance,
transparency, and reproducibility for the translation. This helps reduce the amount of errors and back-and-forth between
data managers and OBIS. It is highly recommended that, if using a scripting language, the scripts are shared via
distributed version control systems like [GitHub](https://www.github.com).

**Recommendations TL;DR;**
* Follow the guidance at [TDWG's Darwin Core quire reference guide](https://dwc.tdwg.org/terms/).
* Use a scripting language.
* Script should point to source data on a hosted web service.
* Scripts should be shared via GitHub.

**Additional Resources**
* [Standardizing Marine Biological Data Guide](https://ioos.github.io/bio_data_guide/).
* [Aligning data to Darwin Core notebook in IOOS CodeLab](https://ioos.github.io/ioos_code_lab/content/code_gallery/data_management_notebooks/2020-12-08-DataToDwC.html).

## Sending to OBIS-USA
*section on sending to OBIS-USA (TBD)* maybe a section in bio data guide?

## Sending to NCEI
See [https://www.ncei.noaa.gov/archive](https://www.ncei.noaa.gov/archive) for more information.

In the submission package sent to NCEI, indicate that the observations are from an IOOS MBON project (or some
affiliation with IOOS).
* [ATRAC](https://www.ncdc.noaa.gov/atrac/guidelines.html) - Use the Advanced Tracking and Resource Tool for Archive
Collections (ATRAC) to submit repeating or multiple delivery data, or data that exceeds 20 GB.
* [S2N](https://www.nodc.noaa.gov/s2n/) - Use Send2NCEI to submit non-repeating or single delivery data less than 20 GB.

## Loading into MBON Portal
* See documentation on [contributing to the MBON portal](https://mbon.ioos.us/help/how-to/catalog/contribute-data.html).