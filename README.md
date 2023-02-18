# Housing Development Board (HDB) Resale Flat Prices Prediction

___Note___: Before running the codes, please unzip `train.csv.zip` file in the `datasets` folder.

## Background
Singapore allocates 14% of their land to address the nation's housing needs. With the evergrowing resident population (6 million as of 2023), the demand for housing flats continuously exceeds the supply. This has resulted in a yearly steady increase in housing prices.

New flat buyers have two purchasing options for HDB flats - 1) Buying a Built-To-Order (BTO) flat or 2) Buying from the resale market.

Each option has their pros and cons for buyers to consider before making a purchasing decison.

Some key factors to consider include: </br>

___1. Eligibility Criteria___
- BTO flats have an income ceiling for combined income, capped at `SGD$`14,000.

- Flat purchasers can opt for an executive condominium if their combined income does not exceed `SGD$`16,000.

- If the combined income exceeds the above mentioned ceilings, flat purchasers will have to buy from the resale market instead.

- BTO applicants must also have only purchased up to one HDB, DBSS (Design, Build and Sell Scheme) or executive condominium in the past.

___2. Price___
- BTO flats are known to be cheaper than resale flats (note: this might not equate to having a cheaper cost per floor area)

___3. Location___
- BTO applicants must be prepared to accept that the ideal location of choice might not be awarded.

- If applying to a popular location, the applicant has to be prepared for it to be oversubscribed.

- The resale market offers more flexibility on the choice of location.

___4. Lease Tenure___
- New BTO flats have a fresh 99-year lease and the next generation (i.e. children of the purchaser) can continue to stay in the flat for the remaining duration.

- Purchasing from the resale market would mean purchasing the remaining lease of the chosen flat.

___5. Waiting Period___
- Average waiting period for a BTO flat to be built is between 2.4 - 5.3 years, with an average waiting time of 4.1 years.

- Flat purchasers looking at resales flats will be able to purchase these flats immediately as they have already been built.

- Flat purchasers who are married or already have children might be less inclined to wait for a BTO flat.

___6. Renovation Cost___
- Renovation cost for a resale flat is higher than that of a BTO flat as it involves an extensive amount of hacking and rebuilding of existing features within a flat.

- Average amount a flat purchaser may spend on renovations for a resale flat may range from `SGD$`40,000 for a 3-room flat to `SGD$`79,000 for a 5-room flat.

- The above amount is relatively high in comparison to `SGD$`38,500 for 3-room BTO flat and `SGD$`52,000 for a 5-room BTO flat.

___7. Future Market Value___
- BTO flats fetch a higher resale value after its Minimum Occupancy Period (MOP) - 5 years into its lease.

- Upon reaching MOP, the BTO flat will compete in the open market, within the same location, with other resale flats that could be alot older.

- This gives the BTO flat a slight advantage and enables it to command a higher selling price.

Sources: </br>
- https://sites.google.com/site/environmentalcomparison/lab </br>
- https://dollarsandsense.sg/bto-vs-resale-choose/

The analysis conducted focuses on HDB flats in the resale market, to make predictions on its future prices using machine learning algorithms. The results are then submitted to a kaggle competition (https://www.kaggle.com/competitions/dsi-sg-project-2-regression-challenge-hdb-price) for evaluation against the baseline score resulting from the baseline submission.

## Problem Statement
NexProp is a newly established real estate company, specialising in the provision of data-driven recommendations for its customers.

As NexProp's first data scientist within its data science division, NexProp would like you to provide an overview of the resale market landscape and identify key features that drives the increase in HDB resale prices every year.

With the key features indetified, this would enable NexProp to make predicitions on future HDB resale prices.

## Data Dictionary
The raw datasets, obtained from [Data.gov.sg](https://data.gov.sg) - the Singapore government's one-stop portal to its publicly-available datasets from 70 public agencies, were used for the analysis and machine learning. </br>

The two raw files used were:
- `train.csv`
- `test.csv`

Both datasets were cleaned to output the following:
- `train_cleaned.csv`
- `test_cleaned.csv`

During exploratory data analysis, both `train_cleaned.csv` and `test_cleaned.csv` were imported for the addition of an additional column - `lease_remaining` before exporting for use in machine learning:
- `ML_train.csv`
- `ML_test.csv`</br> </br>

`kaggle_baseline_submission.csv` uploaded to kaggle provided a baseline for the performance scoring of the experimented models.

The predicted results, following the format of `sample_sub_reg.csv`, were exported as `result.csv` to be submitted on kaggle for the final scoring.


A brief description on the features extracted and used for analysis is shown below: </br>

|Feature|Type|Dataset|Description|
|---|---|---|---|
|town|object||HDB township where the flat is located, e.g. BUKIT MERAH|
|flat_type|object||type of the resale flat unit, e.g. 3 ROOM|
|resale_price|float64||the property's sale price in Singapore dollars|
|Tranc_Year|int64||year of resale transaction|
|Tranc_Month|int64||month of resale transaction|
|floor_area_sqft|float64||floor area of the resale flat unit in square feet|
|max_floor_lvl|int64||highest floor of the resale flat|
|1room_sold|int64||number of 1-room residential units in the resale flat|
|2room_sold|int64||number of 2-room residential units in the resale flat|
|3room_sold|int64||number of 3-room residential units in the resale flat|
|4room_sold|int64||number of 4-room residential units in the resale flat|
|5room_sold|int64||number of 5-room residential units in the resale flat|
|exec_sold|int64||number of executive type residential units in the resale flat block|
|multigen_sold|int64||number of multi-generational type residential units in the resale flat block|
|studio_apartment_sold|int64||number of studio apartment type residential units in the resale flat block|
|Latitude|float64||Latitude based on postal code|
|Longitude|float64||Longitude based on postal code|
|Mall_Nearest_Distance|float64||distance (in metres) to the nearest mall|
|Hawker_Nearest_Distance|float64||distance (in metres) to the nearest hawker centre|
|mrt_nearest_distance|float64||distance (in metres) to the nearest MRT station|
|bus_stop_nearest_distance|float64||distance (in metres) to the nearest bus stop|
|pri_sch_nearest_distance|float64||distance (in metres) to the nearest primary school|
|sec_sch_nearest_distance|float64||distance (in metres) to the nearest secondary school|
|remaining_lease|int64||number of years remaining on the original 99-year leasehold agreement for the property|

## Summary of Analysis
There are several key factors that determine the variability in HDB resale prices:
- `Location`: Resale flats in prime locations such as central areas, near MRT stations, or with a good view generally command higher prices.
- `Size`: The size of the flat is a major factor, with larger flats typically costing more.
- `Age of the building`: Newer buildings tend to have a higher resale value compared to older buildings.
- `Floor level`: Flats on higher floors are generally more expensive than those on lower floors.
- `Leasehold`: The remaining lease of a resale flat also plays a role in determining its price, a buyers would prefer to buy a flat with a longer lease.

Sources:
- https://www.99.co/singapore/insider/factors-affecting-property-resale-value-2/
- https://www.propertyguru.com.sg/property-guides/hdb-valuation-sales-12882
- https://www.iproperty.com.sg/news/4-factors-that-will-affect-your-flats-resale-value/

The features were further filtered based on the preliminary research conducted, resulting in the feature list listed in the data dictionary.

The analysis informed on the changes in resale prices over the past decade and how multi-generation flats performed differently.

Following which, a deeper analysis was conducted on the effect of `remaining_lease`, `floor_area_sqft`, `max_floor_lvl`, `mrt_nearest_distance`, `bus_stop_nearest_distance`, `Mall_nearest_distance`, `pri_sch_nearest_distance` and `sec_sch_nearest_distance` on the HDB resale prices.

To conclude the analysis, most popular flat types as well as the most expensive and cheapest flats were identified.

### Data Cleaning
Both `train.csv` and `test.csv` were imported into `01_Data_Cleaning.ipynb` for data cleaning.

The following steps were performed at the data cleaning stage:
- Irrelevant columns were dropped based on the preliminary research conducted on features that could potentially affect HDB resale prices.
- Unique values were identified to ensure categorical values had the same number of types of unique values. This is an essential and crucial step to ensure the machine learning conducted at a later stage is unaffected.
- Null values were identified in the `Mall_Nearest_Distance` column in which the median value were imputed due to the distribution of values being right skewed.
- `floor_area_sqft` data type was converted from float64 to int as it had no trailing decimal values
- Outliers were identified using interquartile range but not dropped due to them having a significant presence in our data. This essentially meant that they could be non-outliers.

Both cleaned datasets were then exported as `train_cleaned.csv` and `test_cleaned.csv`.

### Exploratory Data Analysis
Both `train_cleaned.csv` and `test_cleaned.csv` were imported to `02_EDA.ipynb` to commence exploratory data analysis (EDA).

Before jumping into the analysis, an additional column, originally not in the dataset, was created - `remaining_lease`. `hdb_age` was then dropped as most purchasers would be more interested to know the remaining lease. These changes were effected on both imported datasets and `test_cleaned.csv` was exported as `ML_test.csv` to be used for machine learning at the subsequent stages.

The new dataset from `train_cleaned.csv` was used for the remaining of this notebook as it contains the existing resale pricing data which is the key focus for the data analysis.

___Distribution of HDB Flats in Singapore___
- Singapore has done an excellent job for the geographical planning of HDB flats around the island.
- East of Singapore is more densely populated with flats which provides more options for flat purchasers.

___Fluctuation in Resale Prices of Flats Based on Flat Types from 2012 to 2021___
- Most flat types, except multi-generation flats, followed a similar trend for their respective resale prices.
- The difference in trend for resale prices could be attributed to the eligibility of buyers to purchases multi-generation flats, which resulted in a decrease in demand, ultimately affecting the resale price of the flat type.
- Buyers of these flats must be able to buy under the Public Scheme and to qualify, their family nuclei must consist of:
    - Married couple with one or both parents
    - Fiancé / Fiancée couples with one or both parents
    - Widow or widower with child, and one or both parents
    - Divorcee with child, and one or both parents
    - The parents must be registered as essential occupiers of the flat.
    - Essential occupiers cannot have another property under their name. </br>

Source: </br>
- https://stackedhomes.com/editorial/when-is-it-worth-buying-a-3gen-hdb-flat/#gs.orthcy

- With the price converging to that similar to executive flats, flat purchasers may consider purchasing the latter due to the more flexible buying criteria.

___Remaining Lease and Effect on Resale Price___
- HDB resale prices are higher for flats with a longer remaining lease.
- Unsurprisingly, the price of the resale flat depreciates as the remaining lease decreases.

___Average Resale Price of Flats in Various Towns___
- Bukit Timah, Bishan and Bukit Merah has the highest average resale prices for their flat
- Woodlands, Bukit Batok and Yishun has the lowest average resale prices for their flats.

___Volume of Flat Types___
- 4 room flats makes up majority of flats in the resale market.
- Multi-generation flats are not as readily available probably due to its stringent eligbility criterias.

___Floor Area and Effect on Resale Price___
- As the floor area increase, the resale price increases proportionally.

___Max Floor Level and Effect on Resale Price___
- Resale prices of flats increases as the max floor level increases.
- The data points are spread out quite randomly which suggests there is little to no correlation.

___Mrt Nearest Distance and Effect on Resale Price___
- Nearer the resale flats are to an MRT station, the higher the hdb resale price.
- Resale price of flats tend to decline if the flat is located further away from an MRT station.
- Higher datapoints are located on the left of the graph which supports the research that flats located near ammenities such as MRT stations tend to command a higher resale price.

___Bus Stop Nearest Distance and Effect on Resale Price___
- Points in the plot are spread out randomly and no clear pattern can be drawn.
- This indicates there is no strong correlation between the Bus Stop Nearest Distance and Resale Price.
- The trend line is relatively horizontal which indicates no strong correlation.

___Mall Nearest Distance and Effect on Resale Price___
- Similar to the analysis on MRT Nearest Distance, the resale prices tends to be higher for flats located closer to malls.
- Majority of resale flats are located within 1.5km of their nearest malls.

___Primary School Nearest Distance and Effect on Resale Price___
- Resale prices of flats tend to be higher for flats located closer to primary schools.
- However, there is no strong correlation between the resale price and nearest distance to primary schools.

___Secondary School Nearest Distance and Effect on Resale Price___
- Majority of resale flats has a secondary school within 1.5km.
- Interestingly, the resale prices of hdb flats increases the further it is from a secondary school.
- This could be due to other attributes such as:
    - `Location preference`: Being aware from secondary schools may offer peace and quiet, larger living spaces.
    - `Ammenitites`: There could be more ammenities in areas away from secondary school such as parks, shopping centers, entertainment venues.</br>

___Areas with Most Expensive and Cheapest Resale Flat___
- The most expensive flat sold was in CENTRAL AREA. The 5 room flat was sold for `SGD$`1.258 million.
- The cheapest flats that were sold were in Geylang and Toa Payoh. The 2 room flats were sold for `SGD$`150,000.

___Most Expensive and Cheapest Resale Flat Based on Flat Type___ </br>
***1 room flat***
- Most Expensive: Bukit Merah, `SGD$`257,000

- Least Expensive: Bukit Merah, `SGD$`157,000

***2 room flat***
- Most Expensive: Bukit Merah, `SGD$`510,000

- Least Expensive: Bukit Merah and Toa Payoh, `SGD$`150,000

***3 room flat***
- Most Expensive: Kallang/Whampoa and Queenstown, `SGD$`780,000

- Least Expensive: Serangoon and Toa Payoh, `SGD$`170,000

***4 room flat***
- Most Expensive: Clementi, `SGD$`780,888

- Least Expensive: Woodlands, `SGD$`218,000

***5 room flat***
- Most Expensive: Bukit Merah, `SGD$`781,000

- Least Expensive: Woodlands, `SGD$`270,000

***Executive flat***
- Most Expensive: Serangoon and Hougang, `SGD$`781,000

- Least Expensive: Choa Chu Kang, `SGD$`390,000

***Multi-generation flat***
- Most Expensive: Yishun, `SGD$`770,000

- Least Expensive: Tampines, `SGD$`600,000

## Feature Selection and Machine Learning
***Objective*** </br>
The objective of this step is to build a robust model that could accurately predict the future prices of HDB resale flats. (kaggle.com/competitions/dsi-sg-project-2-regression-challenge-hdb-price)

A baseline score, calculated using the mean values of existing resale prices was submitted to the kaggle competition to obtain a RMSE score to beat.

___Trial #1 - Baseline___ </br>
Baseline for feature selection and manipulation. </br>

Numeric Feeatures:
- floor_area_sqft
- remaining_lease
- mrt_nearest_distance
- max_floor_lvl

Categorical Features:
- town
- flat_type

***Key Findings***
- RMSE score of best performing model - Linear Regression, performs better than baseline submitted on kaggle (RMSE 58110 vs. RMSE 142970).
- Best model is one that has the lowest RMSE and highest R2 score.
- Based on the scores above, the better performing model would be the Linear regression model.

___Trial #2 - Swap Features___ </br>
Swap mrt_nearest_distance with Hawker_Nearest_Distance to identify impact on model. </br>

Numeric Feeatures:
- floor_area_sqft
- remaining_lease
- Hawker_Nearest_Distance (previously mrt_nearest_distance in Trial #1)
- max_floor_lvl

Categorical Features:
- town
- flat_type

***Key Findings***
- RMSE score for Trial #2 models is worse than those in Trial #1
- R2 score is lower for all models as compared to performance in Trial #1
- It can be concluded that mrt_nearest_distance is a better predictor than Hawker_Nearest_Distance.

___Trial #3 - Adding Features___ </br>
Include both mrt_nearest_distance and bus_stop_nearest_distance to determine impact on model. </br>

Numeric Feeatures:
- floor_area_sqft
- remaining_lease
- mrt_nearest_distance
- bus_stop_nearest_distance
- max_floor_lvl

Categorical Features:
- town
- flat_type

***Key Findings***
- Previously in Trial #2, it was concluded that models in Trial #1 performed better.
- The RMSE score for models in Trial #3 does not perform as well as those in Trial #1.
- Similarly, the R2 score is not as high as those in Trial #1.
- Models in Trial #1 still performs better than those in Trial #2 and #3.

___Trial #4 - Adding a Relationship___ </br>
Add a relationship feature for bus_stop_nearest_distance and mrt_nearest_distance to determine impact on model. </br>

Numeric Feeatures:
- floor_area_sqft
- remaining_lease
- mrt_nearest_distance
- bus_stop_nearest_distance
- mrt_bus_stop (relationship feature combining mrt_nearest_distance and bus_stop_nearest_distance)
- max_floor_lvl

Categorical Features:
- town
- flat_type

***Key Findings***
- The RMSE score for models in Trial #4 did not perform as well as those in Trial #1.
- Similarly, the R2 score is not as high as those in Trial #1.
- Models in Trial #1 still performs better than those in Trial #2, #3 and #4.

***Summary***
- Trial #1 produced the best model
- Linear Regression within Trial #1 was the best performing model

***Predictions***
The predicted scores were exported as `result.csv` and submitted to the kaggle competition for scoring.

***Result*** </br>
The model obtained a RMSE score of `57984.47091` compared to the baseline RMSE score of `142970.75311` (Please refer to images in `images` folder for both baseline and prediction scores).

## Conclusions and Recommendations
- HDB flats are well distributed across Singapore and new flat buyers have a plethora of options to choose from.
- Resale prices of HDB flats are continuously changing but tend to follow a similar trend with the exception of multi-generation flats which has strict purchasing criterias.
- Flat purchasers looking for HDB resale flats in Bukit Timah, Bishan and Bukit Merah can expect the purchasing price to be  on the steeper side. If they are price-concious, they can look at resale flats at Woodlands, Bukit Batok and Yishun.
- Beyond the towns where these resale flats are located, some of the key factors that influence the resale prices are floor area, max floor level and distance from common ammenities such as MRTs, bus stops, malls, primary schools  and secondary schools.

## Areas for Improvements
- Economical factors were not factored in and it would be interesting to include metrics such as consumer price indexes (CPI) and Personal Consumption Expenditure (PCE) as it might directly influence the buying and selling patterns.
- Having a side-by-side comparison of both BTO and resale flats in terms of their features (max floor level, floor area etc.) and selling price would be interesting to help future buyers weigh the pros and cons of purchasing either if waiting for a flat is the least of their concerns.