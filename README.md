# PROJECT OVERVIEW: Data Visualization of Migration to Canada (with Python)

  <ul>
    <li>Predict Rental Prices across 6 major Canadian cities in 2025 given permanent resident data and rental price data.</li>
    <li>Scraped Permanent Resident Admissions data (since 2015) from Immigration, Refugees and Citizenship Canada.</li>
    <li>Generated synthetic rental price data using a comprehensive ChatGPT prompt to compensate for lack of propietary data.</li>
    <li>Performed Hyperparamter Tuning on Linear Regression and Random Forest Regressor models using GridSearchCV to reach the best models.</li>
  </ul>
  
## Code and Resources Used
  <ul>
    <li><b>IDEs Used:</b> Google Colab, Jupyter Notebook</li>
    <li><b>Python Version:</b> 3.10.12</li>
    <li><b>Libraries and Packages:</b>
    <ul>
      <li><b><i>sklearn Packages:</i> </b> ColumnTransformer, Pipeline, StandardScaler, OneHotEncoder, train_test_split, LinearRegression, mean_squared_error, r2_score, RandomForestRegressor, make_scorer, cross_val_score, GridSearchCV</li>
      <li><b> <i>Other Packages:</i> </b> pandas, files (from google.colab), seaborn</li>
    </ul></li>
    <li><b>ChatGPT version:</b> GPT-4</li>
  </ul>
  
## Web Scraping
Permanent Residence admission Data was scraped from this website: https://open.canada.ca/data/en/dataset/f7e5498e-0ad8-4417-85c9-9b8aff9b9eda/resource/81021dfd-c110-42cf-a975-1b9be8b82980 

## Feature Engineering
The following ChatGPT prompt was used to generate our synthetic data:

<i>Generate a realistic dataset of rental prices for major Canadian cities, including Vancouver, Toronto, Montreal, Calgary, Ottawa, Edmonton, and Halifax. The dataset should include:</i>

<i><b>1.	Data Columns:</b>
<ul>
    <li>City: Major cities like Toronto, Vancouver, Montreal, Calgary, etc.</li>
    <li>Province: Corresponding provinces (e.g., Ontario, British Columbia).</li>
    <li>Libraries and Packages:</li>
    <li>Year: From 2019 to 2023.</li>
  <li>Month: January to December.</li>
  <li>Rental Type: Apartment, Condo, Detached House, Townhouse.</li>
  <li>Number of Bedrooms: 1, 2, 3, 4, etc.</li>
  <li>Number of Bathrooms: 1, 2, 3, etc.</li>
  <li>Square Footage: Ranges for different rental types.</li>
  <li>Furnished: Yes/No.</li>
  <li>Pet Friendly: Yes/No.</li>
  <li>Parking Included: Yes/No.</li>
  <li>Distance to City Center (km): Numeric value.</li>
  <li>Monthly Rent (Target): Dependent variable, with realistic pricing trends.</li>
  <li>Walk Score: A score between 0 and 100 indicating walkability.</li>
  <li>Transit Score: A score between 0 and 100 indicating access to public transit.</li>
  <li>Age of Building: Number of years since the building was constructed.</li>
  <li>Energy Efficiency Rating: Numeric score (e.g., 0–10).</li>
  <li>Lease Term: Length of the lease in months (e.g., 6, 12, 24).</li>
  <li>Noise Level: Numeric score (e.g., 1–10, with 10 being very noisy).</li>
  <li>Nearby Schools Rating: Average rating of schools in the area (1–10).</li>
  <li>Internet Availability: Yes/No indicating high-speed internet availability.</li>
  <li>Crime Rate Index: A score representing the area's safety.</li>
  <li>Annual Property Tax: Approximation based on rent and location.</li>
  </ul>


<b>2.	Realism:</b>
<ul>
<li>Average monthly rent should reflect the general cost of living in each city. For example, Vancouver and Toronto should have higher average rents compared to Edmonton or Halifax.</li>
<li>Include a range of rental prices within cities to capture variability (e.g., downtown areas vs. suburban neighborhoods).</li>
<li>Use realistic distributions for rental prices, square footage, and proximity to transit. For instance, apartments should generally be smaller and less expensive than single-family homes.</li>
</ul>

<b>3.	Additional Notes:</b>
<ul>
<li>Include 10,000 rows of data distributed proportionally across cities.</li>
<li>Reflect seasonality and trends where applicable (e.g., higher prices in Toronto and Vancouver for smaller units due to demand).</li>
<li>Ensure property types align with city norms (e.g., more condos in downtown Toronto, more single-family homes in Calgary suburbs).</li>
</ul>
</i>


## Data Cleaning & Exploratory Data Analysis
  <ul>
    <li>Target Variable=MonthlyRent</li>
    <li>Feature variables categorized into three types: Categorical Variables, Discrete Variables and Continuous Variables.</li>
    <li>Pairwise plots were produced using Seaborn to identify patterns and relationships.</li>
  </ul>
  
![image](https://github.com/user-attachments/assets/49096bf0-eb45-4adb-bafb-11d2a8a7bd10)

  <ul>
    <li>The following features had the most influence on MonthlyRent, and to be used for model building: City, RentalType, Year, Month, Bedrooms, 
SquareFootage, and AnnualPropertyTax.</li>
    <li>Performed Categorical Encoding and Standardized Scaling for pre-processing pipeline, where:</li>
    <ul>
      <li>Dependant variable=MonthlyRent</li>
      <li>Categorical variables=City, RentalType</li>
      <li>Discrete variables=Year, Month, Bedrooms, SquareFootage, Admissions</li>
      <li>Continuous variables=AnnualPropertyTax</li>
    </ul>

## Model Building
<ul>
    <li>Steps for model selection (both linear regression and random forest regressor):</li>
    <ul>
      <li>(1) Define target (y) and features (X) </li>
      <li>(2) Encode categorical features</li>
      <li>(3) Split data into training and testing sets, size=0.2</li>
      <li>(4) Initialize, then train model</li>
      <li>(5) Get model coefficients and intercept</li>
      <li>(6) Make predictions on test set</li>
      <li>(7) Evaluate model</li>
      <li>(8) Perform k-fold cross-validation (k=5)</li>
      </ul>
    <li>Performed hyperparameter tuning on random forest regressor using GridSearchCV.</li>
  </ul>
  
## Model Performance
<b>Linear Regression Model:</b>
  <ul>
    <li><b>RMSE:</b> 114799.009005</li>
    <li><b>R^2 Score:</b> 0.935382</li>
   <li><b>Average MSE from Cross-Validation:</b> 626996.754116</li>
    </ul>
<b>Random Forest Regressor:</b>
  <ul>
    <li><b>RMSE:</b> 34611.563041</li>
    <li><b>R^2 Score:</b> 0.980581</li>
   <li><b>Average MSE from Cross-Validation:</b> 716345.255222</li>
    </ul>

Random Forest Regressor performed better. As it is more suited for non-linear data, suggesting data's non-linearity.



