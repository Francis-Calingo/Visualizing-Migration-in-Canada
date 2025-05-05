# Data Visualization of Migration to Canada (with Python)

# Table of Contents
* [Project Background](#project-background)
* [Data Structure and Initial Checks](#data-structure-and-initial-checks)
* [Executive Summary](#executive-summary)
* [Insights Deep Dive](#insights-deep-dive)
* [Recommendations](#recommendations)
* [Assumptions and Caveats](#assumptions-and-caveats)
* [Credits and Acknowlegements](#credits-and-acknowledgements)


---

# Project Background
Statistics Canada, founded in 1971, serves as Canada’s national statistical agency, and the wide array of data that it collects, whether through the census data collected every demi-decade, or through quarterly population estimates, is absolutely valuable for the Canadian government and subnational governments to enact data-driven policy. In particular, the astronomical increase in the number of people who have landed in Canada over the past few years (whether as permanent residents, non-permanent residents, or a special category such as refugees) means that governments and institutions must respond to the opportunities and challenges that come along with this phenomenon. The characteristics of migration into Canada is far from monolithic, which is why this project was completed, in order to help inform policy and respond to the cosmopolitan nature of migrants as a whole as well as their different settlement patterns using data gathered from Statistics Canada.

Insights and recommendations are provided on the following key areas:

- **Time-Series Analysis:** Migration trends over time will help understand what kind of effects (if any at all) the implementation of certain policies and current events have had on migration.
- **Scatter Plot Analysis:** Settlement patterns of different demographic and socioeconomic classes of people (e.g., gender) to ascertain what kind of specialized services would need to be ameliorated in order to better integrate certain groups of migrants.
- **Scatter Plot Analysis:** Find any associations between different pairings of variables within each of the largest Census Metropolitan Areas (CMAs).
- **Geospatial Analysis:** Analyze the settlement patterns of recently landed non-permanent residents by province/territory to inform provincial and territorial governments.

This Jupyter notebook hosts the project itself. [Link to Download](Visualizing_Migration_Patterns_in_Canada.ipynb)
  <ul>
    <li><b>IDEs Used:</b> Google Colab, Jupyter Notebook</li>
    <li><b>Python Version:</b> 3.10.12</li>
    <li><b>Libraries and Packages:</b>
    <ul>
      <li><b>Geospatial Analysis Libraries: </b> geopandas, matplotlib.plt </li>
      <li><b>Libraries for plotting data: </b> pandas, seaborn, plotly.express, numpy</li>
      <li><b>Libraries to load files:</b> files (from google.colab), zipfile, io</li>
    </ul></li>
  </ul>

The data structure of the 9 Excel files used for this analysis will be outlined in the next section. Data sources: 
* <a href="https://www12.statcan.gc.ca/census-recensement/2021/dp-pd/prof/details/page.cfm?LANG=E&GENDERlist=1,2,3&STATISTIClist=1,4&DGUIDlist=2021A000011124&HEADERlist=26&SearchText=canada">Census Profile, 2021 Census of Population: Selected places of birth for the recent immigrant population</a>
* <a href="https://www12.statcan.gc.ca/census-recensement/2016/dp-pd/prof/details/page.cfm?Lang=E&Geo1=PR&Code1=01&Geo2=PR&Code2=01&SearchText=Canada&SearchType=Begins&SearchPR=01&B1=Immigration%20and%20citizenship&TABID=1&type=0">Census Profile, 2016 Census: Recent immigrants by selected places of birth</a>
* <a href="https://www12.statcan.gc.ca/nhs-enm/2011/dp-pd/dt-td/Rp-eng.cfm?TABID=2&LANG=E&APATH=3&DETAIL=0&DIM=0&FL=A&FREE=0&GC=0&GK=0&GRP=1&PID=105411&PRID=0&PTYPE=105277&S=0&SHOWALL=0&SUB=0&Temporal=2013&THEME=95&VID=0&VNAMEE=&VNAMEF=">2011 National Household Survey: Data tables: Place of Birth, Period of immigration=2006-2011</a>
* <a href="https://www12.statcan.gc.ca/census-recensement/2006/dp-pd/hlt/97-557/T404-eng.cfm?Lang=E&T=404&GH=4&GF=1&SC=1&S=1&O=D#FN2">Place of birth for the immigrant population by period of immigration, 2006 counts and percentage distribution, for Canada, provinces and territories - 20% sample data</a>
* <a href="https://www12.statcan.gc.ca/english/census01/products/standard/themes/Rp-eng.cfm?LANG=E&APATH=3&DETAIL=1&DIM=0&FL=A&FREE=0&GC=0&GID=0&GK=0&GRP=1&PID=62124&PRID=0&PTYPE=55430,53293,55440,55496,71090&S=0&SHOWALL=0&SUB=0&Temporal=2001&THEME=43&VID=0&VNAMEE=&VNAMEF=">2001 Census Topic-based tabulations</a>
* <a href="https://www150.statcan.gc.ca/t1/tbl1/en/tv.action?pid=1710002301&cubeTimeFrame.startMonth=01&cubeTimeFrame.startYear=2001&cubeTimeFrame.endMonth=10&cubeTimeFrame.endYear=2018&referencePeriods=20010101%2C20181001">Archived - Estimates of non-permanent residents, quarterly, inactive, 2001-2018</a>
* <a href="https://www150.statcan.gc.ca/t1/tbl1/en/tv.action?pid=1710004001&pickMembers%5B0%5D=1.1&cubeTimeFrame.startMonth=01&cubeTimeFrame.startYear=2018&cubeTimeFrame.endMonth=10&cubeTimeFrame.endYear=2022&referencePeriods=20180101%2C20221001">Estimates of the components of international migration, quarterly, 2021-2024</a>
* <a href="https://www150.statcan.gc.ca/t1/tbl1/en/tv.action?pid=1710012101&pickMembers%5B0%5D=1.1&cubeTimeFrame.startMonth=01&cubeTimeFrame.startYear=2021&cubeTimeFrame.endMonth=07&cubeTimeFrame.endYear=2024&referencePeriods=20210101%2C20240701">Estimates of the number of non-permanent residents by type, quarterly</a> 
* <a href="https://www12.statcan.gc.ca/census-recensement/2021/geo/sip-pis/boundary-limites/index2021-eng.cfm?year=21">2021 Census – Boundary files</a>
* [2020 Annual Report to Parliament on Immigration](https://www.canada.ca/en/immigration-refugees-citizenship/corporate/publications-manuals/annual-report-parliament-immigration-2020.html)

For the report version of the analysis: [Link to Download](https://github.com/Francis-Calingo/Visualizing-Migration-in-Canada/raw/main/Patterns%20within%20Patterns_%20Using%20Python%20and%20Excel%20to%20Unlocking%20Hidden%20Migration%20and%20Settlement%20Patterns%20in%20Canada.pdf)

For the walkthrough of the project in video form: [Video](https://drive.google.com/file/d/14W0qtsOJdgzcSmXcvERx3pGHeB3109VV/view)

To  fork this repository:
```bash
git clone https://github.com/Francis-Calingo/Visualizing-Migration-in-Canada.git
cd Visualizing-Migration-in-Canada
```

[<b>Back to Table of Contents</b>](#table-of-contents)

---

# Data Structure and Initial Checks


| Data Content  | Number of Entries (Records x Field) | Number of Records  | Number of Fields | Download File Link |
| ------------- | ------------- | ------------- | ------------- | ------------- |
| Non-Permanent migration by provinces & territory  | **1425**  | 95  | 15  | [Download](https://github.com/Francis-Calingo/Visualizing-Migration-in-Canada/raw/main/Non-Permanent%20Migration.csv)  |
| Quarterly international migration by province & territory  | **1425**  | 95  | 15  | [Download](https://github.com/Francis-Calingo/Visualizing-Migration-in-Canada/raw/refs/heads/main/Estimates%20of%20the%20components%20of%20international%20migration%2C%20quarterly.csv) |
| Census-by-census immigration data from Top 10 Countries of Origin in 2020  | **150**  | 50  | 10 | [Download](https://github.com/Francis-Calingo/Visualizing-Migration-in-Canada/raw/refs/heads/main/Migration%20Timeline%20of%20Top%2010%20Countries%20from%202020.csv) |
| % of Recent Migrants that identify as woman by country of origin and province & territory  | **2365**  | 55  | 43  | [Download](https://github.com/Francis-Calingo/Visualizing-Migration-in-Canada/raw/refs/heads/main/Migration%20Gender%20Breakdown.csv) |
| Each province & territory's top 5 countries of origin, recent immigrants  | **248**  | 62  | 4  | [Download](https://github.com/Francis-Calingo/Visualizing-Migration-in-Canada/raw/refs/heads/main/Top%205%20by%20Province%20%26%20Territory.csv)  |
| Age breakdown of immigrant population vs. general population, by province & territory  | **840**  | 140  | 6  | [Download](https://github.com/Francis-Calingo/Visualizing-Migration-in-Canada/raw/refs/heads/main/Migration%20Age%20Analysis.csv) |
| Recent immigrants by census metropolitan areas (CMA) | **338**  | 26  | 13  | [Download](https://github.com/Francis-Calingo/Visualizing-Migration-in-Canada/raw/refs/heads/main/Recent%20Immigrants%20CMA.csv)  |
| Total non-permanent residents by census metropolitan areas  | **130**  | 26  | 5  | [Download](https://github.com/Francis-Calingo/Visualizing-Migration-in-Canada/raw/refs/heads/main/Non-Permanent%20Residents%20CMA.csv)  |
| % Growth rate of CMAs and immigrant population in each CMA | **182**  | 26  | 7  | [Download](https://github.com/Francis-Calingo/Visualizing-Migration-in-Canada/raw/refs/heads/main/CMA%20vs.%20Immigrant%20Growth%20Rate.csv)  |
| **TOTAL** | **7,103**  | 575  | 118  | N/A  |

<details><summary><b>Feature Engineering</b></summary>  
<ul>
    <li><b>Non-Permanent residents:</b> Quarterly data for total non-permanent residents missing between 2018-2021. Quarterly data for net non-permanent migration used to calculate missing values.</li>
    <li><b>2021 Census Gender analysis:</b> For each country of origin, find the total number of respondents that identify as women, divide by the raw total for that country of origin, then multiply by 100 to get the percentage. The same method applies for the general population. </li>
    <li><b>Top 5 countries of origin by province and territory, recent immigrants (2021 census):</b> After determining each province and territory's top 5 countries of origin, take their raw total, by total province or territory's total recent immigrant population, then multiply by 100 to get their percentages.</li>
    <li><b>Age breakdown, nationally and by province and territory (2021 Census):</b> Find the age breakdown of the recent immigrant population (using the intervals [0,5), [5,15), [15,25), [25,45), 45 and above), and calculate their percentages. The age breakdown for the general population is more granular, necessitating arithmetic operations to match with the aforementioned intervals, then the same process can be executed. </li>
    <li><b>Non-permanent residents per-capita by CMA:</b> [NPR Population, 2021]/[CMA Population, 2021], then divided by 100,000.</li>
    <li><b>Growth rates of CMA:</b> [[CMA Population, 2021 Census] - [CMA Population, 2016 Census]]/[CMA Population, 2016 Census], then multiplied by 100</li>
    <li><b>Growth rates of CMA Non-Permanent Resident populations:</b> [[CMA NPR Population, 2021 Census] - [CMA NPR Population, 2016 Census]]/[CMA NPR Population, 2016 Census], then multiplied by 100 </li>
    <li><b>Per-capita population, recent immigrants, by continent of origin (CMAs, 2021):</b> For each continent of origin, take the total, divide by the CMA population, then divide by 100,000.</li>
    <li><b>Growth rate of Non-Permanent Residents, Q3 2022-Q3 2024:</b> [[NPR Population, Q3 2024] - [NPR Population, Q3 2022]]/[NPR Population, Q3 2022], then multiplied by 100</li>

</ul>
</details>

For the diagram that helps map the workflow of migrating data from Statistics Canada's select datasets to csv files:

<img src="https://github.com/Francis-Calingo/Visualizing-Migration-in-Canada/blob/main/Figures/Figure1.1.jpg"/>

The shapefile has **104 entries (8 fields x 13 records)**. 

It is important to note that the shapefile was extracted from a zip file that was downloaded from the Boundary files webpage of Statistics Canada. There are no associated CSVs, so in order to ascertain the fields, the shapefile needed to be exported as a CSV file via QGIS.
As you can see, most of the fields are irrelevant in isolation besides FEDENAME, which houses the English names of the ridings *in order* . The csv itself is not needed, the shapefile is. [But it is in this repo for reference](https://github.com/Francis-Calingo/Visualizing-Migration-in-Canada/blob/main/Shapefile_Features.csv) to better understand the structure of the shapefile as well as the workflow of merging it with the main CSV file to create choropleth maps in Python [Figure 1.2].

<img src="https://github.com/Francis-Calingo/Visualizing-Migration-in-Canada/blob/main/Figures/Figure1.2.jpg"/>

[<b>Back to Table of Contents</b>](#table-of-contents)

---

# Executive Summary

### Overview of Findings

* Migration patterns as a whole was characterized by a rapid increase over the past several years, particulalrly with regards to non-permanent residents and people landing from India and Syria (although seasonality is a consistent pattern).

* Settlement patterns by province/territory were characterized by some variations of gender ratios for each migrant community, consistency in the top sources of migrants (albeit with some notable exceptions, including the dominance of francophone countries in settlement patterns in Québéc), and a working age plurality (i.e., aged 25-44 years).

* For the most part, settlement patterns across CMAs are characterized by within-group homogeneity and between-group heterogeneity (i.e., CMAs within the sam region tend to exhibit similar settlement patterns), although all CMAs share the phenomenon that their foreign-born population is growing at a faster rate than their general population.

* Over the past few years, Nunavut and Alberta experienced the highest non-permanent resident growth rate, while the Atlantic region was surprisingly low in comparison.

[<b>Back to Table of Contents</b>](#table-of-contents)

---

# Insights Deep Dive
### Time-Series Analysis:

* **Observe the dip in NPRs during the first three waves of COVID-19, as well as the accelerated growth after 2022.** This reflects the travel restrictions during the height of the spread of COVID-19, as well as domestic labour shortages following the end of said restrictions.
  
* **Seasonality is observed with quarterly immigration data.** Policy changes (e.g., changes to immigration policies following the lifting of all federal COVID-19 regulations in 2022), as well as major historical events (e.g., COVID-19) had visible effects on migration in recent years, but other than that, the patterns in immigration remain largely seasonal, with migration tending to peak in the third quarter of the calendar year and bottoming in the first quarter of the year.

<img src="https://github.com/Francis-Calingo/Visualizing-Migration-in-Canada/blob/main/Figures/Figure3.1.jpg"/>
  
* **The top three sources of immigrants for Canada remain unchanged over the past two decades, while some countries have become a bigger source of migration to Canada over the past decade.** In no particular order, China, India, and the Philippines remain the top three sources of immigration to Canada, with each country taking turns as being the top source. Other countries such as Syria and Nigeria have seen an increase over the past decade, with Syria's increase in particular having been fuelled by the recently concluded Syrian Civil War as well as drastic changes in refugee policies stemming from a change in government in 2015.

<img src="https://github.com/Francis-Calingo/Visualizing-Migration-in-Canada/blob/main/Figures/Figure3.2.jpg"/>

<img src="https://github.com/Francis-Calingo/Visualizing-Migration-in-Canada/blob/main/Figures/Figure3.3.jpg"/>

---

### Categorical Data Analysis:

* **While, for the most part, the gender ration for most migrant communities nearly mirror the national average, there are some variations by country, on one extreme is Japan with a disporportionately high proportion of women compared to the national average, and on the other extreme is the Republic of Ireland.** If we look at the different provinces and territories, some countries of origin display consistent behaviour like Japan, and for others like Algeria (in Alberta), we’ll observe that there is a much bigger difference.

<img src="https://github.com/Francis-Calingo/Visualizing-Migration-in-Canada/blob/main/Figures/Figure3.4.jpg"/>

<img src="https://github.com/Francis-Calingo/Visualizing-Migration-in-Canada/blob/main/Figures/Figure3.5.jpg"/>
  
* **Some countries such as China remain a top source of immigrants for each province and territory, while a few interesting exceptions abound, such as the dominance of francophone countries as the top sources of immigrants for Québéc, and the appearance of the United States and the United Kingdom as a top source of immigration for British Columbia.** Variations also exist within each country of origin as well. For example, recent immigrants from the Philippines take up a significant portion of the recent migrant population in places such as Newfoundland and Labrador and NWT, while they are not even a top source of recent migration for Québéc.

<img src="https://github.com/Francis-Calingo/Visualizing-Migration-in-Canada/blob/main/Figures/Figure3.6.jpg"/>

<img src="https://github.com/Francis-Calingo/Visualizing-Migration-in-Canada/blob/main/Figures/Figure3.7.jpg"/>
  
* **It appears that the characteristic of the foreign-born population is more oriented towards working-age adults (where people aged 25-44 years make up the plurality) than the general population (where people older than 45 years make up the plurality).** Even in Nunavut, where the age structure is significantly younger compared to the rest of the country, the pattern still holds.

<img src="https://github.com/Francis-Calingo/Visualizing-Migration-in-Canada/blob/main/Figures/Figure3.8.jpg"/>

<img src="https://github.com/Francis-Calingo/Visualizing-Migration-in-Canada/blob/main/Figures/Figure3.9.jpg"/>

### Scatter Plot Analysis:

* **Outside of Montréal, Québéc has quite a low per-capita non-permanent resident population.** For other regions, the results are a mixed bag and we therefore cannot immediately surface any discernible patterns.

<img src="https://github.com/Francis-Calingo/Visualizing-Migration-in-Canada/blob/main/Figures/Figure3.10.jpg"/>
  
* **Virtually every CMA’s foreign-born population is outpacing their general population’s growth rate, with a bit of regional variation.** BC exhibited the highest general population growth rate, but the Atlantic exhibited the highest foreign-born population growth rate, possibly due to both the federal and provincial governments’ push to attract more immigrants to the Atlantic region in a bid to offset population loss and inter-provincial out migration.

<img src="https://github.com/Francis-Calingo/Visualizing-Migration-in-Canada/blob/main/Figures/Figure3.11.jpg"/>
  
* **For the most part, there were no interesting nor discernible patterns for the rate of migration for people from the Americas, Europe, and Oceania. It appears that migrants of African origin, on a per-capita basis, is comparatively high compared to other CMAs, while it is comparatively lower with migrants of Asian origin.** And to some extent it rings true for the rest of Québéc.

<img src="https://github.com/Francis-Calingo/Visualizing-Migration-in-Canada/blob/main/Figures/Figure3.12.jpg"/>

<img src="https://github.com/Francis-Calingo/Visualizing-Migration-in-Canada/blob/main/Figures/Figure3.13.jpg"/>

* **The points representing the Prairie CMAs appear to be clustered in a similar area for both Africa and Asia plots.** This insight suggests that they share a similar migration and settlement pattern.

<img src="https://github.com/Francis-Calingo/Visualizing-Migration-in-Canada/blob/main/Figures/Figure3.14.jpg"/>


### Spatial Analysis:

* **Nunavut by far experienced the fastest non-permanent resident growth from Q3 2022 to Q3 2024.** Although, that could largely be attributed to its small non-permanent resident, but could also signal a shift in government priorities in terms of migration and settlement.
  
* **Alberta also experienced high growth.** This is reflective of the province's generally high growth rate in the past few years, both from international migration and inter-provincial migration.
  
* **Growth has slowed down for British Columbia and Ontario.** This is reflective of the fact that both provinces lead the country in migration in general, and already had an established foreign-born community (permanent and non-permanent).
  
* **The Maritime provinces experience relatively little growth.** This is in spite of the increasing popularity of the Maritimes for permanent and non-permanent migration.

<img src="https://github.com/Francis-Calingo/Visualizing-Migration-in-Canada/blob/main/Figures/Figure3.15.jpg"/>

[<b>Back to Table of Contents</b>](#table-of-contents)

---

# Recommendations:

By making this kind of data more granular and adding a spatial and geographic component, policy decisions both within and outside Canada can be remodelled to better cater to communities with different needs and socioeconomic conditions. Based on the insights and findings above, we would recommend all levels of government and civic organizations to consider the following: 

* There is seasonality observed with migration. **Organizations who are helping migrants integrate in Canadian society should keep this mind so that they can plan their yearly agendas accordingly and accomodate for higher volumes in certain months.**

* China, India, and the Philippines remain the top sources of immigration for Canada, while countries such as Nigeria and Syria have seen an increase over the past few years. **All levels of governments must ensure that, with the high (or increasing) volumes coming from specific countries, they combat any potenial misinformation campaigns targeting those communities, as higher volumes of arrivals coming from certain countries may tend to garner more media attention, and, therefore, increase the likelihood of discriminatory sentiment specific to those communities.**
  
* While the gender ratio for recent migrant communities is, for the most part, on par with the Canadian or provincial/territorial averages, there remains anomalies, both at the national and subnational level. **Therefore, more women-specific migrant resources for certain migrant communities such as the Algerian diaspora in Alberta and the Japanese community at the national level should be made available.**
  
* Québéc's settlement patterns stand out in comparison with the other provinces, and territories, as, unlike the other provinces, India and the Philippines were not one of Québéc's Top 5 sources of recent immigration, while francophone countries made up 4 of the top 5. **Québéc’s unique migration patterns should be examined further, research on the different ways its language laws have an effect on migration should be conducted, and supports for migrant communities who are more anglophone should be executed.**

* The age structure for the foreign-born population appears to be defined by the plurality of working-age adults (25-44 years) while the age structure for the Canadian-born population is skewed more towards 45 years+. **While it is clear that this is tied to government efforts to utilize immigration to avoid the worst effects of the aging population as seen in countries such as Japan, it must be prepared to adjust accordingly as the foreign-born population slowly becomes part of the aging population in the next few decades.**

* Outside of Montreal, Québéc has quite a low per-capita non-permanent resident population, while the results for other provinces and territories show a mixed bag. **As a previous plot has shown a drastic increase of the non-permanent resident population in the last few years at the national level, Québéc will start to slowly experience that growth as well, and its ministry responsible for immigration will need to have its budget increased accordingly so that its largely homogenous communities outside of the Greater Montréal area can effectively integrate incoming non-permanent residents.**

* Virtually every CMA’s foreign-born population is outpacing their general population’s growth rate, with a bit of regional variation. BC exhibited the highest general population growth rate, but the Atlantic exhibited the highest foreign-born population growth rate. **Similarly with Québéc, the Atlantic provinces' respective immigration ministries will need to have their budgets increased (or such ministries would need to be established if not already established).**

* In Montréal, it appears that migrants of African origin, on a per-capita basis, is comparatively high compared to other CMAs, while it is comparatively lower with migrants of Asian origin. And to some extent it rings true for the rest of Québéc. The cluster of red points from the third scatter plot represent Prairie CMAs, suggesting that they share a similar migration pattern. **These settlement patterns mean that Québéc municipalities should consider funding (or increase funding for) culturally-approporiate integration programs for their African communities, while Parairie municipalities should increase cross-provincial and cross-municipal coopertion in terms of integrating newcomers.**
  
* Nunavut by far experienced the fastest non-permanent resident growth within that time period, although that can largely be attributed to its small non-permanent resident. Alberta also experienced high growth, mirroring its generally high growth as a whole over the past decade. Growth has slowed down for British Columbia and Ontario. Surprisingly, the Maritime provinces experience relatively little growth despite government initiatives to attract immigrants and foreign labour into that region. **Regardless, given the high growth rate of the non-permanent resident population over the past few years across the country, and the vast size of Canada geographically, consulates should consider redirecting more of their resources towards underserved communities, especially communities with high levels of non-permanent migration such as Nunavut.**

[<b>Back to Table of Contents</b>](#table-of-contents)

---

# Assumptions and Caveats:

Throughout the analysis, multiple assumptions were made to manage challenges with the data. These assumptions and caveats are noted below:

* Since it was hypothesized that Ontario and Quebec would experience different migration and settlement patterns, the Ottawa-Gatineau CMA was split into its Ontario and Quebec parts. Therefore, the scatter plot analysis contained 26 points for each plot.
  
* Data only goes up to the third quarter of 2024 (i.e., September 30). Recent changes to immigration policies by the federal government have either not gone to fruition yet or have only been recently implemented. The analysis will therefore not account for the anticipated drop in immigration in the coming months.
  
* Some of the datasets are estimates based on a 25% sample size and not the full count, which may slightly render parts of the data not fully accurate, but the agency’s methodology balances accuracy and operational costs effectively.

* Even though Plotly was heavily used (which ended up being useful for filtering for certain results such as the time-series visualization of Syrian migration to Canada in the past two decades), the project is mostly static in nature and does not fully utilize the interactive capabilities of Plotly. There is an opportunity to scale up this project and productionize it into publically-available interactive graphs and dashboards that can be hosted in websites such as think-tanks, government websites, and civic organizations that cover migration topics).

* Statistics Canada's definition of "recent immigrants" is those that migrated to Canada within the last 5 years of a census year (e.g., 2016-2021, 2011-2016, 2006-2011, etc.). Since the most recent census was taken back in 2021, for the purposes of this analysis, "recent immigrants" will refer to those that immigrated to Canada between 2016-2021.

[<b>Back to Table of Contents</b>](#table-of-contents)

---

# Credits and Acknowledgements

"Bar Charts in Python". Plotly, https://plotly.com/python/bar-charts/

"Filled Area Plots in Python". Plotly, https://plotly.com/python/filled-area-plots/

"Horizontal and Vertical Lines and Rectangles in Python". Plotly, https://plotly.com/python/horizontal-vertical-shapes/

"Mapping and Plotting Tools". — GeoPandas, https://geopandas.org/en/stable/docs/user_guide/mapping.html.

N. Frerebeau. "Paul Tol’s Color Schemes", R-Packages, 25 February 2025. https://cran.r-project.org/web/packages/khroma/vignettes/tol.html.

"seaborn.FacetGrid". Seaborn. https://seaborn.pydata.org/generated/seaborn.FacetGrid.html

[<b>Back to Table of Contents</b>](#table-of-contents)







