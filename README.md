# PROJECT OVERVIEW: Data Visualization of Migration to Canada (with Python)
  <ul>
    <li>Performed data visualizations and geosoatial analysis of settlement patterns of immigrants (permanent and non-permanent) in Canada.</li>
    <li>Scraped data from Statistics Canada. (census data and quarterly estimates)</li>
    <li>Performed feature engineering on some variables to create new variables.</li>
    <li>Downloaded shapefile of Canada's provincial and territorial boundaries to create choropleth map.</li>
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
    <li><b>Top 10 Sources of International Migration in 2020:</b></li>
    <li><b>Census Data:</b> 3.10.12</li>
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
  </ul>

## Feature Engineering

Non-Permanent residents

Top 10 Sources of International Migration in 2020

Gender analysis: 2021 census women divided by total . For general population.

Country of origin: after determining, divide country recent immigrants by total recent immigrants

Since age data for general population convert raw to percentage divide amount by total. Since age breakdown for more granular, 

Non-permanent residents per-capita: NPR / CMA pop

Growth rates of CMA

Growth rates of NPR pop 

Per-capita population recent immigrants

Growth rate of NPR



## Time-Series Analysis

Analysis 1
![image](https://github.com/user-attachments/assets/03d9e24a-170a-457b-b0f1-0b761813bde9)


Analysis 2
![image](https://github.com/user-attachments/assets/74ed8f90-e6a4-46c4-8a81-3480b90ba132)


Analysis 3

![image](https://github.com/user-attachments/assets/662fe140-ef7d-4cfe-bfd3-3c3c12cd1834)



## Categorical Data Analysis

Gender Breakdown

![image](https://github.com/user-attachments/assets/23336d6e-132c-4013-9714-b11f7c4bb0f9)


![image](https://github.com/user-attachments/assets/8be8f594-a276-45a6-b162-0ab86f75d9a2)


Top 5

![image](https://github.com/user-attachments/assets/2853a607-2df6-4373-829f-feb71d23fa2c)


Age
![image](https://github.com/user-attachments/assets/a0d7ef70-55ba-4ab9-9d5a-cc01f7e8bea3)

![image](https://github.com/user-attachments/assets/be1d5411-889f-4aa8-b36d-94853fb87d1f)

![image](https://github.com/user-attachments/assets/85a8b8c6-63d6-45ba-b88a-bcf9d5148f15)

![image](https://github.com/user-attachments/assets/f2301fe9-67be-419a-9d4e-81fd6d2dbb95)


## Scatter Plot Analysis

Plot 1/2
![image](https://github.com/user-attachments/assets/2087a234-f7cd-4048-844c-26b0ca1b4318)


Plot 3
![image](https://github.com/user-attachments/assets/54482f66-032f-4979-afeb-d351ea3aba72)

![image](https://github.com/user-attachments/assets/79432d4b-ceeb-4392-9e9f-6a8234a25de8)


## Spatial Analysis

![image](https://github.com/user-attachments/assets/4809a5b3-4682-4ee3-a165-be5e6e70e738)




