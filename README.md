# A Tale of Four Neighborhoods data and documentation

Jack Rechsteiner, [jjr156@pitt.edu](mailto:jjr156@pitt.edu); last updated July 25, 2025

------------------------------------------------------------------------

## Repo Summary

[A Tale of Four Neighborhoods](https://arcg.is/4iSbG) is a University of Pittsburgh Digital Scholarship and Publishing project completed as part of the 2025 Digital Scholarship Summer Graduate Internship.
This repository contains the data and code that were used in A Tale of Four Neighborhoods, along with documentation detailing the processes and decisions that occurred in creating the project.

This `README.md` is separated into two main sections:
- [Data Sources](#data-sources)
- [Data Processing](#data-processing)

## Data Sources

A Tale of Four Neighborhoods contains three types of data: [map data](#map-data), [census data](#census-data), and [news article data](#news-article-data)

### Map Data

The historic map used in this project is the [2005 US Geological Survey High Resolution Orthoimage for Pittsburgh, PA](https://www.pasda.psu.edu/uci/DataSummary.aspx?dataset=602) from [the Pennsylvania Spatial Data Access (PASDA) portal](https://www.pasda.psu.edu/).
PASDA provides official Pennsylvania geospatial data that provides open access to the public.
According to PASDA, this map "consists of 0.3-meter pixel resolution (approximately 1-foot), natural color orthoimages covering the Pittsburgh, PA Urban Area (Allegheny and Beaver Counties)".
This map was chosen because the year of the map falls within the 2000 to 2005 time range examined in this project and because "Orthoimagery combines the image characteristics of a photograph with the geometric qualities of a map".

The contemporary map used in this project is the [World Imagery map](https://www.arcgis.com/home/item.html?id=10df2279f9684e4a9f6a7f08febac2a9) from [ArcGIS Online](maps.arcgis.com).
The World Imagery map is licensed under the [Esri Master License Agreement](https://www.esri.com/en-us/legal/terms/master-agreement?rsource=https%3A%2F%2Fwww.esri.com%2Flegal%2Fsoftware-license) and is available for use with ArcGIS applications.
According to ArcGIS, the World Imagery map features "a high-resolution, high-quality image layer over defined metropolitan" and "high-resolution aerial photography contributed by the GIS User Community".
This map was chosen because of its compatibility with ArcGIS StoryMaps and its resolution is of similar quality to the 2005 US Geological Survey High Resolution Orthoimage for Pittsburgh, PA.

### Census Data

All census data in this project was sourced from the U.S. Census Bureau data available on [Social Explorer](https://www.socialexplorer.com/).
The data for the year 2000 came from the [Census 2000 on 2010 Geographies survey](https://www.socialexplorer.com/data/RC2000) to ensure that the 2000 census tracts are equivalent to the 2023 census tracts.
The data for the year 2023 came from the [ACS 2023 (5-Year Estimates) survey](https://www.socialexplorer.com/data/ACS2023_5yr) because it was the most recent Census Bureau survey available with data at the census tract-level.
Monetary values were adjusted to 2020 inflation dollars to make the results easily comparable to the Census 2020 data when it becomes available.

The following data tables were used for this project:
- Total Population
- Age (Short Version) 
- Race
- Hispanic or Latino by Race 
- Educational Attainment for Population 25 Years and Over 
- Median Household Income 
- Tenure
- Occupancy Status

An attempt was also made to include information about the prior living location of participants.
However, it was decided to exclude this information from the project as the 2000 Census compared residents by their living location 5 years prior to the survey and the 2023 ACS compared residents by their living location 1 year prior to the survey.
This was determined to be too much of a time frame difference to be truly comparable.

### News Article Data

The [news articles from 2000 to 2005](2000_2005_OCR/) came from the [Documenting Pitt collection](https://documenting.pitt.edu/) that is part of the [University of Pittsburgh ULS Digital Collections](https://digital.library.pitt.edu/).
A search was conducted to find all archived articles from [Pitt News](https://documenting.pitt.edu/collection/pitt-news) and [University Times](https://documenting.pitt.edu/collection/university-times/) that contained mentions of the 4 neighborhoods examined in this project.
The `.OCR` files for the articles are not publicly available but were available by request from the University Library System.
The `.OCR` files were then converted to `.txt` files to be more easily processed in R.
The Pitt News and University Times articles are in copyright but are free to use in any way that is permitted by the copyright.

The [news articles from 2020 to 2025](2020_2025_Articles/) came from the [Pitt News website](https://pittnews.com/) and the [University Times website](https://www.utimes.pitt.edu/).
A search was conducted to find all articles that contained mentions of the 4 neighborhoods examined in this project.
Articles were downloaded from their respective sites as `.pdf` files.

## Data Processing

All data used in this project was modified or added to in some way before being incorporated into the project website.
These modifications and additions are detailed in the sections below.

### Map Layers

The [base maps](#map-data) used in this project have not been modified.
Additional layers have been overlaid on the maps to highlight the borders and areas of the neighborhoods examined in this project.
These layers were drawn in Google Earth Pro based on census tract maps to be consistent with the areas represented in the census data.
After creating these layers in Google Earth Pro, they were then imported into ArcGIS Online to be used with base maps.

### Census Categories

The census data values reported in the charts are unchanged from their values in Social Explorer with the exception of two calculated categories that contain combined values to enhance the readability of the charts.

The first category is the "Other* Race" category.
The decision to collapse values into this category was made so that populations would not be excluded from the charts while still allowing the charts to be easily displayed on the page.
The "Other* Race" category combines the following race categories from the census data:
- Asian
- American Indian and Alaska Native
- Hispanic or Latino
- Native Hawaiian and Pacific Islander
- Some Other Race

The second category is the "Graduate Degree" category.
The decision to collapse values into this category was made to make it easier to view differences in populations that attained education beyond a 4-year college degree.
The "Graduate Degree" category combines the following education categories from the census data:
- Master Degree
- Professional Degree
- PhD

### News Text Analysis

The [news articles](#news-article-data) used in this project were read into R to create a text corpus.
This corpus was then used to categorize articles by their time frame of publication, the neighborhood mentioned in the article, and the main theme associated with the neighborhood in the article.
It is important to note that the themes are not meant to capture the entirety of the articles but are meant to capture the reason that a neighborhood was mentioned in an article.
For example, the article ["Upperclassmen offer advice to incoming first-years"](https://pittnews.com/article/181711/news/upperclassmen-offer-advice-to-incoming-first-years/) was categorized under the "retail" theme because Lawrenceville was mentioned as having "beautiful restaurants and a ton of ice cream joints".

The full script that was used to clean and categorize the news articles can be found in [text_mining.Rmd](text_mining.Rmd).
The output of the data processing can also be viewed in the [full_article_df.csv](full_article_df.csv) and [full_article_df.rds](full_article_df.rds).

After processing the news article corpus, the [full_article_df.rds](full_article_df.rds) file was used to calculate the values presented in the news article charts seen on the project website.
The script that was used for this analysis can be found in [text_analysis.Rmd](text_analysis.Rmd).
