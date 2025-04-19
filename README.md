# Data Visualization of Migration to Canada (with Python)

# Table of Contents
* [Project Background](#project-background)
* [Data Structure and Initial Checks](#data-structure-and-initial-checks)
* [Executive Summary](#executive-summary)
* [Insights Deep Dive](#insights-deep-dive)
* [Recommendations](#recommendations)
* [Assumptions and Caveats](#assumptions-and-caveats)

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

For the report version of the analysis: [Link to Download](https://github.com/Francis-Calingo/Visualizing-Migration-in-Canada/raw/main/Patterns%20within%20Patterns_%20Using%20Python%20and%20Excel%20to%20Unlocking%20Hidden%20Migration%20and%20Settlement%20Patterns%20in%20Canada.pdf)

For the walkthrough of the project in video form: [Video](https://drive.google.com/file/d/14W0qtsOJdgzcSmXcvERx3pGHeB3109VV/view)

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

---

# Executive Summary

### Overview of Findings

The time-series visualizations showed a rapid increase of migration ,particulalry with regards to non-permanent migration as well as people landing from India and Syria.

[Visualization, including a graph of overall trends or snapshot of a dashboard]

With regards to the categorical data analysis, we noticed some consistency with each province and territory's major sources of migrants, with some exceptions (notably Quebec, where their major sources of migrants remain francophone countries). The age distribution is characterized by , with most immigrants falling within the working age range (), while some ethnic groups in certain provinces exhbitied some anomalies with regards to the gender distribution.

In terms of the scatter plto analysis, clustering was apparent with census metropolitan areas from certain regions (e.g., Parairie CMAs) exhibiting similar migration patterns.

Over the past few years, Nunavut and Alberta experienced the highest non-permanent resident growth rate, while the Atlantic region was surprisingly low in comparison.

---

# Insights Deep Dive
### Time-Series Analysis:

* **There ** More detail about the supporting analysis about this insight, including time frames, quantitative values, and observations about trends.
  
* **Seasonality is observed with quarterly immigration data.** Policy changes (e.g., changes to immigration policies following the lifting of all federal COVID-19 regulations in 2022), as well as major historical events (e.g., COVID-19) had visible effects on migration in recent years, but other than that, the patterns in immigration remain largely seasonal, with _____.
  
* **The top three sources of immigrants for Canada remain unchanged over the past two decades, while some countries have become a bigger source of migration to Canada over the past decade.** In no particular order, China, India, and the Philippines remain the top three sources of immigration to Canada, with each country taking turns as being the top source. Other countries such as Syria and Nigeria have seen an increase over the past decade, with Syria's increase in particular having been fuelled by the recently concluded Syrian Civil War as well as drastic changes in refugee policies stemming from a change in government in 2015.

---

### Categorical Data Analysis:

* **Main insight 1.** More detail about the supporting analysis about this insight, including time frames, quantitative values, and observations about trends.
  
* **Main insight 2.** More detail about the supporting analysis about this insight, including time frames, quantitative values, and observations about trends.
  
* **Main insight 3.** More detail about the supporting analysis about this insight, including time frames, quantitative values, and observations about trends.
  
* **Main insight 4.** More detail about the supporting analysis about this insight, including time frames, quantitative values, and observations about trends.

[Visualization specific to category 2]


### Scatter Plot Analysis:

* **Main insight 1.** More detail about the supporting analysis about this insight, including time frames, quantitative values, and observations about trends.
  
* **Main insight 2.** More detail about the supporting analysis about this insight, including time frames, quantitative values, and observations about trends.
  
* **Main insight 3.** More detail about the supporting analysis about this insight, including time frames, quantitative values, and observations about trends.
  
* **Main insight 4.** More detail about the supporting analysis about this insight, including time frames, quantitative values, and observations about trends.

[Visualization specific to category 3]


### Category 4:

* **Main insight 1.** More detail about the supporting analysis about this insight, including time frames, quantitative values, and observations about trends.
  
* **Main insight 2.** More detail about the supporting analysis about this insight, including time frames, quantitative values, and observations about trends.
  
* **Main insight 3.** More detail about the supporting analysis about this insight, including time frames, quantitative values, and observations about trends.
  
* **Main insight 4.** More detail about the supporting analysis about this insight, including time frames, quantitative values, and observations about trends.

[Visualization specific to category 4]

---

# Recommendations:

Based on the insights and findings above, we would recommend the [stakeholder team] to consider the following: 

* Specific observation that is related to a recommended action. **Recommendation or general guidance based on this observation.**
  
* Specific observation that is related to a recommended action. **Recommendation or general guidance based on this observation.**
  
* Specific observation that is related to a recommended action. **Recommendation or general guidance based on this observation.**
  
* Specific observation that is related to a recommended action. **Recommendation or general guidance based on this observation.**
  
* Nunavut has experienced rapid growth rate, but . **Recommendation or general guidance based on this observation.**
  
---

# Assumptions and Caveats:

Throughout the analysis, multiple assumptions were made to manage challenges with the data. These assumptions and caveats are noted below:

* Assumption 1 (ex: missing country records were for customers based in the US, and were re-coded to be US citizens)
  
* Data only goes up to the third quarter of 2024 (i.e., September 30). Recent changes to immigration policies by the federal government have either not gone to fruition yet or have only been recently implemented. The analysis will therefore not account for the anticipated drop in immigration in the coming months.
  
* Some of the datasets are estimates based on a 25% sample size and not the full count, which may slightly render parts of the data not fully accurate, but the agency’s methodology balances accuracy and operational costs effectively.



=========================================

## Table of Contents
* [Introduction](#introduction)
* [Code and Resources Used](#code-and-resources-used)
* [Web Scraping](#web-scraping)
* [Feature Engineering](#feature-engineering)
* [Time-Series Analysis](#time-series-analysis)
* [Categorical Data Analysis](#categorical-data-analysis)
* [Scatter Plot Analysis (Top 25 CMAs**)](#scatter-plot-analysis-top-25-cmas)
* [Spatial Analysis](#spatial-analysis)
* [Discussion](#discussion)

<details><summary><h2>Introduction</h2></summary> 
  <ul>
    <li>Performed data visualizations and geospatial analysis of settlement patterns of immigrants (permanent and non-permanent) in Canada.</li>
    <li>National, provincial and territorial, and census metropolitan area [CMA] breakdown</li>
    <li>Scraped data from Statistics Canada. (census data and quarterly estimates)</li>
    <li>Performed feature engineering on some variables to create new variables.</li>
    <li>Downloaded shapefile of Canada's provincial and territorial boundaries to create choropleth map.</li>
    <li>N.B. 1: Some of the data from Statistics Canada are estimates based on 25% sampling.</li>
    <li>N.B. 2: For the purpose of this analysis, the Ottawa-Gatineau CMA was broken up into two parts: its Ontario and Quebec part, rendering the analysis of the "Top 25" CMAs Top 26.</li>
    <li>N.B. 3: Statistics Canada's definition of "recent immigrants" is those that migrated to Canada within the last 5 years of a census year (e.g., 2016-2021, 2011-2016, 2006-2011, etc.)</li>
  </ul>

</details>

<details><summary><h2>Code and Resources Used</h2></summary>  
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
</details>

<details><summary><h2>Web Scraping</h2></summary>    
  <ul>
    <li><b>Top 10 Sources of International Migration in 2020: </b> https://www.canada.ca/en/immigration-refugees-citizenship/corporate/publications-manuals/annual-report-parliament-immigration-2021.html#gba</li>
    <li><b>Census Data:</b></li>
    <ul>
      <li><b>2021: </b> https://www12.statcan.gc.ca/census-recensement/2021/dp-pd/prof/details/page.cfm?LANG=E&GENDERlist=1,2,3&STATISTIClist=1,4&DGUIDlist=2021A000011124&HEADERlist=26&SearchText=canada </li>
      <li><b>2016: </b> https://www12.statcan.gc.ca/census-recensement/2016/dp-pd/prof/details/page.cfm?Lang=E&Geo1=PR&Code1=01&Geo2=PR&Code2=01&SearchText=Canada&SearchType=Begins&SearchPR=01&B1=Immigration%20and%20citizenship&TABID=1&type=0 </li>
      <li><b>2011:</b> https://www12.statcan.gc.ca/nhs-enm/2011/dp-pd/dt-td/Rp-eng.cfm?TABID=2&LANG=E&APATH=3&DETAIL=0&DIM=0&FL=A&FREE=0&GC=0&GK=0&GRP=1&PID=105411&PRID=0&PTYPE=105277&S=0&SHOWALL=0&SUB=0&Temporal=2013&THEME=95&VID=0&VNAMEE=&VNAMEF= </li>
      <li><b>2006:</b> https://www12.statcan.gc.ca/census-recensement/2006/dp-pd/hlt/97-557/T404-eng.cfm?Lang=E&T=404&GH=4&GF=1&SC=1&S=1&O=D#FN2 </li>
      <li><b>2001:</b> https://www12.statcan.gc.ca/english/census01/products/standard/themes/Rp-eng.cfm?LANG=E&APATH=3&DETAIL=1&DIM=0&FL=A&FREE=0&GC=0&GID=0&GK=0&GRP=1&PID=62124&PRID=0&PTYPE=55430,53293,55440,55496,71090&S=0&SHOWALL=0&SUB=0&Temporal=2001&THEME=43&VID=0&VNAMEE=&VNAMEF= </li>
    </ul></li>
    <li><b>Quarterly Data:</b>
    <ul>
      <li><b>Archived - Estimates of non-permanent residents, quarterly, inactive, 2001-2018: </b> https://www150.statcan.gc.ca/t1/tbl1/en/tv.action?pid=1710002301&cubeTimeFrame.startMonth=01&cubeTimeFrame.startYear=2001&cubeTimeFrame.endMonth=10&cubeTimeFrame.endYear=2018&referencePeriods=20010101%2C20181001 </li>
      <li><b>Estimates of non-permanent residents, quarterly, 2021-2024: </b> https://www150.statcan.gc.ca/t1/tbl1/en/tv.action?pid=1710012101&pickMembers%5B0%5D=1.1&cubeTimeFrame.startMonth=01&cubeTimeFrame.startYear=2021&cubeTimeFrame.endMonth=10&cubeTimeFrame.endYear=2024&referencePeriods=20210101%2C20241001 </li>
      <li><b>Estimates of the components of international migration, quarterly:</b> https://www150.statcan.gc.ca/t1/tbl1/en/tv.action?pid=1710004001&pickMembers%5B0%5D=1.1&cubeTimeFrame.startMonth=01&cubeTimeFrame.startYear=2001&cubeTimeFrame.endMonth=10&cubeTimeFrame.endYear=2024&referencePeriods=20010101%2C20241001</li>
    </ul></li>
    <li><b>Shapefile: </b> https://www12.statcan.gc.ca/census-recensement/2021/geo/sip-pis/boundary-limites/index2021-eng.cfm?year=21</li>
  </ul>
</details>

<details><summary><h2>Feature Engineering</h2></summary>  
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

<details><summary><h2>Time-Series Analysis</h2></summary>  

<p>The first plot is a breakdown of the number of non-permanent residents in Canada quarterly by provinces and territories, you’ll notice the dip in NPRs during the first three waves of COVID-19, reflecting the travel restrictions of the time, as well as the accelerated growth after 2022, reflecting domestic labour shortages.  </p>
<p>The next plot is net quarterly international migration. Once again you see the effects COVID had on migration, as well as the increase in numbers after all COVID-related restrictions were lifted. You can also see the seasonality of migration with all these peaks and valleys.</p>

![image](https://github.com/user-attachments/assets/4adb6cb1-0d54-4f6f-9a9f-4f1be46872dc)

<p>An advantage of Plotly is its interactivity. In this case, it's the ability to look at province(s) and/or territory (or territories) in isolation. For example, let's examine Nova Scotia's non-permanent resident population and Saskatchewan's quarterly net international migration:</p>

![image](https://github.com/user-attachments/assets/b227050b-e253-42c4-aad5-74d6560c4917)

![image](https://github.com/user-attachments/assets/f925f5ca-42fc-47b1-83cc-a5eccb163b38)


<p>The next plot breaks migration patterns of recent migrants down census-by-census, using the top 10 countries of origin from 2020. China, India, and the Philippines have consistently been Canada's top 3 countries of origin, with recent immigrants from India especially seeing an accelerated growth.</p>

![image](https://github.com/user-attachments/assets/e4c4745c-f0ed-446a-956e-1b73f116bf4b)

<p>Observe the rapid growth of the Syrian migrant population in the 2010s coinciding with the Syrian Civil War.</p>

![image](https://github.com/user-attachments/assets/0e3796f2-046c-469b-8ae2-279b4100d8e0)

</details>


<details><summary><h2>Categorical Data Analysis</h2></summary>  

<p> The first plot is a gender analysis of recent migrants (2016-21) by province and territories. Each bar represents the % of recent migrants by country of origin in province and territory that identify as woman, and this dash line represents the percentage of the general population within each geographic area. We see here that there are some variations by country, on one extreme is Japan with the largest positive percent difference, and on the other extreme is the Republic of Ireland.  If we look at the different provinces and territories, some countries of origin display consistent behaviour like Japan, and others like Burundi (in Alberta), you’ll see that there is a much bigger difference.</p>

![image](https://github.com/user-attachments/assets/68b003fc-0895-4781-a30f-b023a9282ed8)

![image](https://github.com/user-attachments/assets/61092b9d-fd39-4b16-ba22-929cf9e12331)


<p>The next plot is a stacked bar chart that looks at each province and territory’s top 5 countries of origin amongst recent migrants (2016-21). Some countries like China consistently show up. There are a few interesting cases such as the US and UK making it to British Columbia’s Top 5. Québéc's migration pattern stood out, where even its linguistic culture has an impact on migration, as all but one of the top 5 countries are francophone countries or countries where French is widely understood.</p>

![image](https://github.com/user-attachments/assets/ff5b9ada-36d6-40f1-a9bf-6596205df1c2)

<p>As this is a Plotly plot, we can see certain aspects of the plot in isolation. For example, when we filter for the Philippines, we can see that recent immigrants from the Philippines take up a significant portion of the recent migrant population in places such as Newfoundland and Labrador and NWT. Conversely, they don’t even make the Top 5 In Québéc (likely due to language barriers).</p>

![image](https://github.com/user-attachments/assets/36dd722a-3213-4f54-90e9-77d2418ef04a)


<p>The next plot is an age-based analysis comparing the age distribution of the general population versus the total immigrant population, again using 2021 census data. This FacetGrid shows a general pattern that people aged 25-44 make up the plurality of the foreign-born population, but those aged 45+ make up the plurality of the general population. Of course, there are a few interesting cases such as Nunavut, where the young age on average as a whole is visualized well here. So it seems that the characteristic of the foreign-born population is more oriented towards working-age adults than the general population.</p>

![image](https://github.com/user-attachments/assets/a0d7ef70-55ba-4ab9-9d5a-cc01f7e8bea3)

![image](https://github.com/user-attachments/assets/be1d5411-889f-4aa8-b36d-94853fb87d1f)

![image](https://github.com/user-attachments/assets/85a8b8c6-63d6-45ba-b88a-bcf9d5148f15)

![image](https://github.com/user-attachments/assets/f2301fe9-67be-419a-9d4e-81fd6d2dbb95)

</details>

<details><summary><h2>Scatter Plot Analysis (Top 25 CMAs**)</h2></summary>  

<p><i>See N.B. 2 at the beginning.</i></p>
<p>This first scatter plot compares CMA population to each CMA’s non-permanent resident population per capita, with points categorized by region (i.e., BC, Prairies, Ontario, Québéc, Atlantic). You can see that outside of Montreal, Québéc has quite a low per-capita non-permanent resident population. Everything else is pretty much à mixed bag.</p>

![image](https://github.com/user-attachments/assets/d642d399-c8b6-4129-9d8f-fc2c74260992)

<p>Secondly, the growth rates of these CMAs and their immigrant population (2016-21) were compared. Again they are broken down by region. And based on this graph, you can see that pretty much every CMA’s foreign-born population is outpacing their general population’s growth rate, with a bit of regional variations. BC exhibited the highest general population growth rate, but the Atlantic exhibited the highest foreign-born population growth rate.</p>

![image](https://github.com/user-attachments/assets/fb5d53e1-ae54-419a-9c59-8439efc391c5)

<p>The third plot is a FacetGrid of some scatter plots comparing CMA populations to per-capita recent immigrant populations broken down by continents of origin, and colours once again assigned by region. Note that using Seaborn instead of Plotly changed the colouring scheme. For the most part, there were no interesting nor discernible patterns for the rate of migration for people from the Americas, Europe, and Oceania. But where it gets interesting is looking at the plots for Africa and Asia. It’s more dispersed for the Asia plot versus the Africa plot.</p>

![image](https://github.com/user-attachments/assets/4a9aba8d-5915-4c48-ae18-fd102eb26a2e)

![image](https://github.com/user-attachments/assets/ae9bc189-97a6-496a-b3ba-26c6c8887919)

![image](https://github.com/user-attachments/assets/155724b9-578d-49e3-bb4a-05cb816b13af)


<p>But look at the point circled in red. This is Montreal, observe the difference between see the difference between both plots. It appears that migrants of African origin, on a per-capita basis, is comparatively high compared to other CMAs, while it is comparatively lower with migrants of Asian origin.And to some extent it rings true for the rest of Québéc. </p>

![image](https://github.com/user-attachments/assets/97284812-3263-4420-a91f-082b4970c3e6)

![image](https://github.com/user-attachments/assets/9809442c-bd90-4158-8a7b-9f29fd76a197)

  
<p>Also, the cluster of red points represents Prairie CMAs, suggesting that they share a similar migration pattern. </p>

![image](https://github.com/user-attachments/assets/e1d42442-9d4b-447b-a565-fc22dfa785ff)

![image](https://github.com/user-attachments/assets/66904767-2e5b-4408-87ec-9563225a1d77)

</details>

<details><summary><h2>Spatial Analysis</h2></summary>  

<p> Recall that the national non-permanent resident population rose dramatically after Q3 2022. Here is a choropleth map showing a geographic breakdown of that growth.</p>
<p> Nunavut by far experienced the fastest non-permanent resident growth within that time period, although that can largely be attributed to its small non-permanent resident. Alberta also experienced high growth, mirroring its generally high growth as a whole over the past decade. Growth has slowed down for British Columbia and Ontario. Surprisingly, the Maritime provinces experience relatively little growth despite government initiatives to attract immigrants and foreign labour into that region. </p>


![image](https://github.com/user-attachments/assets/4809a5b3-4682-4ee3-a165-be5e6e70e738)

</details>

<details><summary><h2>Discussion</h2></summary>  

<p>By making this kind of data more granular and adding a spatial and geographic component, policy decisions both within and outside Canada can be remodelled to better cater to communities with different needs and socioeconomic conditions. For example,</p>
<ul>
  <li>A country’s consular services can be redirected more towards underserved communities, especially communities with high levels of non-permanent migration.</li>
  <li>Which governments will have to do more to provide more specialized services to help certain communities integrate well?</li>
</ul>

</details>




