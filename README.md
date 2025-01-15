# PROJECT OVERVIEW: Data Visualization of Migration to Canada (with Python)
  <ul>
    <li>Performed data visualizations and geosoatial analysis of settlement patterns of immigrants (permanent and non-permanent) in Canada.</li>
    <li>National, provincial and territorial, and census metropolitan area [CMA] breakdown</li>
    <li>Scraped data from Statistics Canada. (census data and quarterly estimates)</li>
    <li>Performed feature engineering on some variables to create new variables.</li>
    <li>Downloaded shapefile of Canada's provincial and territorial boundaries to create choropleth map.</li>
    <li>N.B. 1: Some of the data from Statistics Canada are estimates based on 25% sampling.</li>
    <li>N.B. 2: For the purpose of this analysis, the Ottawa-Gatineau CMA was broken up into two parts: its Ontario and Quebec part, rendering the analysis of thew "Top 25" CMAs Top 26.</li>
    <li>N.B. 3: For the purpose of this analysis, the Ottawa-Gatineau CMA was broken up into two parts: its Ontario and Quebec part, rendering the analysis of thew "Top 25" CMAs Top 26.</li>
  </ul>
  
## Code and Resources Used
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
  
## Web Scraping
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

## Feature Engineering
<ul>
    <li><b>Non-Permanent residents:</b> Quarterly data for total non-permanent residents missing between 2018-2021. Quarterly data for net non-permanent migration used to calculate missing values.</li>
    <li><b>2021 Census Gender analysis:</b> For each country of origin, find total number of respondants that identify as women, divide by the raw total for that country of origin, then multiply by 100 to get percentage. The same method applies for the general population. </li>
    <li><b>Top 5 countries of origin by province and territory, recent immigrants (2021 census):</b> After determining each province and territory's top 5 countries of orign, take their raw total, by total province or territory's total recent immigrant population, then multiply by 100 to get their percentages.</li>
    <li><b>Age breakdown, nationally and by province and territory (2021 Census):</b> Find the age breakdown of the recent immigrant population (using the intervals [0,5), [5,15), [15,25), [25,45), 45 and above), and calculate their percentages. The age breakdown for the general population is more granular, necessitating arithmetic operations to match with the aforementioned intervals, then the same process can be executed. </li>
    <li><b>Non-permanent residents per-capita by CMA:</b> [NPR Population, 2021]/[CMA Population, 2021], then divided by 100,000.</li>
    <li><b>Growth rates of CMA:</b> [[CMA Population, 2021 Census] - [CMA Population, 2016 Census]]/[CMA Population, 2016 Census], then multiplied by 100</li>
    <li><b>Growth rates of CMA Non-Permanent Resident populations:</b> [[CMA NPR Population, 2021 Census] - [CMA NPR Population, 2016 Census]]/[CMA NPR Population, 2016 Census], then multiplied by 100 </li>
    <li><b>Per-capita population, recent immigrants, by continent of origin (CMAs, 2021):</b> For each continent of origin, take the total, divide by the CMA population, then divide by 100,000.</li>
    <li><b>Growth rate of Non-Permanent Residents, Q3 2022-Q3 2024:</b> [[NPR Population, Q3 2024] - [NPR Population, Q3 2022]]/[NPR Population, Q3 2022], then multiplied by 100</li>

</ul>

## Time-Series Analysis

<p></p>

![image](https://github.com/user-attachments/assets/4adb6cb1-0d54-4f6f-9a9f-4f1be46872dc)


<p></p>

![image](https://github.com/user-attachments/assets/e4c4745c-f0ed-446a-956e-1b73f116bf4b)




## Categorical Data Analysis

<p></p>

![image](https://github.com/user-attachments/assets/68b003fc-0895-4781-a30f-b023a9282ed8)

![image](https://github.com/user-attachments/assets/61092b9d-fd39-4b16-ba22-929cf9e12331)


<p></p>

![image](https://github.com/user-attachments/assets/ff5b9ada-36d6-40f1-a9bf-6596205df1c2)



<p></p>

![image](https://github.com/user-attachments/assets/a0d7ef70-55ba-4ab9-9d5a-cc01f7e8bea3)

![image](https://github.com/user-attachments/assets/be1d5411-889f-4aa8-b36d-94853fb87d1f)

![image](https://github.com/user-attachments/assets/85a8b8c6-63d6-45ba-b88a-bcf9d5148f15)

![image](https://github.com/user-attachments/assets/f2301fe9-67be-419a-9d4e-81fd6d2dbb95)


## Scatter Plot Analysis (CMAs)

<p></p>

![image](https://github.com/user-attachments/assets/d642d399-c8b6-4129-9d8f-fc2c74260992)

![image](https://github.com/user-attachments/assets/fb5d53e1-ae54-419a-9c59-8439efc391c5)



<p></p>

![image](https://github.com/user-attachments/assets/4a9aba8d-5915-4c48-ae18-fd102eb26a2e)

![image](https://github.com/user-attachments/assets/ae9bc189-97a6-496a-b3ba-26c6c8887919)

![image](https://github.com/user-attachments/assets/155724b9-578d-49e3-bb4a-05cb816b13af)



## Spatial Analysis

<p> Recall that the national non-permanent resident population rose dramatically after Q3 2022. Here is a choropleth map showing a geographic breakdown of that growth.</p>
<p> Nunavut by far experienced the fastest non-permanent resident growth within that time period, althoucgh that can largely be attributed to its small non-permanent resident. Alberta also experienced high growth, mirroring its generally high growth as a whole over the past decade. Growth has slowed down for British Columbia and Ontario. Surprisingly, the Maritime provinces experience relatively little growth despite government initiatives to attract immigrants and forign labour into that region. </p>


![image](https://github.com/user-attachments/assets/4809a5b3-4682-4ee3-a165-be5e6e70e738)


## Discussion

<p>By making this kind of data more granular and adding a spatial and geographic component, policy decisions both within and outside Canada can be remodelled to better cater to communities with different needs and socioeconomic conditions. For example,</p>
<ul>
  <li>A country’s consular services can be redirected more towards underserved communities, especially communities with high levels of non-permanent migration.</li>
  <li>Which governments will have to do more to provide more specialized services to help certain communities integrate well?</li>
</ul>





