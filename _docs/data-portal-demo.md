---
title: "MBON Data Portal Demonstration"
keywords: homepage
tags: [getting_started, about, overview]
toc: false
summary: This page demonstrates the MBON Data Portal and some of the tools in the portal.
---

# BeachCOMBERS - Effort Based Beach Cast Surveys
_20 Years of Data_

**About this document**

CeNCOOS (<https://www.cencoos.org>) (Central and Northern California Ocean Observing System) working with the BeachCOMBERS 
program, aggregated beach cast surveys of marine mammals and seabirds from BeachCOMBERS, Beach Watch (<https://farallones.org/beach-watch>), 
and the Marine Mammal Stranding Program (<http://gsp.humboldt.edu/Projects/MMSP/Site1/aboutus.html>) at Cal Poly Humboldt. 
These data, when combined cover surveys from Del Norte County down to Los Angeles County for over 25 years. 
These data have been made available in the California Ocean Observing Systems Data Portal (<https://data.caloos.org/>), which in 
addition to the COMBERS data, is jam packed with other marine data including data from moorings, satellite, R.O.V surveys, 
and oceanographic and atmospheric models. 

Here, we are going to walk through some of the tools in the portal and access some of the COMBERS data that many of you 
have helped collect. 

_Note: If you get lost or want to skip ahead, there are links to the portal along the way._

* TOC
{:toc}

## Open the Data Portal
Note: The data portal works best using the Firefox and Chrome web browsers. 

The Cal OOS Portal can be accessed by going to data.caloos.org The portal has three main components:
1.	The Map Layer
2.	The Data Catalog (which can also be accessed in the Map Layer
3.	The Glider Visualizer (which we are not going to cover today)
To get to the **Catalog Layer** click on the **Search 1000+ Datasets** button.

[Screenshot of clicking on link]

Now let’s search for the BeachCOMBERS data. This is part of the Data Layer named **Effort-based surveys**, **Northern and 
Central California Beaches**, **Seabirds and Marine Mammals**, but the **Data Catalog** is pretty smart and each dataset includes 
a set of tags that are used to classify different types of data. 

_Note: There are many advanced ways to filter queries in the **Data Catalog** that we won't be covering here, but can be 
accessed by selecting the **Advanced** button underneath the search bar_

[Screenshot of catalog]

## Add Data Layer to the map
Once we find the dataset we want, we can add it to the Map Layer by selecting the Layers button and then the Add to map button. 

Here we also can read a narrative about the dataset, which includes a description of how different metrics are calculated as 
well as a link to the ISO metadata record for those who want to dive deeper.

[Screenshot of searching data catalog]

## Navigating the Map Layer (Click on the Map Button) 
Here we can visualize many types of data both spatially and temporally. 

Each different dataset is called a **Layer**. 

By default, the real-time sensors data layer will be displayed.

[Screenshot of map w/ sensor layer]

There is a lot going on here! Let’s focus on the blue **Navigation Header** at the top of the portal.

[Screenshot of tabs at top of map sensor layer]

**There are seven Tabs here**:
1. **Catalog** - This takes us to the Data Catalog
2. **Map** -This will take us to the Catalog entry for a loaded data layer
3. **Data Views** -These are collections on plots from different Data Layers (we'll come back to this soon) 
4. **Settings** - Here you can change things like the Units and color schemes 
5. **Share** -This will generate a unique link to what you are currently seeing in the portal. This can be shared with others or used to regenerate the portal in its current state. 
6. **Help** - Here you find links to the help documents and an interactive guide to the portal 
7. **Feedback** -This is a great way to report bugs, ask questions, or open a line of communication with us! We track all of the feedback and appreciate any comments.

## Exploring the Data 
Now let’s go back to the map by clicking on **Map** button.

[Screenshot of map w/ sensor layer]

It looks very busy, so let’s go over how to use the **Map**.

Currently, we have two data Layers loaded up. First the Seabird carcass layer and the Real-Time sensor layer, which is 
loaded by default (See [Appendix for how to use this layer](https://www.cencoos.org/images/tutorials/COMBERS_portal_tutorial_V2.html#sensor_layer)). 

In the meantime, let’s hide this layer. 

Under the **Legend** tab select the **eyeball icon with a slash** next to the title of the layer. Selecting this again 
will re-enable the layer.

[Screenshot of legend from map w/ eyeball highlighted]

**Zooming into Monterey Bay**

[Screenshot w/ zoom tools highlighted]

Zooming in the portal can be accomplished a couple of different ways:
1. The Plus and Minus Buttons
2. The Magnification Tool: Drag a rectangle over the region that you want to zoom to.
3. Zoom in/out with a scro11 whee1 or by doub1e c1icking on a region.

Now that that is done, we should only be able to see **Seabird Carcass** surveys. Each color corresponds to a survey site.

[Screenshot of seabird carcass in mapper]

Let change the default **measurement** to display the **Counts** instead of **Carcasses per effort per km**. Click on the 
**Measurement** drop down menu in the Legend and select **Counts**.

[Screenshot of dropdown menu]

Now hover the mouse over a site and see what happens.

[screenshot of mouse hover]

This is a sum off all of the most common Seabird Carcasses that has been found at this beach, as well as some metadata about the beach. 
We can also click on a site to see the time series of that site. Try it outl! -->

## Filtering Data 
The portal has multiple ways to filter data: by time, by taxonomy, by collection group and more. 

In the Legend box select plus sign on the **Species (common name)** drop-down menus. This will give a list of the common 
names of different birds that were identified.

[Screenshot filter selector]

For more information about filtering by taxonomy and organization see [Appendix: Advanced Filtering](https://www.cencoos.org/images/tutorials/COMBERS_portal_tutorial_V2.html#filter_layer).

## Keyword Filtering 
There are some other really cool filtering feature, try selecting a Species using the common name. 

You can also use keywords to filter the data, try searching for “gull."

[Screenshot of filter by keyword]

Now when you hover over a site you can see that multiple species of gulls are included in the filter.

[Screenshot of hover over]

**Polygon Selection**

Select the polygon icon on the right-hand side of the page.

[Screenshot highlighting polygon]

Now use that tool to draw a polygon around Monterey Bay. When you are done, double click on the polygon and this will 
extract a time series of all of the selected data.

[Screenshot of selecting a polygon]

Now let’s look at some specific mortality events and then include some environmental data from satellites. 

Using what the tools we just showed:
* Filter the data to just select common Murre
* Use the polygon selection tool to select the beaches around Monterey Bay 
* Select the Carcasses Per Km Measurement

The results should be a time series plot that looks similar to this:

[Screenshot of histogram plot]

Let’s expand this plot by clicking on the <span style="color:red;">Enlarge</span> icon (see the red box above)

Now we can change how the data are binned through time. By default this dataset is binned into annual values, but we can 
also display the data for each month (the raw values) or by the season. 

Click on the **Time Bin** pull down and select **Months**.

[Screenshot of timebin highlighting some pieces]

Adding 

From this plot a couple of things stand out:
1. There is a seasonal signal to Seabird Deposition - Fall and Summer tend to have higher deposition than Winter and Spring
2. There are three unusual events that stand out
   1. 1997: El Nino year, HASS, and Gill Net mortalities
   2. 2007: Starvation event
   3. 2015: The Blob: Marine Heatwave

## Adding/Comparing Sea Surface Temperature
Let's add the SST layer as measured from Satellites.

This can be found by searching the **Data Catalog** as shown earlier, but the data catalog can be easily accessed by 
selecting the **Find Data** next to the **Legend** in the Map Layer.

Now let’s search for "SST Monthly" and add the AVHRR West Coast SST, 1 MONTH Composite layer by selecting the blue cross 
next to the name.

[GIF of searching in map]

[GIF adding data and making histogram]

Now let’s create a **time series of SST in the middle of Monterey Bay**. This is done by creating a virtual sensor, a 
tool that extracts a time series at a single point out of a spatial dataset. This make take a second to load. 
[Link](https://data.cencoos.org/?ls=2f9faf8d-f7f4-0666-16d3-e0d41b079384#map)

[GIF adding SST to map]

Once it’s loaded, try to see if you can expand the plot of change around temporal binning.

[Screenshot of timeseries]

_Tip: The portal has a ton of features and data. Feel free to poke around and try to break things!_

### TOPIC: Comparing Data with Data Views

Now we can create a **Data View** to view multiple types of data on the same page. The first data view will compare two beaches.
1. Use the polygon to select the Common Murres in Monterey Bay
2. With the time series open for the beach, Select the counts per effort per km
3. Create a new Data View by selecting the Blue Star button. Then select the Plus sign to create a new data view. Give it a name.
   Then a check the two boxes to **Save to data view** and **Add to compare chart**

[GIF creating new view]

[GIF looking at charts]

Now add SST time series to the **Monterey Beaches** Data view you just learned how to create from the middle of Monterey Bay.

Finally, let’s look at the Data View! This is done by selecting the **Data View** button near the top of the portal and 
selecting the data view you just created from the drop down menu.

### TOPIC: Comparing Data with Data Views
Now we can create a **Data View** to view multiple types of data on the same page. The first data view will compare two beaches.
1. Use the polygon to select the Common Murres in Monterey Bay
2. With the time series open for the beach, Select the counts per effort per km
3. Create a new Data View by selecting the **Blue Star** button. Then select the Plus sign to create a new data view. Give it a name.
   Then a check the two boxes to **Save to data view** and **Add to compare chart**

[GIF save data to data view and add to compare chart]

1. Now add SST time series to the `Monterey Beaches` Data view you just learned how to create from the middle of Monterey Bay.
2. Finally, lets look at the Data View! This is done by selecting the **Data View** button near the top of the portal and 
selecting the the data view you just created from the drop down menu.

[Screenshot of data views dropdown on map]

[Link](https://data.cencoos.org/?ls=d5c72fe4-1f12-115f-6ede-fcfc17807d63#data/5)

## The Data View

[Screenshot of data view]

There is a lot of information here, but what stands out (to me at least) is that the increases in mortality are seen at both beaches in 2009 and again in 2015.

**Now let’s add some SST data**

Now the mortality following the Blob really stands out, as well as the seasonality of carcass deposition.

[Screenshot of timeseries, highlighting blob]

Here we can see just how warm the winter months of in 2014. We can also visualize SST as an anomaly or climatology (these are really pseudo-climatologies)

[GIF of SST timeseries - changing anomoly/climatology]

## Finally: The Feedback Button
If you are having any trouble, something doesn't look right, or really anything else. Please use the feedback button in 
the top right of the portal. This button will send us a link to what you are looking at and help us figure out what is 
going on. It's also a great way for us to log suggestions, so if there is something you would like to see, we want to 
hear it!

[Screenshot of Feedback button]

## Appendix: Using the Real-time Sensor Layer
The colors that you see on the map correspond to a different parameter being measured at a given location. By default we 
are seeing **Air Temperature** and the color corresponds to the most recent value (gray if no values have reported in 24 hours.
Hovering over a circle will give us more information about the data stream and show some recent data.

[Screenshot of picking a point from map]
 
## Appendix: Advanced Filtering
The portal has multiple ways to filter data: by time, by taxonomy, by collection group and more.
In the Legend box select plus sign on the **Advanced Icon**. This will expand the filtering options.

[Screenshot of bird carcass advanced options]

Now let’s select **BeachCOMBERS** from the **Organization Drop down Menu**.

[Screenshot of organization dropdown]

Now if you zoom out on the map you will notice that it is only showing data collected by BeachCOMBERS.


