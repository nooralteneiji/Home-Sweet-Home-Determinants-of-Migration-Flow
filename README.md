```diff
- account for people irrationally scoring their happiness
```

# Dataset 
[World Happiness Report](https://worldhappiness.report/archive/)
- `country`: The name of the country for which the happiness data is reported.
- `year`: The year in which the happiness data is recorded.
- `GDP`: Gross Domestic Product per capita, which measures the economic output per person in a country.
- `socialSupport`: The level of social support and the presence of a support network in a person's life.
- `lifeExpectancy`: The average number of years a person is expected to live in good health, capturing the overall health and well-being of individuals in a country.
- `freedom`: The degree of political and social freedoms enjoyed by individuals in a country.
- `generosity`: The measure of generosity, including charitable donations and helping others, in a country.
- `corruption`: The perceived level of corruption and trustworthiness within the public sector of a country.
- 'happiness'

  

[dataset](https://figshare.com/collections/Bilateral_international_migration_flow_estimates_for_200_countries/4470464)
- Provides an estimation of bi-lateral flow of migration, not captured by standard migration datasets (i.e., [Our World In Data](https://ourworldindata.org/migration)).

[csv from github](https://github.com/null2/globalmigration/blob/master/Data%20on%20the%20global%20flow%20of%20people_Version%20March2014.csv)

`year`, `origin`, `destination`, `type` (outward, return, transit)

Outward migrants move away from their country of birth. 

Return migrants move to their country of birth. 

Transit migrants move from and to countries, neither of which is their country of birth.

3 different estimations of migration flow are in the columns: 
- `da_min_open`(demographic accounting, open minimization method)
- `da_min_closed` (demographic accounting, closed minimization method)
- `da_pb_closed` (demographic accounting, pseudo baysian method)
   - We will only this estimation since [Abel and Cohen, 2019](https://www.nature.com/articles/s41597-022-01271-z)(https://www.nature.com/articles/s41597-019-0089-3) found the Pseudo-Bayesian demographic accounting method to be the best estimation of migration flow from migrant stock data (how many migrants are residing in a country during a specific point in time) published by the World Bank and United Nations.

region_orig	region_orig_id	region_dest	region_dest_id	country_orig	country_dest	regionflow_1990	regionflow_1995	regionflow_2000	regionflow_2005	countryflow_1990	countryflow_1995	countryflow_2000	countryflow_2005

**Why was this dataset was choosen and not UN/World Bank data?**
- Widely available data on the number of people living outside of their country of birth do not adequately capture contemporary intensities and patterns of global migration flows[(Abel and Sanders, 2014)](https://www.science.org/doi/full/10.1126/science.1248676?ijkey=ypit4%2Fxi7wo4M&siteid=sci&keytype=ref).
- Stock data, measured at a given point in time as the number of people living in a country other than the one in which they were born, are more widely available and far easier to measure across countries than are flow data capturing movements over a period of time [(Abel and Sanders, 2014)](https://www.science.org/doi/full/10.1126/science.1248676?ijkey=ypit4%2Fxi7wo4M&siteid=sci&keytype=ref).
- However, flow data are essential for understanding contemporary trends in international migration and for determining relationships.
      - They used an innovative methodology to estimate bilateral flows between 196 countries from 1990 through 2010. The estimates reflect migration transitions and thus cannot be compared to annual movements flow data published by United Nations and Eurostat 2. The authors used statistical missing data methods to estimate the five-year migrant flows that are required to meet differences in migrant stock totals. For example, if the number of foreign-born in the United States increases between two time periods, they estimated the minimum migrant flows between the US and all other countries in the world that are required to meet this increase. For each country of birth, they estimated the minimum number of migrant flows required to match differences in stocks by assuming that people are more likely to stay than to move. This estimation procedure was replicated simultaneously for all 196 countries to estimate birthplace specific flow tables, resulting in a comparable set of global migration flows 3.


[UCDP Georeferenced Event Dataset](https://ucdp.uu.se/downloads/index.html#ged_global)

*Countries with less immigrants, more genetically pure?*




[climate dataset](https://resourcewatch.org/data/explore/cli029a-Vulnerability-to-Climate-Change-Index?section=Discover&selectedCollection=&zoom=3&lat=0&lng=0&pitch=0&bearing=0&basemap=dark&labels=light&layers=%255B%257B%2522dataset%2522%253A%25224d2d47c1-fed1-4484-83e3-c91c3f6f7315%2522%252C%2522opacity%2522%253A1%252C%2522layer%2522%253A%25226c2a0892-87e7-41ef-b4f0-e53c89baab5c%2522%257D%255D&aoi=&page=1&sort=most-viewed&sortDirection=-1)
[index variable descr](https://gain.nd.edu/assets/254377/nd_gain_technical_document_2015.pdf)



---


# Overview of Research Questions
**(1) Trends in Migration:**
Let us set the stage by providing a broad understanding of how migration patterns and happiness scores have shifted over time. Recognizing the trends at a macro level can form the foundation for more specific exploration later on.
   - How have migration patterns changed over time in relation to shifts in the happiness scores of both source and destination countries?
    
    
**(2) Trends in Migration and Country Characteristics**

**(3) What are the predictors of migration?**
- What influences the decision to migrate?    
    
  **Environmental Indicators and Climate Migration:**
With the increasing urgency of climate change, environmental factors become crucial. Delving into data about climate vulnerability, environmental degradation, and resource depletion in both source and target countries might elucidate a new dimension of migration. This could establish a narrative around "climate migrants" or "environmental refugees."


**looking at Digital and Technological Footprints** variables such as internet freedom, digital infrastructure quality, and tech ecosystem vitality can be migration determinants, especially for the young, urban, and skilled demographic.


---

# Q1: What are the migration patterns?

## Trend analysis 
### Check distribution 
Before seeing if there is a statistically significant difference between the the migration types, we need to see if data normally distributed. This step is important as it will inform us which type of non-parametric test to use.

As we can see, migration data is skewed to the left. 

![distribution migration](https://github.com/nooralteneiji/Happiness-Without-Borders/blob/main/Outputs/Figures/q1_distributionMigration.png)


### Check if significant deifferences between migration type 
Since we do not have a normal distribution and we want to test more than two groups, we will use a Kruskal-Wallis Test.

We do not need to do a test between the migration types and happiness scores since comparing them would not be meaningful.

We will compare the differences in migration weights for each pair of migration types (e.g., 'inwards' vs. 'outwards', 'inwards' vs. 'transit', 'outwards' vs. 'transit') and the differences in happiness scores between 'transit' and 'happiness_source' for each year separately.

The null hypothesis for the Kruskal-Wallis test is that the distributions of the two groups being compared are identical, while the null hypothesis for the Wilcoxon signed-rank test is that there is no difference between the paired samples. If the p-value is less than the significance level (<0.05), it indicates a statistically significant difference between the groups.

Based on the low p-values we reject the null hypothesis for all tests, indicating that there is a statistically significant difference in migration weights between each pair of migration types for each year. This means that the migration weights are not coming from the same distribution for all pairs of migration types and there are significant differences between them.


### Line graph: Viusalize migration trends as a function of time

![globaltrend](https://github.com/nooralteneiji/Happiness-Without-Borders/blob/main/Outputs/Figures/q1_globalTrend.png)

The plot shows the trends and implications of migration weight and happiness over the years 2005, 2010, and 2015. The data is presented using two y-axes, with migration weight (transit_mean, return_mean, and outward_mean) represented on the left y-axis and happiness (happiness_source_mean and happiness_target_mean) represented on the right y-axis.

Trends for Migration Weight:
- Outward migration most popular.
- Transit Mean: This represents the average migration over the years between two countries which individuals are not originally. It shows a decreasing trend from around 1421 in 2005 to about 534 in 2010 and then slightly increasing to approximately 559 in 2015.

- Return Mean: This represents the average return migration weight over the years. It starts at around 4308 in 2005, decreases to approximately 3687 in 2010, and then continues to decline to about 3104 in 2015.

- Outward Mean: This represents the average outward migration weight over the years. It starts at approximately 9571 in 2005, decreases to around 7902 in 2010, and then further declines to about 7174 in 2015.

Implications:
The decreasing trends in transit mean, return mean, and outward mean migration weight indicate that there might have been changes in migration patterns over the years. The decrease in transit migration weight suggests a reduction in the number of people migrating between two countries which they are not originally from. Similarly, the decline in return and outward migration weights indicates a possible decrease in the number of people returning to their home countries or leaving their home countries, respectively.


### Which countries are people migrating to? [REMOVE INSIGNIFICANT COUNTRIES W OVERLAPPING LABELS]

**WE ARE ONLY LOOKING AT countries that send and recieve at least 0.5% of world's migrants**

*The chord graph code was written based on this [source](https://holoviews.org/reference/elements/bokeh/Chord.html).*

**Overall routes**

![chord_country](https://github.com/nooralteneiji/Happiness-Without-Borders/blob/main/Outputs/Figures/Q1_chord_diagram_countryRoute.png)


!!!!!!!!!!!!!! show flow between top 50 countries that send and recieve at least 0.5% of world's migrants!!!!!!!!!!!

**Which countries are most people migrating to?**

*HOW TO READ THE GRAPH: Look at the largest nodes. They represent the destination country, so all chords coming from other countries indicate where the people are migrating from to reach the destination country.*

People are migrating to the UK, US, UAE, Canada, Austrailia, Germany, Russia, Saudia Arabia, Italy and Spain.

![country toward](https://github.com/nooralteneiji/Happiness-Without-Borders/blob/main/Outputs/Figures/q1_chord_diagram_topCountryToward.png)

**Which countries are most people migrating away from?**

*HOW TO READ THE GRAPH:Look at the largest nodes. They represent  the country of origin, so all chords coming from other countries indicate where the people are migrating towards*

People are migrating away from Mexico, India, China, Bangladesh, Pakistan, Russia, Saudia Arabia, Syria, US, UK, Germany.

![country away](https://github.com/nooralteneiji/Happiness-Without-Borders/blob/main/Outputs/Figures/Q1_chord_diagram_topCountryAway.png)

### Which regions are people migrating away from? 

*HOW TO READ THE GRAPH: Look at the largest nodes. They represent the country of origin, so all chords coming from other countries indicate where the people are migrating towards*

![region](https://github.com/nooralteneiji/Happiness-Without-Borders/blob/main/Outputs/Figures/chord_diagram_Region.png)  

### Which sub-regions are people migrating away from? 

*HOW TO READ THE GRAPH: Look at the largest nodes. They represent the country of origin, so all chords coming from other countries indicate where the people are migrating towards*

![chord_subregion](https://github.com/nooralteneiji/Happiness-Without-Borders/blob/main/Outputs/Figures/chord_diagram_subRegion.png)


# Q2: What are the migration patterns with respect to country qualities?


## Are people migrating to better countries?

A handful of countries in the African continent expirence a better happiness score once they migrate and arrive at the destination country.

![world heatmap](https://github.com/nooralteneiji/Happiness-Without-Borders/blob/main/Outputs/Figures/Q2_WorldHappinessMap.png)


### Migrating to happier countries? 

**Movinge to happier country?**

![happier](https://github.com/nooralteneiji/Happiness-Without-Borders/blob/main/Outputs/Figures/Q2_chord_diagram_happier.png)

**Movinge to less happy country?**

![less happy](https://github.com/nooralteneiji/Happiness-Without-Borders/blob/main/Outputs/Figures/Q2_chord_diagram_lessHappy.png)


### Migrating to better GDP?!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!

### Migrating to better life expectancy?!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!

### Migrating to less corruption?!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!

### Migrating to more freedom?!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!

### Migrating to less attacks?!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!

---

# Q3: Decoding the decision to migrate
Migration is a multifaceted phenomenon driven by a combination of economic, social, political, and environmental factors. The decision to migrate can be based on push factors (negative conditions encouraging or forcing individuals to leave a place) and pull factors (attractive conditions luring individuals to a new place).

We want to predict the percentage_weight of migration between countries.

The factors we will examine as drivers of migration:

- Economic Factors (GDP)
- Social Factors (social support)
- Quality of Life Factors (happiness, life expectancy)
- Political or Civic Freedoms (perception of corruption, freedom)
- Cultural or Social Values (generosity)
- Violence (number of violence events)    

1. **Factors from Dataset**:
    - **Push Factors**: Factors that may influence someone's decision to leave their home country.
        - `GDP_source`
        - `socialSupport_source`
        - `happiness_source`
        - `lifeExpectancy_source`
        - `corruption_source`
        - `freedom_source`
        - `generosity_source`
        - `source_total_violence`
        
    - **Pull Factors**: Factors that may attract someone to a new country.
        - `happiness_target`
        - `GDP_target`
        - `socialSupport_target`
        - `lifeExpectancy_target`
        - `freedom_target`
        - `generosity_target`
        - `corruption_target`
        - `target_total_violence`
    
    - **Differential Factors**: Comparing conditions between the source and target countries.
        - `happiness_difference`
        - `GDP_difference`
        - `socialSupport_difference`
        - `lifeExpectancy_difference`
        - `freedom_difference`
        - `generosity_difference`
        - `corruption_difference`
    
2. **Control Variables**:
    - These are variables that might affect the outcome (migration) but are not of primary interest. They can account for potential confounders or other variables that might distort the relationship between the main independent variables and the dependent variable (migration).
        - `year`: Temporal factors can influence migration.
        - `source`: Country-specific effects, such as policies, can be influential.
        - `sourceRegion` & `sourceSubRegion`: Regional factors, like regional economic policies or regional conflicts, might play a role.
        - `target`, `targetRegion`, & `targetSubRegion`: Migration might be influenced by the specificities of target places, such as their immigration policies or socio-cultural attitudes towards immigrants.
        - `percentage_weight`, `weight`, and `total_weight`: These may capture the intensity or magnitude of migration. They might be your dependent variables, unless you have a different metric for migration.

## Method 

**Random forest**: We are essentially creating multiple decision trees, where each tree gets a different subset of the data (via bootstrapping) and different pair of features. The decisons from all the trees will be taken in aggregate to create the prediction.

**Why?** Was proven to have second highest accuracy when compared to other supervised machine learning models [(Kaur et al., 2019)](https://www.mdpi.com/2076-3417/9/8/1613).


### Data Preprocessing
   
   - **Encode Categorical Variables**: RF can handle categorical data, but scikit-learn prefers numerical data. So, from our dataframe `violenceHappinessMigration_df`, we will encode:
      - `source`
      - `sourceRegion`
      - `sourceSubRegion`
      - `target`
      - `targetRegion`
      - `targetSubRegion`
      - `happiness_category` (ordinal encoding since it has a ranking)
      
   - **Handle Missing Data**: Ensure that there's no missing data. 

   - **Feature Scaling**:  RF isn't as sensitive to different scales (unlike SVM), and we do not plan to use other algorithms for comparison--so we will skip this step.
   
   - **Split into X and y**: We are trying to understand the relative impact of migration and want to compare across countries/regions of different sizes, so we will use `percentage_weight` rather than `weight`. This is becuase it accounts for the size of the population, making it possible to compare migration rates between large and small countries/regions on an equal footing. Additionally, it can give a clearer picture of the actual impact or significance of migration relative to the source population.
   
   - **Split into training and test set**: where 30% of the data is reserved for testing, and the rest (70%) is used for training.

### Hyperparameter Tuning

   - We used Grid Search with Cross-Validation to find optimal hyperparameters (e.g., number of trees, max depth of trees, min samples split).

MSE = `0.0336`.

This is a measure of the average squared difference between the actual target values (y_test) and the predicted values (y_pred) obtained from the RandomForestRegressor model.

In this case, the MSE value of 0.0336 indicates that the model has reasonably accurate predictions on the test set, with small errors in its predictions compared to the actual target values.


### Model Training and Validation

   - **K-Fold Cross Validation**: Implemented 10-fold validation to ensure that our model's performance is consistent across different partitions of your data.
   
   While Random Forests inherently utilize bootstrapping, it's essential to remember that this only offers an internal validation. On the other hand, the external k-fold cross-validation sheds light on different aspects of model performance.

**How 10-fold cross-validation works:** We split the training dataset into 10 equal "folds." During each of the 10 iterations, we train the model using 9 folds and validate it using the remaining fold. This way, every fold gets its turn as a validation set, enabling us to assess the model's performance across diverse data subsets.

So, why do go out of our way to add this approach?

- **Performance Insight**: With this method, we receive an array of performance metrics, in our case, ten distinct MSE values. The spread of these scores, captured by `std_mse`, offers a glance into the model's consistency. A low standard deviation suggests stability across varied data partitions, while a high one indicates potential inconsistencies.

- **Optimal Data Use**: Unlike the typical train-test split approach, where some data might remain untouched, k-fold cross-validation ensures we're both training and validating across the entire dataset.

- **Balancing Bias and Variance**: The spread of performance metrics across folds can hint at the model's sensitivity to specific data nuances.

- **A Check Against Overfitting**: While Random Forests have built-in mechanisms against overfitting, they aren't foolproof. Cross-validation aids in spotting signs of overfitting. A high variance in performance across folds might be a red flag.

- **Gauging Generalization**: By averaging performance over multiple data subsets, we gain a more trustworthy perspective on how well the model might perform on unseen data.

- **Harmonizing with GridSearchCV**: Remember our earlier GridSearchCV step? It also banked on cross-validation. Keeping the evaluation method consistent ensures we're comparing apples to apples.

In a nutshell, 10-fold cross-validation is our way of diving deeper into the model's performance, giving us a richer and more nuanced understanding than a simple train-test split would."

10-Fold Cross-Validation MSE:`0.0428 (+/- 0.0066)`

This score is the average of the MSEs from each of the 10 different train-test splits in the k-fold cross-validation. The variability (+/- 0.0066) gives an indication of the consistency of the model performance across different splits.

This average MSE provides a more generalized assessment of the model's performance. The variability indicates how much the performance might change based on different data splits.

   
### Model Performance
   

Overview of the model's performance:

MAE = `0.106`
- takes into account error magnitude 

- on average, the model's predictions are off by approximately 14.28% from the true values. In other words, the model is, on average, about 0.1428 units away from the true value.

MSE = `0.0339`
- variance of errors 
-  It penalizes larger errors more severely than smaller ones, meaning it's more sensitive to outliers than the MAE.

- our MSE value suggests that our model does a good job of fitting the data, as the value is relatively low.

- This is the MSE calculated after training the model on the entire training set and then testing it on a separate, held-out test set (the one we created with train_test_split).
- This score gives an indication of how the model, trained on the entire training dataset, performs on unseen data.
- previously we found the average of the MSEs from each of the 10 different train-test splits in the k-fold cross-validation.
    - The slight difference between these two MSE values is due to the variability inherent in the dataset and the training process. The fact that the two values are relatively close suggests that our model's performance is consistent and that it generalizes well to new data. The cross-validation MSE gives you a range of likely performances, and the test set MSE falls comfortably within this range, which is a good sign.

R^2 = `0.987`
- proportion of the total variation in the dependent variable that's explained by the independent variables 
- ranges from 0 to 1, where higher values are better, indicating that more variance is explained by the model.

- approximately 98.7% of the variability in the percentage_weight is explained by the model. This suggests that the model captures most of the variance in the data.
- **!!However!!**  with such high R^2 values we need to be cautious becuase it could be a sign of overfitting.
    - Given that we used k-fold cross-validation earlier, the risk is somewhat mitigated.

The Random Forest model has shown a very high R^2 score and relatively low error metrics, indicating that it performs well on the test set. The high R^2 score suggests that the features we have selected are very predictive of migration patterns (AKA percentage_weight). 

### Model Interpretation

#### Feature Importance

RF allows us to extract feature importance which tells us which variables are most influential in making predictions.
   
![feature importance](https://github.com/nooralteneiji/Happiness-Without-Borders/blob/main/Outputs/Figures/q3_featureImportances.png)
   
This highlights the most influential factors in determining the migration patterns (as measured by `percentage_weight`).
   
##### Observations:

1. **Country-Specific Influences**: 
    - **Source Countries**: The model indicates that the source countries, specifically `source_Pakistan`, `source_India`, `source_Bangladesh`, `source_China`, and `source_Saudi Arabia`, are amongst the most important features in predicting migration patterns (`percentage_weight`).
    - **Target Countries**: Similarly, target countries like `target_Germany`, `target_India`, and `target_Bahrain` play significant roles.
    - These findings suggest that specific countries play a pivotal role in influencing global migration patterns.

2. **Economic & Societal Metrics**: 
    - Features like `GDP_source`, `lifeExpectancy_source`, and `happiness_source` are high up on the list, emphasizing the role of economic and societal well-being metrics in influencing migration decisions.

3. **Implicit Interactions and Patterns**: 
    - Some features like `source_Pakistan` and `source_India` have higher importances than general metrics like `GDP_source`. This suggests that there might be country-specific factors, beyond just GDP or happiness, influencing migration. 
    - There might be political, social, or environmental factors at play in these countries that drive migration.

4. **Climate & Environmental Considerations**: 
    - The presence of `target_climateIndex` and `source_climateIndex` indicates that environmental considerations might be playing a role in migration decisions. This could hint at factors such as climate change, environmental degradation, or natural disasters impacting migration patterns.
    
    
**What does it mean for the model to indicate that `source_Pakistan` is the most important predictor?**

The model is suggesting that the fact that a person is migrating from Pakistan is a strong indicator for the outcome variable, `percentage_weight`, at least within the scope of this model specifically. 

1. Relevance of `source_Pakistan`: If `source_Pakistan` emerges as one of the most influential predictors, it underscores that there are significant migration patterns (or weights) emanating from Pakistan. This could be due to a multitude of reasons: economic factors, societal unrest, geopolitical tensions, environmental challenges, or a combination of these and other factors.

2. Comparing to `GDP_difference`: The fact that `source_Pakistan` has a higher feature importance than `GDP_difference` suggests that the specific migration dynamics related to Pakistan might be more telling than the economic disparities (as measured by GDP differences) between source and target countries. It could imply:

   - Economic Factors: Even if the GDP difference between Pakistan and another country isn't vast, other intrinsic factors within Pakistan might be compelling its citizens to migrate. These factors could be unemployment rates, wage disparities, or local economic downturns that aren't fully captured by just looking at GDP.
   
   - Beyond Economics: Migration isn't solely driven by economic reasons. Political instability, religious or ethnic tensions, environmental factors, or educational opportunities can be substantial motivators. If the migration from Pakistan is more predictive than the GDP difference, it suggests that non-economic factors might be at play prominently in the case of Pakistan.

3. Holistic Interpretation: While `source_Pakistan` is highly predictive, it's crucial not to discount the role of other variables. For instance, `GDP_difference` might still play a significant role in migration patterns from other countries. Each predictor captures a unique facet of the broader migration landscape, and their collective interplay shapes the overall dynamics.


##### Link to Research Question:

**Factors Influencing Migration**: 
   - From the feature importance, it's clear that both source and target countries significantly influence migration decisions. Specific countries are highlighted, which means for a deeper understanding, you might need to investigate country-specific dynamics further.
   - Economic, societal, and environmental metrics play a crucial role in decision-making.

##### Implications:

1. **Geo-political Undertones and Migration Dynamics**:
    - **Emerging Economies and Migration**: The elevated significance of countries such as `source_Pakistan`, `source_India`, and `source_Bangladesh` may resonate with the broader political narrative of South Asia. The socio-political unrest, combined with the burgeoning youth population and economic constraints, might be catalyzing migration waves.
    - **Traditional Destinations**: The prominence of `target_Germany` underscores the traditional allure of Western Europe as a bastion of stability and economic opportunity. On the other hand, `target_Bahrain` suggests the continuation of the Gulf countries' role as sought-after destinations for labor migrants, particularly from South Asia.

2. **Economic Disparities and Societal Tensions**:
    - While GDP is often touted as a primary factor for migration, the relative significance of `GDP_source` juxtaposed against `happiness_source` and `lifeExpectancy_source` reflects a nuanced tapestry of migration. It underscores that migration is not just an economic decision but is profoundly intertwined with societal well-being and broader life satisfaction metrics.

3. **The Silent Narratives Beyond Macro Metrics**:
    - The disproportionate weightage of specific source countries, even over overarching economic indicators like `GDP_source`, is revelatory. It hints at deeper, often unspoken or under-represented narratives. For instance, the role of political instability, regional tensions, or societal fractures in countries like Pakistan and India might be overshadowing purely economic considerations.

4. **Environmental Factors and the New Migration Paradigm**: 
    - The emphasis on `target_climateIndex` and `source_climateIndex` is evocative of the emerging global narrative around climate-induced migration. It paints a picture of a world where environmental considerations, from degrading ecosystems to more immediate natural calamities, are becoming as central to migration decisions as traditional economic or political factors. The confluence of climate change and its socio-political repercussions cannot be understated in this new migration dynamic.   
   
#### Interaction Between Variables

   - Interactions between variables can be further explored. For example, why do certain source countries have higher importance than others? Is there an interaction between GDP, life expectancy, and specific countries?
   - The role of the climate index in both source and target countries needs further scrutiny. Is environmental migration becoming more prominent?
   
While RF doesn't explicitly give interaction terms like linear regression, high feature importance scores can sometimes hint at interactions. Further, partial dependence plots help visualize the relationship between the target and a set of features, and potentially highlight interactions.

Specifcally, Partial Dependence Plots (PDPs) can show the relationship between a feature and the target. We will look at the features with highest importance to show how migration weight changes with variations in a particular feature while keeping all other features fixed. 

![PPD plot](https://github.com/nooralteneiji/Happiness-Without-Borders/blob/main/Outputs/Figures/Figures/q3_PPD.png)

  
#### Tree Visualization
Although visualizing all trees might be overwhelming, we will visualize some individual trees to understand the decision-making process.
   
   
#### Plotting Predictions vs. Actuals
This can give us insights into where our model might be under or over-predicting.
   
#### Error Distribution
Plotting residuals or errors to diagnose model issues.
   
   
   
   
### Analyze Areas of Poor Performance

   - **Clusters of Poor Predictions**: We will look at clusters where model predictions fail. This will be done by analyzing the residuals (difference between actual and predicted values) and clustering them, for example, using k-means or DBSCAN.
   
   - **Explore Clusters**: After identifying clusters with poor predictive power, we explore these clusters to see if there's a commonality among them. Perhaps there's a specific region or time period where the model struggles. We will use exploratory data analysis techniques, like distributions, scatter plots, and summary statistics.
    - Cluster the data based on residuals (e.g., using K-means clustering).
    - Analyze the characteristics of each cluster. Are there common features in these mis-predicted instances?
    - We will use SHAP (SHapley Additive exPlanations) or LIME (Local Interpretable Model-agnostic Explanations) to understand why the model made certain predictions.

Implementing this methodology will give us a thorough analysis of our dataset using Random Forest. We will have a well-tuned model, insights into the most important features and their interactions, and a deep understanding of where the model performs well and where it struggles.

# Concluding thoughts 

The data-driven findings, offer profound insights into the complex web of international migration. It's an interaction between economics, societal well-being, geopolitics, and now, environmental considerations. Migration, as this study suggests, is far from a monolithic phenomenon; it's a reflection of a world in flux, constantly reshaped by a plethora of forces, both overt and covert.


# limitations 
- Selection Bias: Migrants are a selective group, and the decision to move to a particular country may be influenced by factors that are difficult to capture in the data. For example, individuals who are more optimistic or have higher adaptability may be more likely to migrate, which can bias the results.
- Confounding Variables: There are likely to be other variables that influence both migration decisions and happiness levels. For example, cultural factors, language, job opportunities, family support, and personal characteristics can all impact both migration choices and happiness.
- Cultural Magnetism and Soft Power: Beyond the palpable economic and political indicators, the cultural allure of a destination can be a significant pull factor. This encompasses facets like art, cinema, literature, music, fashion, and even academic or entrepreneurial ecosystems. The soft power a country wields could make it a preferred destination for migration.
- Violence dataset is not city specific, but it implies that the whole country is expirencing violence. More granular data is availble from the same dataset, but the happiness and mirgation data do not have the level of unit of anlaysis, hence we could not use it.
- Missing countries in Internet dataset

# Future directions 
- Is there a correlation between a nation's average happiness score and the genetic diversity of its population? Control for socioeconomic factors and historical events that might have impacted both happiness and genetic diversity.
We used a regression analysis to explore the correlation between a nation's average happiness score (dependent variable) and genetic diversity metrics (independent variables). The model was adjusted for socioeconomic factors and historical events.

- Are there discernible patterns in allelic frequencies among countries with higher emigration rates as compared to those with lower rates?
This question is focused on understanding patterns in allelic frequencies among countries with different emigration rates. Population genetics and statistical analyses was used for exploring the relationship between genetics and migration patterns.

- How does an influx of migrants impact the host country in subsequent years?

-  How have migration patterns changed over time in relation to shifts in the happiness scores of both source and destination countries?

- looking at Digital and Technological Footprints. variables such as internet freedom, digital infrastructure quality, and tech ecosystem vitality can be migration determinants, especially for the young, urban, and skilled demographic.

- can look at more specific indicators 
SENSITIVITY INDICATOR 1: Natural capital dependency
- The indicator captures a country’s reliance on ecosystem services, which are themselves exposed to disruption by climate change.

EXPOSURE INDICATOR 1: Projected change of biome distribution
- The indicator captures the threat of changes in biome function. It is based on the projected impact of climate change on the area occupied by different biomes within a country.

EXPOSURE INDICATOR 1: Projected change of warm periods
- Human living conditions are threatened by the increased intensity and/or frequency of extreme weather, including storms, flooding, landslides and heat waves, that climate change is bringing or will bring (Satterthwaite, 2008).


EXPOSURE INDICATOR 2: Projected change of flood hazard
- An indicator that complements the warm period projection, to capture one of the important disastrous threats to human living conditions.


SENSITIVITY INDICATOR 1: Urban concentration
- Countries in which urban populations are concentrated in a single or a small number of urban areas are considered more sensitive to climate change(Lankao, 2008). According to this indicator, a country with a highly concentrated urban sector and a highly urbanized population is the most sensitive.























# Archive
---

(2) Migration Effects on Host Country :
Now that we understand the overarching patterns, it's logical to then focus on the specific implications of these patterns.
- How does an influx of migrants impact the host country in subsequent years? Adjust for economic impact, unemployment rates, and social integration programs.

(2) Are people migrating to happier countries?
- Chord plot with unhapping countries with people flowing to happier ones?

(3) Happiness and Genetic Diversity:
After exploring the direct impact of migration on happiness, this question delves deeper into understanding if there's any inherent relationship between a country's happiness score and the genetic diversity of its population.
- Is there a correlation between a nation's average happiness score and the genetic diversity of its population? Control for socioeconomic factors and historical events that might have impacted both happiness and genetic diversity.

(4) Genetics and Migration:
Building on the knowledge of how happiness relates to genetic diversity, it's a fitting progression to then explore how genetic factors might influence or be influenced by migration patterns.
- Are there discernible patterns in allelic frequencies among countries with higher emigration rates as compared to those with lower rates? Consider adjusting for shared historical migrations or neighboring country influence.











3. **Difference in Happiness Scores**: We compared the distribution of differences in happiness scores (source - target) over time. If the distribution leans towards positive, it suggests people migrate to happier countries.

4. **Correlation Analysis**: Measure correlation coefficients between the difference in happiness scores and migration weights. A positive correlation might suggest that as the happiness difference increases, so does the migration weight.

5. **Economic Downturns**:
    - Identify years of global economic downturns (you might need external data for this or define it based on a decrease in average global GDP).
    - Analyze migration patterns during these years. Do more people migrate during economic downturns?
    - Check the relationship between happiness scores and migration during these years. Do people tend to move from countries with larger drops in GDP or happiness?

6. **Regional Conflicts**:
    - Identify major regional conflicts during the time frame (this would require external data).
    - See if there's a spike in migration from these conflict zones.
    - Analyze the happiness score trend in these zones compared to global average.


# Circular migration plot 
representing the inter-relationships between data points in a graph. The nodes are arranged radially around a circle with the relationships between the data points drawn as arcs (or chords) connecting the nodes. The number of chords is scaled by a weight (migration flow).
This code was written based on this [source](https://holoviews.org/reference/elements/bokeh/Chord.html).





**References**
[Inspiration 1](http://download.gsb.bund.de/BIB/global_flow/) 

[Global migration datasheet](http://download.gsb.bund.de/BIB/global_flow/VID_Global_Migration_Datasheet_web.pdf)

![inspo](https://s3-eu-west-1.amazonaws.com/pfigshare-u-previews/15025469/preview.gif?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAIYCQYOYV5JSSROOA/20230722/eu-west-1/s3/aws4_request&X-Amz-Date=20230722T162858Z&X-Amz-Expires=10&X-Amz-SignedHeaders=host&X-Amz-Signature=ce612851f3829e2033fe6baf0a073882eb8dbfeacfa380167a0823de20e47339)


![How to read flow plot](https://github.com/nooralteneiji/Happiness-Without-Borders/blob/main/FlowChord.png)

![circular chord plot example](https://www.science.org/cms/10.1126/science.1248676/asset/0c9e0fd7-57fa-4460-9c26-6b82230adf14/assets/graphic/343_1520_f2.jpeg)

References used to write code for chord diagram: [Used chapter 5 as it details how to create migrations plots in javascript and R](https://github.com/null2/globalmigration/blob/master/VID%20WP%20Visualising%20Migration%20Flow%20Data%20with%20Circular%20Plots.pdf), [source 1](https://holoviews.org/reference/elements/bokeh/Chord.html), [source 2](https://stackoverflow.com/questions/65344303/circular-chord-diagram-in-python), [source 3](https://d3blocks.github.io/d3blocks/pages/html/Chord.html), [source 4 (guide for chord diagrams in R)](https://download.gsb.bund.de/BIB/global_flow/VID%20WP%20Visualising%20Migration%20Flow%20Data%20with%20Circular%20Plots.pdf)


