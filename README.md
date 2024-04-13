# Predictive Analytics Insights for HDB Resale Trends

<div id="top"></div>

<!-- PROJECT SHIELDS -->
<!--
*** I'm using markdown "reference style" links for readability.
*** Reference links are enclosed in brackets [ ] instead of parentheses ( ).
*** See the bottom of this document for the declaration of the reference variables
*** for contributors-url, forks-url, etc. This is an optional, concise syntax you may use.
*** https://www.markdownguide.org/basic-syntax/#reference-style-links
-->

<!-- PROJECT LOGO -->
<br />

<h2 align="center">HDB Resale</h2>

  <p align="center">
    Singapore
    <br />
  </p>
</div>

<!-- ABOUT THE PROJECT -->

## About The Project

<p> 
This study encompasses a comprehensive exploration of HDB resale price prediction that integrates exploratory data analysis (EDA), machine learning (ML) modelling to generate actionable insights for real estate decision making. HDB resale flats play a vital role in Singapore’s housing landscape, but their fluctuating prices have the potential to create uncertainty amongst the buyers and sellers. The complexity of pricing factors such as location, distance to MRT and amenities around the flat can overwhelm potential stakeholders easily. This study aims to simplify the complexity by identifying the most important features and evaluating their impact on resale prices in order to provide the relevant stakeholders a more effective means to predict resale prices to make a more informed decision.
</p>

<p align="right">(<a href="#top">back to top</a>)</p>

<br />

## Instructions to Run

### Directories
Create a dataset folder to store the following data files.
- `hdb_latest_raw.csv` [HDB Dataset with MRT](https://www.kaggle.com/datasets/chngyuanlongrandy/hdb-prices-with-closest-mrt-distance/data)
- `points_of_interest.csv` [LTSG POI Dataset](https://sites.google.com/view/ltsg)

<br />

### Packages
Install the relevant packages when prompted.

<br />

### Data Blending

#### 1. Run the Data Blending Notebook to merge HDB and POI Datasets

<p> 
HDB Resale dataset is filtered to the most recent 15-year period of HDB sales that contains recent trends in resale prices and Points of Interest dataset that provides a snapshot of the surrounding amenities and facilities (i.e. Healthcare, Education, Recreation) available around HDBs to understand the lifestyle and convenience associated with living in a particular area.
</p>

<br />

### Exploratory Data Analysis (EDA)

#### 2. Run the EDA Notebook 

<p> 
To further understand how these can impact the resale price, an in-depth EDA is carried out consisting of outlier analysis and correlation analysis to uncover the relationships between the variables.
</p>

<br />

### Price Prediction

#### 3. Run the Price Prediction Notebook 

<p> 
Data preprocessing techniques are employed to clean and prepare the data to be used for ML modelling. Feature Engineering techniques like One-Hot Encoding was used to convert categorical variables into numerical variables coupled with Feature Selection methods such as Variance Threshold to reduce the dimensionality and computational complexity while retaining only the more informative features for modelling. This also mitigates the issue of overfitting. In addition, highly correlated features were removed to reduce the impact of multicollinearity that may result in biassed results which in turn may affect our subsequent model performance and interpretability. 

With the cleaned dataset, ML modelling is carried in two stages, Baseline Modelling and Advanced Modelling. As the prediction of HDB resale prices is a supervised regression task, the modelling process is evaluated based on certain regression metrics such as Mean Absolute Error (MAE), Mean Absolute Percentage Error (MAPE), Mean Squared Error (MSE), Root Mean Squared Error (RMSE) and R2 (Coefficient of Determination). Baseline modelling includes the use of Linear Regression (LR) and Decision Tree Regressor (DTR) models to uncover linear and non-linear relationships in the data respectively. Given DTR outperforms LR as it has a greater R-Squared value of 0.99971 > 0.97155 and a lower RMSE of 2504 < 24828, DTR has been chosen as our baseline model to look into more complex Ensemble models for better performance. The most important feature in that model is "healthcare_within_1km_count" after hyperparameter tuning. For Advanced modelling, bagging methods like Random Forest Regressor (RFR) and boosting methods like XGBoost (XGB) were selected to improve on our baseline model. XGB did not perform as well as baseline DTR with a lower MAE, RMSE and R-Squared whereas RFR outperforms baseline DTR with the highest coefficient of determination of 0.99982, the lowest RMSE of 1973 and the lowest MAE of 250.03. The most important feature in this model was "remaining_lease", which is ranked 2nd amongst numerical attributes in correlation coefficient significance supported from correlation analysis. As RFR is the best performing model, we will be using RFR for the future predictions of HDB Resale Prices.
</p>

<br />

### Case Study

#### 4. Run the Case Study Notebook

<p> 
This case study aims to enhance the comprehension and relatability of our findings regarding the factors influencing resale prices and our model. To achieve this objective, we will present an example — a real resale HDB flat. Specifically, we will visually portray the flat within its geographical context to unveil the influence of its features, such as location and nearby amenities, on its resale price.

To assess the impact of a flat's geographical context on its resale price, we narrow down the dataset based on performance in POI-related measures. After experimentation, we find that the most comprehensive combination of POI-measures, where HDB flats perform above the 75th percentile across all measures, includes:
- Average healthcare POI rating within 2km
- Average healthcare POI rating within 1km
- Average education POI rating within 2km
- Average education POI rating within 1km
- Number of recreational POIs within 2km
- Average recreation POI rating within 2km

Using this combination, we shortlist 25 flats for the case study. Considering another geographical factor, proximity to the nearest MRT, we filter to 20 flats, selecting only those below the 25th percentile in terms of distance.

Further refinement identifies 3 flats with poor performance across:
- Floor area in square metres (below 75th percentile)
- Remaining lease (below 50th percentile)

From these, we prioritise the flat with the lowest storey range, reflecting the general preference for higher storey flats in Singapore. This approach emphasises the influence of a flat's geographical context on its resale price by focusing on those performing poorly in non-POI related metrics.

The map of the target flat with its associated POIs within a 2km radius can be seen in `hdb_map.html`. The selected HDB unit can be identified by the red marker, while the Healthcare POIs are indicated by the blue markers, the education POIs by the green markers and the recreational POIs by the orange markers. There are around 12-15 of each POI located within the 2km radius of the selected HDB unit.

</p>

<p align="right">(<a href="#top">back to top</a>)</p>

<br />
