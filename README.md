# [project name]
DSC 80 Spring 2024 Final Project
<br> Authors: Adrian Apsay, Ethan Flores

# Introduction
Welcome to our DSC 80 final project, where we aim to explore and gain insights focused on major power outage risks in the United States.  Over the past two decades, America has experienced numerous major outages, thus affecting millions of individuals causing numerous disruptions across the country. These outages highlight the urgent need for proactive measures to mitigate risks and enhance the resilience of our electrical grid.

We want to investigate the relationship of outage duration and severity based on the economic output of a given state. We hypothesize that states with lower economic output results in greater outage duration and severity due to the lack of resources and funds to maintain infrastructure that powers the electricity of the state. This question will provide insight into the economic productivity and performance of each state on a per-person basis, making it useful for comparing the economic status of different states based on the impact of power outages. By exploring this relationship, as represented by PC.REALGSP.STATE, we can assess how disruptions in electricity supply that provide power is affected by the economic well-being of each state. This analysis pinpoints vulnerabilities in states with lower economic output per capita, guiding policy decisions to enhance resilience to power outages and boost overall economic productivity for infrastructure funding.

Our dataset, derived from the article titled 'A Multi-Hazard Approach to Assess Severe Weather-Induced Major Power Outage Risks in the U.S.' by Mukherjee et al. (2018), covers the period from January 2000 to July 2016. It provides comprehensive information about severe weather-induced major power outages in the United States, including the geographical locations of the outages, regional climatic data, land-use characteristics, electricity consumption patterns, and economic indicators of the states affected by the outages. As defined by the Department of Energy, the major outages refer to those that impacted at least 50,000 customers or caused an unplanned firm load loss of at least 300 MW. The dataset, after simple formatting, contains a total of 1534 rows and 56 columns.  The key columns are listed below: 

|Column                |Description|
|---                |---        |
|`'YEAR'`                |Year an outage occurred|
|`'U.S._STATE'`                |State the outage occurred in|
|`'OUTAGE.DURATION'`                |Duration of outage events (in minutes)|
|`'PC.REALGSP.STATE'`                |Per capita real gross state product (GSP) in the U.S. state (measured in 2009 chained U.S. dollars)|
|`'UTIL.REALGSP'`                |Real GSP contributed by Utility industry (measured in 2009 chained U.S. dollars)|


# Data Cleaning and Exploratory Data Analysis
## Data Cleaning
We want to investigate the relationship of outage duration and severity based on the economy of a given state. We hypothesize that states with lower economic productivity results in greater outage duration and severity due to the lack of resources and funds to maintain infrastructure that powers the electricity of the state. This question will provide insight into the economic productivity and performance of each state, making it useful for comparing the economic status of different states based on the impact of power outages. By exploring the relationship between outage duration/severity in relation to the economic output of a state from their utilities sector along with their utility contribution to the state's total GSP, as represented by `UTIL.REALGSP` and `UTIL.CONTRI` respectively, we can assess how disruptions in electricity supply that provide power is affected by the economic well-being of each state. This analysis can help identify potential vulnerabilities in states with lower measures of economic productivity and possibly create policy decisions that improve resilience to power outages as well as enhancing overall economic productivity in the utilities sector to fund infrastructure and prevent these outages.

The Power Outages dataset is an Excel file that also had descriptions for each column. Reading into the Excel file locally in order to perform cleaning and EDA-related tasks displayed a deformed dataframe with columns that aren't necessary to the relationship we wanted to investigate. As such, we decided to keep only `YEAR`, `U.S._STATE`, `OUTAGE.DURATION`, `UTIL.REALGSP`, `UTIL.CONTRI` and fixed the format. These columns will be particularly useful for our exploratory data analysis as they provide essential information that allows us to investigate the relationship between power outage characteristics and economic factors at the state level.

Relevant Columns: `YEAR`, `U.S._STATE`, `OUTAGE.DURATION`, `UTIL.REALGSP`, `UTIL.CONTRI`

We kept these columns as they are useful for exploratory data analysis (EDA), providing essential information that allows us to investigate the relationship between power outage characteristics and economic factors at the state level overtime each year.

By analyzing these columns together, we can investigate how power outage duration and severity vary across different 
states and how they may be influenced by economic factors such as state-level economic output and their contribution in the utility sector. This analysis will highlight insights and patterns in areas where power outages are more rampant and/or more severe conditioned on the economic output and utility contribution for each state. 

Some columns we want to explain even further and our choices into keeping these columns are `UTIL.REALGSP` and `UTIL.CONTRI`:

Real Gross State Product of Utility Sectory by Each State (UTIL.REALGSP) will provide insights into the economic output of each state generated by the utility sector, helping to understand the importance of utilities in the state's economic activity and how different patterns may arise in outage duration and severity based on this metric.

Utility Industry's Contribution to Real Gross State Product (UTIL.CONTRI) represents the contribution of utility services to the overall economy of the state, that is, the share of the state's economy that may be contributed by utility services. It highlights the importance of utilities within each state's economy, which could be useful in understanding patterns in power outages (i.e. do states with more concentration on utilities in their economy have lesser outage duration and/or severity?)


## Exploratory Data Analysis
For almost the entirety of our EDA, we will be creating a dataframe that offers more nuanced information to garner deeper insights into the relationships between power outages and economic factors. That is, each row represents a power outage at a certain year and state (YEAR and U.S._STATE are also columns). We've also added additional columns:
1. `Total_Outages_Per_State_That_Year`: the total number of power outages per state that year
2. `Avg_Outage_Duration_Per_State_That_Year`: the average duration of power outages per state and year
3. `Outage_Severity`: interpreted as a measure of the severity of power outages in each state that year, taking into account both total number of outages and average duration for that state per year. This was computed by multiplying the
total number of outages by the average outage duration (`Total_Outages_Per_State_That_Year * Avg_Outage_Duration_Per_State_That_Year`)
4. `UTIL.REALGSP`: From original dataset (explained why this column was kept prior)
5. `UTIL.CONTRI`: From original dataset (explained why this column was kept prior)


Here are the first 5 rows of our new dataframe that we will be using for our Exploratory Data Analysis:

| YEAR | U.S._STATE | Total_Outages_Per_State_That_Year | Avg_Outage_Duration_Per_State_That_Year | UTIL.REALGSP | UTIL.CONTRI | Outage_Severity |
|------|-------------|-----------------------------------|----------------------------------------|--------------|-------------|-----------------|
| 2000 | Alabama     | 3                                 | 2247.0                                 | 5704         | 3.800386    | 6741.0          |
| 2000 | Alaska      | 1                                 | NaN                                    | 724          | 2.008545    | NaN             |
| 2000 | Arizona     | 2                                 | 66.0                                   | 5745         | 2.836533    | 132.0           |
| 2000 | California  | 1                                 | NaN                                    | 29581        | 1.789511    | NaN             |
| 2000 | Delaware    | 1                                 | NaN                                    | 1016         | 2.018356    | NaN             |

## Univariate Analysis
Plot 1: We'll take a look at the distribution of the `Avg_Outage_Duration_Per_State_That_Year` column to understand how outage durations vary across states per year.
<iframe
  src="assets/univariate_1.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
This histogram provides a visual understanding of how the average outage durations are distributed across different states and years, which can highlight trends or outliers worth investigating further. We can see that this histogram is right-skewed, where a majority of average outage durations are clustered towards the lower end of averages. Most states seem to experience relatively shorter average outage durations with the cut-off being around 15,000 minutes.


Plot 2: We will examine the distribution of the `Outage_Severity` column using a histogram in order to understand the severity of power outages across different states and years as a whole, which may serve as a better measurement in comparison to just total outages and average outage duration for each state per year since it accounts for both.
<iframe
  src="assets/univariate_2.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
This histogram plot visualizes the distribution of power outage severity across different states and years. The x-axis represents the severity of power outages, while the y-axis represents the frequency of occurrences. From the plot, we can observe the distribution of outage severity and identify any patterns or outliers present. In this case, we see that this histogram is right-skewed, with a majority of outage severities prevalent up to 50,000 minutes.

Plot 3: We will examine the distribution of the `UTIL.REALGSP` column using a histogram in order to understand the economic output generated by the utility sector across states and years.
<iframe
  src="assets/univariate_3.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
We see that the distribution of the Utility Real GSP is skewed right. If we were to label what makes a high or low Real GSP across states and years, we should use the median as a measure to classify such labels (under median, low; over median, high).

Plot 4: We will examine the distribution of the `UTIL.CONTRI` column using a histogram in order to understand the contribution of utility services to the overall economy of the state across years, that is, the share of the state's economy that may be contributed by utility services.
<iframe
  src="assets/univariate_4.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
We see that the distribution of Utility Contributions follows an approximately normal distrubtion, with the data clustered around 2%. This means that many states across 2000-2016 had its utility industry contribute to roughly 2% of their state economy. If we were to label what makes a high or low utility contribution, we would use the mean as a measure to classify such labels (under mean, low; over mean, high).


## Bivariate Analysis
Plot 1: Let's examine the relationship between `Outage_Severity` and `UTIL.REALGSP` using a scatter plot. This will help us understand if there's any association between the severity of power outages and the real gross state product contributed by the utility industry (economic output by the utility industry of the state) and further explore the relationship we're trying to investigate: the outage duration and severity based on the economy of a given state.
<iframe
  src="assets/bivariate_1.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
There seems to be particularly important findings in this scatterplot. The majority of data points cluster at lower Utility Real GSP values (under 10,000 USD) and lower Outage Severity values (under 50,000 minutes). Some states with higher Utility Real GSP values (20,000 - 30,000 USD) show higher Outage Severity values. For the most part, however, there appears to be no strong linear correlation between Utility Real GSP and Outage Severity, as the points seem to be widely scattered. It is important to note, though, that higher Utility GSP seem to show slightly more spread relative to outage severity by state. It could be inferred that states with higher Utility GSP likely have larger and more complex utility infrastructures that require varying levels of maintenance, age of infrastructure, and operational challenges. This possibly leads to a wider range of outage severities, but further analysis is necessary. Another finding as a result of this plot is that states that have a Utility Real GSP between 20k-30k are primarily New York, California, and Texas.

This bivariate analysis made us curious about the total outages for each state, so we plotted a geographical map below:
<iframe
  src="assets/outages_map_geo.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
California, Texas, and New York have had more outages in comparison to other U.S. States.

Plot 2: Let's examine the relationship between `Outage_Severity` and `UTIL.CONTRI` using a scatterplot. We want to see if there is any association between the severity of power outages and the contributions of a state's utility industry (economic output by the utility industry of the state) and further explore the relationship we're trying to investigate: the outage duration and severity based on the economy of a given state.
<iframe
  src="assets/bivariate_2.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
There doesn't seem to be any strong correlation between economic contributions in the utility industry of a state and outage severity, although we thought it would make sense to find a relationship between the two. It could be inferred that while higher economic contributions from the utility industry from a state may suggest greater financial resources to better uphold utility infrastructure (which also implies that the outage severity may be lessened due to better infrastructure), there may be other underlying factors as to why outages may be more severe outside the economic scope. It can be said, however, that there seems to be slightly more outage severity in states with lesser utility contributions in their economy.


## Interesting Aggregates / Aggregated Analysis
To further invesitage into outage duration/severity and its relationship to the state's economy using real GSP and utility contribution, we can create a pivot table. We decided to categorize states into 'High' and 'Low' based on their Utility Real GSP ('High' Real GSP if the Real GSP for a state at a particular year is greater than the median, else low) and contributions ('High' Utility Contribution label if the utility contribution for a state at a particular year is greater than the median, else low) for comparative analysis. We decided to use the median to label Real GSP as we see in the univariate analyses that Utility Real GSP is skewed right across states and years, thus prone to outliers. We use the mean to label utility contributions as we see in the univariate analyses that it follows a normal distribution. This can help determine if states with higher economic contributions and/or real GSP experience fewer outages or shorter outage durations. This is crucial for understanding the relationship between economic resources of a state and power outage occurrences.

| UTIL.REALGSP Label | UTIL.CONTRI Label | Avg_Outage_Duration_Per_State_That_Year | Total_Outages_Per_State_That_Year |
|--------------------|-------------------|----------------------------------------|-----------------------------------|
| High               | High              | 3094.850101                            | 516                               |
| High               | Low               | 2534.791183                            | 447                               |
| Low                | High              | 2678.692685                            | 190                               |
| Low                | Low               | 1893.920447                            | 381                               |

Let's visualize this:
<iframe
  src="assets/pivot_table.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
Given this pivot table, we garner some interesting findings. We see that a high Real GSP leads to a higher average outage duration in comparison to a low Real GSP without considering the utility contribution label. This may be due in part of better developed infrastucture requiring longer maintenance and security, but as stated previously, this requires more analysis outside of our current scope. Considering utility contributions, it seems that a high utility contribution regardless of GSP label leads to a higher average outer duration. It can also be seen that a low Real GSP label seems to lessen the average outage duration for both high and low utility contribution labels, possibly signifying the notion that Real GSP plays an influential role in outage duration.


# Assessment of Missingness

## NMAR Analysis

## Missingness Dependency

    
# Hypothesis Testing
After performing extensive data cleaning and Exploratory Data Analysis (EDA) to investigate the relationship of outage duration/severity in relation to the utility sector of a state's economy, the question is raised: does the utility real GSP of a state have profound impact on power outage duration? Using the original dataset, we will be asserting the following null and alternative hypotheses:

**Null Hypothesis (H0)**: There is no significant difference in the average outage duration between states with high economic productivity based on their utility sector (`UTIL.REALGSP`) and states with low economic productivity based on their utility sector.

**Alternative Hypothesis (H1)**: On average, the power outage duration for states with high economic productivity is larger than the power outage duration for states with low economic productivity.

**Test Satistic**: We will be using a difference of means; `(average power outage duration of high Real GSP) - (average power outage duration of low Real GSP)`

We will categorize the states into 'High' and 'Low' based on their Utility Real GSP ('High' Real GSP if the Real GSP for a state at a particular year is greater than the median, else low). We decided to use the median to label Utility Real GSP as we see in the univariate analyses that Real GSP is skewed right across states and years, thus prone to outliers.

We will then run a permutation test with 10,000 simulations to generate an empirical distribution of the test statistic, difference of means, under the null hypothesis.

**Results**:
The resulting p-value is 0.0, and with a significance level alpha of 0.05, we reject the null hypothesis. This means that, on average, the power outage duration for states with high economic productivity (measured by `UTIL.REALGSP`) is larger than states with low economic productivity. The plot below displays this empirical distribution along with the observed difference from our permutation test of 10,000 simulations.

<iframe
  src="assets/empirical_distribution.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

    
# Framing a Prediction Problem
From our analysis we can see that there wasn't a prominent relationship between duration/severity of power outages and the economic characteristics of each state. As a result, we have shifted our focus into if we are able to predict the cause of an outage based on the duration of the outage and its economic characteristics for the given state.

We will employ a multiclass classification model to accurately predict the labels in the `CAUSE.CATEGORY`. At this moment, we have only analyzed and placed an emphasis on the economic features of the dataset along with the duration of each outage. As a result, they will be our main features.In addition, due to the great imbalances in the `CAUSE.CATEGORY` column, we will opt for our test statistic to be F1-score.

| CAUSE.CATEGORY                | Count |
|-------------------------------|-------|
| severe weather                | 763   |
| intentional attack            | 418   |
| system operability disruption | 127   |
| public appeal                 | 69    |
| equipment failure             | 60    |
| fuel supply emergency         | 51    |
| islanding                     | 46    |
    
# Basline Model
For our multiclass classification problem, we will opt for a Random Forest classifier. This model will be ran on the following features: `CAUSE.CATEGORY`,`OUTAGE.DURATION`, `PC.REALGSP.STATE`, `PC.REALGSP.USA`,`PC.REALGSP.REL`,`PC.REALGSP.CHANGE`, `UTIL.REALGSP`, `TOTAL.REALGSP`, `UTIL.CONTRI`, `PI.UTIL.OFUSA`. Outside of the `CAUSE.CATEGORY` column (its nominal), the rest of the columns are quantitative. Therefore no necessary encodings are necessary for our baseline model. In addition, because the `CAUSE.CATEGORY` is our response variable there is no need to encode it as well.

Our baseline model showcased the following statistics:

| Model                          | Training Accuracy | Testing Accuracy | Precision | Recall | F1-Score |
|--------------------------------|-------------------|------------------|-----------|--------|----------|
| Random Forest, Baseline Model  | 0.99              | 0.68             | 0.67      | 0.68   | 0.68     |

The baseline model obtained a training accuracy of 99%, demonstrating strong performance on the training data. However, its testing accuracy dropped to 68%, which suggests overfitting and a need for improved generalization to new data. Despite these challenges, the model maintains a balanced F1-score of 0.68, indicating its capability to effectively balance precision and recall in classification tasks. While the score is solid, there is much to be improved on.
    
# Final Model
In our final model, I have decided to create 4 new features which is the alteration of `PC.REALGSP.STATE`, `PC.REALGSP.USA`, `PC.REALGSP.REL`, and `PC.REALGSP.CHANGE` by transforming them through a StandardScaler(). Economic indicators like these are likely to have different scales and units. Standardizing these features using StandardScaler ensures that they are all transformed to have a mean of 0 and a standard deviation of 1. This makes the interpretation of their coefficients more straightforward and prevents features with larger scales from dominating the model.

The modeling algorithm I chose to tune my Random Forest was `GridSearchCV`. From this, we saw that the best performing hyperparameters was: `Best Parameters: {'clf__max_depth': 50, 'clf__min_samples_leaf': 2, 'clf__min_samples_split': 10, 'clf__n_estimators': 50}`

Our final model showcased the following statistics:
| Model                                                   | Training Accuracy | Testing Accuracy | Precision | Recall | F1-Score |
|---------------------------------------------------------|-------------------|------------------|-----------|--------|----------|
| Random Forest, Baseline Model                            | 1.0               | 0.70             | 0.67      | 0.70   | 0.68     |
| Random Forest, Transformers with GridSearch, Final Model | 0.9               | 0.73             | 0.71      | 0.73   | 0.71     |

The final model (Random Forest with Transformers and GridSearch) is better than the baseline model primarily due to its improved generalization to new data, as evidenced by lower testing accuracy and higher precision and recall values. With the higher F1-score, indicating superior overall performance in classification tasks by maintaining a better balance between precision and recall.
    
# Fairness Analysis
In this section I decided to perform permutation tests on two separate groups from the`CAUSE.CATEGORY`, severe weather and intentional attack. Using their scores of precision, I aimed to test the following hypotheses.
- Null Hypothesis: Our model is fair. Its precision for severe weather and intentional attack are roughly the same, and any differences are due to random chance.
- Alternate Hypothesis: Our model is unfair. Its precision for intentional attack is lower than its precision for severe health.

After performing the test, I obtained a p-value of `0.8878`. This indicates insufficient evidence to reject the null hypothesis that the model's precision for severe weather and intentional attacks is not significantly different. This suggests that any observed variations in precision between the two categories are likely due to random chance rather than systematic bias. Therefore, the model appears to be fair in its performance across both types of events based on the available data.