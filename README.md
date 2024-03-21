# Power Outages Research Project

## Introduction
Lights working and the internet running are often taken for granted until they suddenly disappear during a power outage. In this project, I aim to delve into a comprehensive dataset related to power outages. This dataset includes crucial information on various aspects of outages, such as electricity consumption, regional economic characteristics, regional land-use patterns, regional climate data, and most importantly, outage events. My goal is to find the factors that make some poweroutages more sever then others and well as use these fatcors to predict a power ouatges severity

The dataset is from University of Purdue since 2018. The data is divided into five sections:such as electricity consumption, regional economic characteristics, regional land-use patterns, regional climate data, and most importantly, outage events. The dataframe for Poweroutages has 1,526 rows. Each row represents an outage that happened in a state. If a poweroutage affects more than one state their will be a row for each event. For further research purposes, I added two columns represnting a timestamp for the start of and outage and end. Most importantly I am adding a columns represnting wether a State's power sector is classified as regulated. This is becuase in teh past a major cause of teh Claifornia's rolling blakcouts in the early 2000s was the deregulation of its power sector. I want to test if this is an outlier ouccurance or maybe states that have a deregulate dpower sector have more outages. 

## Project Steps
1. **Data Cleaning and Exploratory Data Analysis**: We will start by cleaning the dataset and conducting exploratory data analysis to obtain basic information about the data and explore relationships between columns.
2. **Missingness Analysis**: We will assess the missingness contained in the dataset, focusing on the description, review, and rating columns. Specifically, we will analyze the missingness mechanism (NMAR, MCAR, or MAR) and provide insights into the missingness of some reviews.
3. **NMAR Analysis**: In-depth analysis of the review column to understand the reasons behind missing reviews.
4. **MCAR and MAR Analysis**: Imputation strategies for handling missing data.

Stay tuned for more insights as we delve into the fascinating world of recipes and ratings!

## Data Cleaning and Exploratory Data Analysis

# Data Cleaning
Each additional minute the powers out for more problems arrise. This makes knowing the length of a power outage vital in addressing its serverity. Here I combined the OUTAGE.START.DATE and OUTAGE.START.TIME columns into one timestamp object and OUTAGE.END.DATE and OUTAGE.END.TIME into another timestamp object.
# Univariate Analysis
<iframe
  src="assets/Outages-Duration-Histogram.html"
  width="600"
  height="600"
  frameborder="0"
></iframe>

<iframe
  src="assets/REGULATED.html"
  width="600"
  height="600"
  frameborder="0"
></iframe>

# Bivariate Analysis
<iframe
  src="assets/REGULATED_groups.html"
  width="600"
  height="600"
  frameborder="0"
></iframe>



# Interesting Aggregates

|   Central |   East North Central |   Northeast |   Northwest |   South |   Southeast |   Southwest |   West |   West North Central |\n|----------:|---------------------:|------------:|------------:|--------:|------------:|------------:|-------:|---------------------:|\n|         2 |                    1 |           9 |           1 |       1 |           1 |         nan |      1 |                  nan |\n|         5 |                    3 |           2 |           2 |       5 |           5 |           4 |      1 |                    5 |

Here you can see a pibvot tbale of where dereguated states are located. You can see that theyre consentrated in the northeast.
## Assessment of Missingness
# NMAR Analysis
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
I believe that The MW.LOSS column is MAR

# Missingness Dependency
0.8363394331374345 differnece observed of the PI.UTIL.OFUSA if MW is missing or not this has an extremely low p values of 0.01
and can be seen by this grph
<iframe
  src="assets/DiffMeans_PI.UTIL.OFUSA.html"
  width="600"
  height="600"
  frameborder="0"
></iframe>


128.76779051172707 differnece observed of the OUTAGE.DURATION if MW is missing or not this has an extremely low p values of 0.678
and can be seen by this grph
<iframe
  src="assets/DiffMeans_OUTAGE.DURATION.html"
  width="600"
  height="600"
  frameborder="0"
></iframe>



<iframe
  src="assets/PI.UTIL.OFUSA_MISSING.html"
  width="600"
  height="600"
  frameborder="0"
></iframe>
<iframe
  src="assets/OUTAGE.DURATION_MISSING.html"
  width="600"
  height="600"
  frameborder="0"
></iframe>

## Hypothesis Testing

# Hypothesis Testing

Clearly state your null and alternative hypotheses, your choice of test statistic and significance level, the resulting 
p 0.0005 we reject the null hypothesis that 
-value, and your conclusion. Justify why these choices are good choices for answering the question you are trying to answer.

Optional: Embed a visualization related to your hypothesis test in your website.

<iframe
  src="assets/hypothesis_test.html"
  width="600"
  height="600"
  frameborder="0"
></iframe>

# power-outage

|   YEAR |   MONTH | U.S._STATE   | POSTAL.CODE   | NERC.REGION   | CLIMATE.REGION     |   ANOMALY.LEVEL | CLIMATE.CATEGORY   | OUTAGE.START.DATE   | OUTAGE.START.TIME   | OUTAGE.RESTORATION.DATE   | OUTAGE.RESTORATION.TIME   | CAUSE.CATEGORY     | CAUSE.CATEGORY.DETAIL   |   HURRICANE.NAMES |   OUTAGE.DURATION |   DEMAND.LOSS.MW |   CUSTOMERS.AFFECTED |   RES.PRICE |   COM.PRICE |   IND.PRICE |   TOTAL.PRICE |   RES.SALES |   COM.SALES |   IND.SALES |   TOTAL.SALES |   RES.PERCEN |   COM.PERCEN |   IND.PERCEN |   RES.CUSTOMERS |   COM.CUSTOMERS |   IND.CUSTOMERS |   TOTAL.CUSTOMERS |   RES.CUST.PCT |   COM.CUST.PCT |   IND.CUST.PCT |   PC.REALGSP.STATE |   PC.REALGSP.USA |   PC.REALGSP.REL |   PC.REALGSP.CHANGE |   UTIL.REALGSP |   TOTAL.REALGSP |   UTIL.CONTRI |   PI.UTIL.OFUSA |   POPULATION |   POPPCT_URBAN |   POPPCT_UC |   POPDEN_URBAN |   POPDEN_UC |   POPDEN_RURAL |   AREAPCT_URBAN |   AREAPCT_UC |   PCT_LAND |   PCT_WATER_TOT |   PCT_WATER_INLAND | OUTAGE.START        | OUTAGE.RESTORATION   | REGULATED   |
|-------:|--------:|:-------------|:--------------|:--------------|:-------------------|----------------:|:-------------------|:--------------------|:--------------------|:--------------------------|:--------------------------|:-------------------|:------------------------|------------------:|------------------:|-----------------:|---------------------:|------------:|------------:|------------:|--------------:|------------:|------------:|------------:|--------------:|-------------:|-------------:|-------------:|----------------:|----------------:|----------------:|------------------:|---------------:|---------------:|---------------:|-------------------:|-----------------:|-----------------:|--------------------:|---------------:|----------------:|--------------:|----------------:|-------------:|---------------:|------------:|---------------:|------------:|---------------:|----------------:|-------------:|-----------:|----------------:|-------------------:|:--------------------|:---------------------|:------------|
|   2011 |       7 | Minnesota    | MN            | MRO           | East North Central |            -0.3 | normal             | 2011-07-01 00:00:00 | 17:00:00            | 2011-07-03 00:00:00       | 20:00:00                  | severe weather     | nan                     |               nan |              3060 |              nan |                70000 |       11.6  |        9.18 |        6.81 |          9.28 |     2332915 |     2114774 |     2113291 |       6562520 |      35.5491 |      32.225  |      32.2024 |         2308736 |          276286 |           10673 |           2595696 |        88.9448 |        10.644  |       0.411181 |              51268 |            47586 |          1.07738 |                 1.6 |           4802 |          274182 |       1.75139 |             2.2 |      5348119 |          73.27 |       15.28 |           2279 |      1700.5 |           18.2 |            2.14 |          0.6 |    91.5927 |         8.40733 |            5.47874 | 2011-07-01 17:00:00 | 2011-07-03 20:00:00  | True        |
|   2014 |       5 | Minnesota    | MN            | MRO           | East North Central |            -0.1 | normal             | 2014-05-11 00:00:00 | 18:38:00            | 2014-05-11 00:00:00       | 18:39:00                  | intentional attack | vandalism               |               nan |                 1 |              nan |                  nan |       12.12 |        9.71 |        6.49 |          9.28 |     1586986 |     1807756 |     1887927 |       5284231 |      30.0325 |      34.2104 |      35.7276 |         2345860 |          284978 |            9898 |           2640737 |        88.8335 |        10.7916 |       0.37482  |              53499 |            49091 |          1.08979 |                 1.9 |           5226 |          291955 |       1.79    |             2.2 |      5457125 |          73.27 |       15.28 |           2279 |      1700.5 |           18.2 |            2.14 |          0.6 |    91.5927 |         8.40733 |            5.47874 | 2014-05-11 18:38:00 | 2014-05-11 18:39:00  | True        |
|   2010 |      10 | Minnesota    | MN            | MRO           | East North Central |            -1.5 | cold               | 2010-10-26 00:00:00 | 20:00:00            | 2010-10-28 00:00:00       | 22:00:00                  | severe weather     | heavy wind              |               nan |              3000 |              nan |                70000 |       10.87 |        8.19 |        6.07 |          8.15 |     1467293 |     1801683 |     1951295 |       5222116 |      28.0977 |      34.501  |      37.366  |         2300291 |          276463 |           10150 |           2586905 |        88.9206 |        10.687  |       0.392361 |              50447 |            47287 |          1.06683 |                 2.7 |           4571 |          267895 |       1.70627 |             2.1 |      5310903 |          73.27 |       15.28 |           2279 |      1700.5 |           18.2 |            2.14 |          0.6 |    91.5927 |         8.40733 |            5.47874 | 2010-10-26 20:00:00 | 2010-10-28 22:00:00  | True        |
|   2012 |       6 | Minnesota    | MN            | MRO           | East North Central |            -0.1 | normal             | 2012-06-19 00:00:00 | 04:30:00            | 2012-06-20 00:00:00       | 23:00:00                  | severe weather     | thunderstorm            |               nan |              2550 |              nan |                68200 |       11.79 |        9.25 |        6.71 |          9.19 |     1851519 |     1941174 |     1993026 |       5787064 |      31.9941 |      33.5433 |      34.4393 |         2317336 |          278466 |           11010 |           2606813 |        88.8954 |        10.6822 |       0.422355 |              51598 |            48156 |          1.07148 |                 0.6 |           5364 |          277627 |       1.93209 |             2.2 |      5380443 |          73.27 |       15.28 |           2279 |      1700.5 |           18.2 |            2.14 |          0.6 |    91.5927 |         8.40733 |            5.47874 | 2012-06-19 04:30:00 | 2012-06-20 23:00:00  | True        |
|   2015 |       7 | Minnesota    | MN            | MRO           | East North Central |             1.2 | warm               | 2015-07-18 00:00:00 | 02:00:00            | 2015-07-19 00:00:00       | 07:00:00                  | severe weather     | nan                     |               nan |              1740 |              250 |               250000 |       13.07 |       10.16 |        7.74 |         10.43 |     2028875 |     2161612 |     1777937 |       5970339 |      33.9826 |      36.2059 |      29.7795 |         2374674 |          289044 |            9812 |           2673531 |        88.8216 |        10.8113 |       0.367005 |              54431 |            49844 |          1.09203 |                 1.7 |           4873 |          292023 |       1.6687  |             2.2 |      5489594 |          73.27 |       15.28 |           2279 |      1700.5 |           18.2 |            2.14 |          0.6 |    91.5927 |         8.40733 |            5.47874 | 2015-07-18 02:00:00 | 2015-07-19 07:00:00  | True        |





# H1
## INTRODUCTION

### H3
<iframe
  src="assets/power-outage.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>