# Predicting New Locations For Texas Roadhouse Using Gradient Boosting and SHAP.

<h2>Introduction</h2>
This end-to-end machine learning project designed to predict new locations for the restaurant chain, with a focus on states currently growing in population, such as Colorado, Montana, Idaho, Utah, and South Carolina. <br>
<h5>Business Use Case:</h5>
Project can be expanded to new restaurants and other industries for use in predicting locations for new business. <br>
<h4>Tableau Public:</h4>

[Interact with the Texas Roadhouse Dashboard on Tableau Public](https://public.tableau.com/views/texasRoadhouseDashboard/Dashboard1?:language=en-US&publish=yes&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link)

<h4>PowerPoint Presentation:</h4> 

[Project Presentation](https://github.com/emilyschnepp/PredictingNewLocationsForTexasRoadhouse/blob/main/presentation/texasRoadhouse.pptx)



<h6>This project is not affiliated with Texas Roadhouse.</h6>

<h2>Prerequisites</h2>
<h4>Tableau Public</h4>
<h4>Python, with the following libraries:</h4> 
• Sklearn <br>
• shap <br>
• matplotlib <br>
• pandas <br>
• numpy <br>
• seaborn <br>
• imblearn <br>
• geopy <br>
• praw <br>
• math <br>
• statsmodels <br>
• requests <br>
• pgeocode <br>

<h2>Data Sources</h2> 
With respect to query limits and requests for lag times or breaks, the following APIs were used: <br>
<br>
•	Google Places API: Collected data on Texas Roadhouse locations, including ratings, total user reviews, and geographic coordinates. <br>
•	US Census API: Collected more than 40 variables of demographic data such as population, income levels, and housing statistics for cities with and without existing restaurant locations. <br>

Used the following additional resources: <br>
•	Census Gazetteer: Ensured accurate location mapping with FIPS codes. <br>

Ultimately, three comprehensive datasets were created: <br>

[trhCensusDf_updated](https://github.com/emilyschnepp/PredictingNewLocationsForTexasRoadhouse/blob/main/data/trhCensusDf_updated.csv) includes 598 Texas Roadhouse locations along with the Census data for the communities in which they are located. 

[updatedLocationResearch.csv](data/updatedLocationResearch.csv) has ~1500 potential sites to explore for new Texas Roadhouse locations across Utah, Colorado, Montana, Idaho and South Carolina.

[finalizedTRH.csv](https://github.com/emilyschnepp/PredictingNewLocationsForTexasRoadhouse/blob/main/data/finalizedTRH.csv) contains ~2100 rows and joins both updatedLocationResearch.csv and trhCensusDf_updated.csv. 

<br>
In total, the datasets contained over 50 variables from the Google Places and US Census APIs. <br>

Note: Geolocation data was sourced from SimpleMaps’ free US Zip Code database. <br>

<h2>How To Use</h2>
1.	Download files: download the .ipynb and associated .csv datasets. <br>
2.	Upload: Upload to Google Colab or your local Jupyter Notebook environment. <br>
3.	Run the Scripts: <br>
<br>

For exploratory data analysis use [this EDA script](https://github.com/emilyschnepp/PredictingNewLocationsForTexasRoadhouse/blob/main/scripts/trhEDA.ipynb) and datasets trhCensusDf_updated.csv.

For location prediction use: [this location prediction script](https://github.com/emilyschnepp/PredictingNewLocationsForTexasRoadhouse/blob/main/scripts/trhNewLocationPredictor.ipynb) and datasets trhCensusDf_updated.csv and updatedLocationResearch.csv.

<h2>Models</h2> 
• Baseline Model: Logistic Regression <br>
• Fine-Tuned Model: Gradient Boosting Classifier <br>
• Hyperparameter tuning was conducted on the fine-tuned models, using GridSearchCV. The winningest hyperparameters were reintegrated into the gradient boosting model to streamline the code. <br>

<h2>Features</h2> 
<h4>Features Engineered:</h4>
•	successMetric: Combination of user ratings and total ratings, weighted in favor of restaurants with a higher rating count. <br>
•	success: Binary, based on a successMetric above the 75th percentile. <br>
•	nearestDistanceToTRH: Designed to calculate distance between existing and potential locations and the next closest TRH location. <br>
•	IncomeRentRatio and povertyRatio: Percentages, designed to merge Census features. <br>
•	populationPenalty and distancePenalty: Initially predictions were in low population areas and very close to other Texas Roadhouse locations. These features were engineered to find restaurants further out, in cities with bigger populations. <br>

<h4>Top Features for Prediction:</h4>

[SHAP Feature Importance](visualizations/shapFeatureImportance.png) - Illustrates how features contribute to the model's predictions. <br>

[SHAP Force Plot](visualizations/shapForcePlot.png) - Illustrates how the features individually influence the model's probability of success. <br>

<h2>Data Preprocessing</h2> 
<h4>The following preprocessing steps were taken:</h4>
• Handled missing values <br>
• Normalized features <br>
• Balanced the dataset using BorderlineSMOTE to oversample the minority class. <br>

<h2>Metrics</h2>
<h4>Metrics Used:</h4> 
• Accuracy <br>
• Precision <br>
• Recall <br>
• F1 Score <br>
• AUC-ROC <br>

<h4>Results:</h4> 
• Logistic Regression Baseline: Accuracy: 0.4758, Precision: 0.4758, Recall: 1.00, F1 Score: 0.6448 <br>
• Gradient Boosting Fine-Tuned Model: Accuracy: 0.8290, Precision: 0.8015, Recall: 0.8516, F1 Score: 0.8258, AUC = 0.8856 <br>
• While the logistic regression model baseline model performed rather poorly, the fine-tuned gradient boosting model was able to achieve solid metrics. <br>
• The average cross validation F1 score is 0.8307 with moderately stable performance across all folds. <br>

<h2>Visualizations</h2> 
<h4>Tableau - Interactive Dashboard:</h4> 
•	Line graph showing a distribution of restaurant ratings, with an annotation at the peak, with 230 restaurants maintaining a rating of 4.4. <br>
•	Geographic maps depicting success probabilities and restaurant ratings. <br>
•	Scatterplot showing restaurant success vs median household income and age. <br>
•	Bar chart of top recommendations for restaurant locations. <br>
•	Filters applied to the dashboard allow the user to specify desired success probabilities and ratings. <br>
•	The color scheme makes use of green for existing restaurants and brown or red for potential locations. <br>

<h4>EDA Visuals with Python:</h4> 
•	Scatter plot of ratings by location. <br>
•	Bar chart of top 10 ratings by city. <br>
•	Interactive map of business density with success metrics. <br>

<h4>Model Visuals with Python:</h4> 
•	SHAP summary plot and force plot for feature explainability. <br>
•	Feature importance bar chart <br>
•	Confusion matrix and ROC curve for evaluation. <br>

<h2>Findings</h2> 
<h4>Top Recommended Locations:</h4>
• Great Falls, MT (0.9603 success probability) 
• Salt Lake City, UT (0.9839 success probability)
Other recommended locations included Billings, MT, Coeur d’Alene, ID, and Meridian, ID. These locations already have Texas Roadhouse restaurants but were recommended despite the implemented distance penalty. This may indicate potential for an additional location in a neighboring area. 
<h4>Additional Insights</h4>
• The data suggests a positive correlation between restaurant ratings and income up to 60K. At 60K that peaks, and then there seems to be a negative correlation as income increases. Restaurants with the highest ratings are in areas with a median age in the early to mid-30s. <br>
• The SHAP Force Plot illustrates how features impact success probability. Median home value was found to increase the success probability. Income rent ratio, and stateFIPS were found to contribute negatively to the success probability. <br>
• The SHAP visualization breaks down how each feature impacts the success probability for a specific prediction. Features pushing the prediction higher are shown in blue, while those lowering it are in red. <br>

<h2>Future Work</h2> 
•	Incorporate missing Texas Roadhouse locations for comprehensive analysis. <br>
•	Add population growth trends and financial data for robust predictions. <br>
•	Refine models to better handle edge cases (e.g., low-population areas). <br>
•	Engineer new features like pop growth rates or competitor features. <br>
•	Consider expanding to additional states. <br>
•	Recalibrate penalties for proximity to existing locations. <br>

<h2>Limitations</h2>
This project is proof-of-concept, but it is not without its limitations. <br>
•	The new restaurant location selection process most probably involves variables from internal sales data that one could not reasonably expect to be available for this project. <br>
•	While a distance penalty was implemented and fine-tuned, getting recommendations in cities where there are already restaurants indicates room for further refinement. <br>
•	Some existing Texas Roadhouse locations were dropped from the analysis because the census data could not be acquired or was faulty. Furthermore, multiple sources reported varying numbers of locations. <br>
