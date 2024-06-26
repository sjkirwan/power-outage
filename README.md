# Power Outages Research Project

## Introduction
Lights working and the internet running are often taken for granted until they suddenly disappear during a power outage. In this project, I aim to delve into a comprehensive dataset related to power outages. This dataset includes crucial information on various aspects of outages, such as electricity consumption, regional economic characteristics, regional land-use patterns, regional climate data, and, most importantly, outage events. My goal is to find the factors that make some power outages more severe than others and use these factors to predict a power outage's severity.

The dataset is from 2018 and can be found on the University of Purdue [website](https://engineering.purdue.edu/LASCI/research-data/outages). The data is divided into five sections: electricity consumption, regional economic characteristics, regional land-use patterns, regional climate data, and, most importantly, outage events. The data frame for power outages has 1,526 rows. Each row represents an outage that happened in a state. If a power outage affects more than one state, each event will have a row. For further research purposes, I added two columns containing a timestamp for the start and end of an outage, respectively. In addition, I added a new third column representing whether a State's power sector is classified as regulated. I decided this would be a valuable column to add as, in the past, a significant cause of California's rolling blackouts in the early 2000s was the deregulation of its power sector. I will be testing whether regulation relates to power outages later in my hypothesis testing section.

## Project Steps
1. **Data Cleaning and Exploratory Data Analysis**: The first step in this project is data cleaning and exploratory data analysis. The goal is to prepare the dataset for analysis and begin to get a sense of how the columns are related.
2. **Assessment of Missingness**: I will assess the dataset's missingness, focusing on the 'OUTAGE.DURATION,' 'PI.UTIL.OFUSA,' and 'DEMAND.LOSS.MW' columns.
3. **Hypothesis Testing** In this section, I will answer my research question about whether the severity of power outages is higher in states that have deregulated their power sector.
4. **Framing a Prediction Problem** In this section, I will address how I will try and predict the severity of a power outage
5. **Baseline Model** In this section, I will be making a basic model to predict the severity of a power outage
6. **Final Model** In this section, I will be improving upon the basic model by adding features, engineering new features from columns, and adjusting hyperparameters
7. **Fairness Analysis** In this section, I will address if the final model's accuracy varies between wealthy and poor states


## Data Cleaning and Exploratory Data Analysis

### Data Cleaning
With each additional minute, the power goes out, and more problems arise. Knowing the length of a power outage is vital in addressing its severity. Here, I combined the 'OUTAGE.START.DATE' and 'OUTAGE.START.TIME' columns into one timestamp object and the 'OUTAGE.END.DATE' and 'OUTAGE.END.TIME' columns into another timestamp object. In addition to realigning the columns, I added a column representing whether a State's power sector is classified as regulated. I got the informatiom about the regulation status of a states power from [here](https://www.electricchoice.com/map-deregulated-energy-markets/). After these modifcations this here is the data frame I will be working with

|   YEAR |   MONTH | U.S._STATE   | POSTAL.CODE   | NERC.REGION   | CLIMATE.REGION     |   ANOMALY.LEVEL | CLIMATE.CATEGORY   | OUTAGE.START.DATE   | OUTAGE.START.TIME   | OUTAGE.RESTORATION.DATE   | OUTAGE.RESTORATION.TIME   | CAUSE.CATEGORY     | CAUSE.CATEGORY.DETAIL   |   HURRICANE.NAMES |   OUTAGE.DURATION |   DEMAND.LOSS.MW |   CUSTOMERS.AFFECTED |   RES.PRICE |   COM.PRICE |   IND.PRICE |   TOTAL.PRICE |   RES.SALES |   COM.SALES |   IND.SALES |   TOTAL.SALES |   RES.PERCEN |   COM.PERCEN |   IND.PERCEN |   RES.CUSTOMERS |   COM.CUSTOMERS |   IND.CUSTOMERS |   TOTAL.CUSTOMERS |   RES.CUST.PCT |   COM.CUST.PCT |   IND.CUST.PCT |   PC.REALGSP.STATE |   PC.REALGSP.USA |   PC.REALGSP.REL |   PC.REALGSP.CHANGE |   UTIL.REALGSP |   TOTAL.REALGSP |   UTIL.CONTRI |   PI.UTIL.OFUSA |   POPULATION |   POPPCT_URBAN |   POPPCT_UC |   POPDEN_URBAN |   POPDEN_UC |   POPDEN_RURAL |   AREAPCT_URBAN |   AREAPCT_UC |   PCT_LAND |   PCT_WATER_TOT |   PCT_WATER_INLAND | OUTAGE.START        | OUTAGE.RESTORATION   | REGULATED   |
|-------:|--------:|:-------------|:--------------|:--------------|:-------------------|----------------:|:-------------------|:--------------------|:--------------------|:--------------------------|:--------------------------|:-------------------|:------------------------|------------------:|------------------:|-----------------:|---------------------:|------------:|------------:|------------:|--------------:|------------:|------------:|------------:|--------------:|-------------:|-------------:|-------------:|----------------:|----------------:|----------------:|------------------:|---------------:|---------------:|---------------:|-------------------:|-----------------:|-----------------:|--------------------:|---------------:|----------------:|--------------:|----------------:|-------------:|---------------:|------------:|---------------:|------------:|---------------:|----------------:|-------------:|-----------:|----------------:|-------------------:|:--------------------|:---------------------|:------------|
|   2011 |       7 | Minnesota    | MN            | MRO           | East North Central |            -0.3 | normal             | 2011-07-01 00:00:00 | 17:00:00            | 2011-07-03 00:00:00       | 20:00:00                  | severe weather     | nan                     |               nan |              3060 |              nan |                70000 |       11.6  |        9.18 |        6.81 |          9.28 |     2332915 |     2114774 |     2113291 |       6562520 |      35.5491 |      32.225  |      32.2024 |         2308736 |          276286 |           10673 |           2595696 |        88.9448 |        10.644  |       0.411181 |              51268 |            47586 |          1.07738 |                 1.6 |           4802 |          274182 |       1.75139 |             2.2 |      5348119 |          73.27 |       15.28 |           2279 |      1700.5 |           18.2 |            2.14 |          0.6 |    91.5927 |         8.40733 |            5.47874 | 2011-07-01 17:00:00 | 2011-07-03 20:00:00  | True        |
|   2014 |       5 | Minnesota    | MN            | MRO           | East North Central |            -0.1 | normal             | 2014-05-11 00:00:00 | 18:38:00            | 2014-05-11 00:00:00       | 18:39:00                  | intentional attack | vandalism               |               nan |                 1 |              nan |                  nan |       12.12 |        9.71 |        6.49 |          9.28 |     1586986 |     1807756 |     1887927 |       5284231 |      30.0325 |      34.2104 |      35.7276 |         2345860 |          284978 |            9898 |           2640737 |        88.8335 |        10.7916 |       0.37482  |              53499 |            49091 |          1.08979 |                 1.9 |           5226 |          291955 |       1.79    |             2.2 |      5457125 |          73.27 |       15.28 |           2279 |      1700.5 |           18.2 |            2.14 |          0.6 |    91.5927 |         8.40733 |            5.47874 | 2014-05-11 18:38:00 | 2014-05-11 18:39:00  | True        |
|   2010 |      10 | Minnesota    | MN            | MRO           | East North Central |            -1.5 | cold               | 2010-10-26 00:00:00 | 20:00:00            | 2010-10-28 00:00:00       | 22:00:00                  | severe weather     | heavy wind              |               nan |              3000 |              nan |                70000 |       10.87 |        8.19 |        6.07 |          8.15 |     1467293 |     1801683 |     1951295 |       5222116 |      28.0977 |      34.501  |      37.366  |         2300291 |          276463 |           10150 |           2586905 |        88.9206 |        10.687  |       0.392361 |              50447 |            47287 |          1.06683 |                 2.7 |           4571 |          267895 |       1.70627 |             2.1 |      5310903 |          73.27 |       15.28 |           2279 |      1700.5 |           18.2 |            2.14 |          0.6 |    91.5927 |         8.40733 |            5.47874 | 2010-10-26 20:00:00 | 2010-10-28 22:00:00  | True        |
|   2012 |       6 | Minnesota    | MN            | MRO           | East North Central |            -0.1 | normal             | 2012-06-19 00:00:00 | 04:30:00            | 2012-06-20 00:00:00       | 23:00:00                  | severe weather     | thunderstorm            |               nan |              2550 |              nan |                68200 |       11.79 |        9.25 |        6.71 |          9.19 |     1851519 |     1941174 |     1993026 |       5787064 |      31.9941 |      33.5433 |      34.4393 |         2317336 |          278466 |           11010 |           2606813 |        88.8954 |        10.6822 |       0.422355 |              51598 |            48156 |          1.07148 |                 0.6 |           5364 |          277627 |       1.93209 |             2.2 |      5380443 |          73.27 |       15.28 |           2279 |      1700.5 |           18.2 |            2.14 |          0.6 |    91.5927 |         8.40733 |            5.47874 | 2012-06-19 04:30:00 | 2012-06-20 23:00:00  | True        |
|   2015 |       7 | Minnesota    | MN            | MRO           | East North Central |             1.2 | warm               | 2015-07-18 00:00:00 | 02:00:00            | 2015-07-19 00:00:00       | 07:00:00                  | severe weather     | nan                     |               nan |              1740 |              250 |               250000 |       13.07 |       10.16 |        7.74 |         10.43 |     2028875 |     2161612 |     1777937 |       5970339 |      33.9826 |      36.2059 |      29.7795 |         2374674 |          289044 |            9812 |           2673531 |        88.8216 |        10.8113 |       0.367005 |              54431 |            49844 |          1.09203 |                 1.7 |           4873 |          292023 |       1.6687  |             2.2 |      5489594 |          73.27 |       15.28 |           2279 |      1700.5 |           18.2 |            2.14 |          0.6 |    91.5927 |         8.40733 |            5.47874 | 2015-07-18 02:00:00 | 2015-07-19 07:00:00  | True        |


### Univariate Analysis
<iframe
  src="assets/Outages-Duration-Histogram.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

Throughout this process, 'OUTAGE.DURATION' will used as a metric of the severity of a power outage. Here, you see how most power outages are fixed quickly.


### Bivariate Analysis
<iframe
  src="assets/Duration_vs_Price.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

One factor that might indicate a significant power outage is the price of electricity. I thought higher prices might mean power companies are trying to encourage less use. While there isn't a major correlation between these two, when the regulatory variable is added, you can see clearly that unregulated states have higher electricity prices!!

<iframe
  src="assets/Mean_Outage_Duration_Cause.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

Another factor that might indicate a significant power outage is the cause of the outage. In this chart, you can see that the average outage time varies drastically between each of the possible cause categories.


## Interesting Aggregates

| CLIMATE.REGION     |   False |   True |
|:-------------------|--------:|-------:|
| Central            |       2 |      5 |
| East North Central |       1 |      3 |
| Northeast          |       9 |      2 |
| Northwest          |       1 |      2 |
| South              |       2 |      5 |
| Southeast          |       1 |      6 |
| Southwest          |     nan |      4 |
| West               |       1 |      1 |
| West North Central |     nan |      5 |

Here, you can see a pivot table showing the number of deregulated power (False meaning deregulated True meaning regulated) states in each region. From this table its clear that states in the Northeast are overwhelmingly deregulated.

## Assessment of Missingness

### NMAR Analysis
The column with the most missing columns is the 'DEMAND.LOSS.MW' column below. I took the first and last ten rows of the data frame with the 'DEMAND.LOSS.MW,' and two other columns that look like they might be related.

**FIRST TEN ROWS**

|   DEMAND.LOSS.MW |   OUTAGE.DURATION |   PI.UTIL.OFUSA |
|-----------------:|------------------:|----------------:|
|                0 |              1548 |             0.3 |
|              nan |               870 |             0.4 |
|                0 |                 0 |             0.4 |
|                0 |               nan |             0.4 |
|              485 |               220 |             0.4 |
|              155 |               720 |             0.5 |
|             1650 |               nan |             0.7 |
|               84 |                59 |             0.3 |
|              373 |               181 |             0.3 |
|               35 |               nan |             0.2 |

**LAST TEN ROWS**

|   DEMAND.LOSS.MW |   OUTAGE.DURATION |   PI.UTIL.OFUSA |
|-----------------:|------------------:|----------------:|
|              nan |              3060 |             2.2 |
|              nan |                 1 |             2.2 |
|              nan |              3000 |             2.1 |
|              nan |              2550 |             2.2 |
|              250 |              1740 |             2.2 |
|              nan |              1860 |             2.1 |
|              nan |              2970 |             2.1 |
|               75 |              3960 |             2.1 |
|               20 |               155 |             2.2 |
|              nan |              3621 |             2.3 |

In these two slices of the power outage data frame it looks like when 'OUTAGE.DURATION' is high and 'PI.UTIL.OFUSA' is high, 'DEMAND.LOSS.MW'tends to be missing. This leads me to believe that 'DEMAND.LOSS.MW' is MAR and is related to these two columns. 

### Missingness Dependency
To test this idea, I perform a permutation test on the 'DEMAND.LOSS.MW' and 'PI.UTIL.OFUSA' columns. For my test statistic, I get an observed 0.836 difference in means of 'PI.UTIL.OFUSA' grouped by the missingness of 'DEMAND.LOSS.MW.' Then, through the permutation test, I got a p-value of 0.01, so it's clear that the two distributions of 'PI.UTIL.OFUSA' are different. This makes clear that 'DEMAND.LOSS.MW' is MAR.

<iframe
  src="assets/DiffMeans_PI.UTIL.OFUSA.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

The 'DEMAND.LOSS.MW' columns' missingness might be related to the 'OUTAGE.DURATION' column. Like before, to test this idea, I perform a permutation test on the 'DEMAND.LOSS.MW' and 'OUTAGE.DURATION' columns. For my test statistic I use difference in means of the 'OUTAGE.DURATION' betweens the groups made by the missingness of 'DEMAND.LOSS.MW.'. The observed value I found is 128.76. This seemed promising however, I got a very high p value of 0.678, so the 'DEMAND.LOSS.MW' columns missingness is probably not related to the 'OUTAGE.DURATION' column

<iframe
  src="assets/DiffMeans_OUTAGE.DURATION.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>


## Hypothesis Testing

### Hypothesis Testing

<iframe
  src="assets/Mean_Outage_Duration.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

**NULL HYPOTHESIS**: The distribution of the length of a power outage in regulated states is the same as in deregulated states

**ALTERNATIVE HYPOTHESIS**: Deregulated states' power outages last longer than regulated states.

Since 'OUTAGE.DURATION' is numerical data, I used the difference in mean as test statistics with a significance level of 0.05

> The observed difference in the mean is -263.63


<iframe
  src="assets/FIXED_FINAL_HYPOTHESIS_TEST.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

After I ran my permutation test, I got a p-value of 0.0682. This means I can not reject the null hypothesis at a significance level of 0.05. This does not diffitively prove that the distribution of the length of a power outage in regulated states is the same as in deregulated states as teh p value was still very low so further analysis should be done.


## Framing a Prediction Problem
My prediction goal is to predict the severity in terms of the duration of a power outage. I'm choosing to use outage duration as the severity metric as MW and customers affected are both missing substantial data. This model will be a regression model. I will evaluate its effectiveness with root mean squared error(RMSE). Most variables will be known at the time of the prediction, except the' DEMAND.LOSS.MW' and 'CUSTOMERS.AFFECTED' columns.

## Baseline Model
My baseline model is a Lasso Regression with a quantitative variable for a total number of customers and a nominal categorical variable that is hot encoded for the cause of the outage. I chose these two variables as they could be indicators of an outage's length. The cause of an outage could be an intentional attack, which is usually very quick to fix, or it could be an extreme weather event, which usually makes restoring power take longer. I chose total customers in the state as states with many customers will have more complex electrical grids that might be harder to fix.

After running the model, I get a RMSE of 9,429. This is very large and points to a flawed model. The graph below shows the difficulty of accurately predicting the outage length.

<iframe
  src="assets/New_Baseline_model.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>


## Final Model
For my final model, I changed away from a Lasso Regression to a Random Forest Regression as Lasso assumes a linear relationship between features and target, which might not be the case here; it also helped that Random Forest Regression has a lower RMSE. In addition, I changed my numerical variables from 'TOTAL.CUSTOMER' to 'POPDEN_RURAL' because the 'TOTAL.CUSTOMER' column is less indicative of a more complex power grid as population density. In addition, I standardized 'POPDEN_RURAL.' 

In exploratory analysis, I found that about varied from region to region, so I added a categorical variable, 'CLIMATE.REGION.' I believe that since industry requires a large amount of electricity, ' IND.PERCEN' could indicate a more complex grid that could take longer to fix. I engineered this feature with a quartile transformer since this category had significant outliers. The second feature I engineered is I binarized the 'PC.REALGSP.CHANGE' column to indicate whether the change was positive or negative, as a state that is losing GDP might invest less in its grid, causing prolonged power outages. The final column I added is the 'REGULATED' column I created earlier as it still had a very low p value so it might help my model.

To find the best hyperparameters, I used GridSearchCV and found keeping most of the defaults was best. Overall, these changes decreased my root mean squared error from 9,429 to 9,138. You can see that this model performed better than the previous model, but there's still a lot to improve upon.


<iframe
  src="assets/New_Final_model.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>


## Fairness Analysis
I wanted to check the fairness of my model in predicting the length of a power outage between poor and rich states. I introduced a binary variable "Rich_State" that is True if the state's per capita GDP is greater than the US capita GDP and False otherwise.

**NULL HYPOTHESIS**: The model root mean squared error does not vary significantly between states with a high per capita GDP as for states with a low GDP per capita

**ALTERNATIVE HYPOTHESIS**: The model has a higher RMSE for poor states than rich states

To test this, I am choosing a p-value of 0.05 and a test statistic of difference in means, as the root mean squared error is a numeric value.

<iframe
  src="assets/new_fairness_test_RMSE.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

I get a p value of 0.1838, which mean I cannot reject the Null Hypothesis. This means our model does not have higher root mean squared error for poor states than rich states. 

