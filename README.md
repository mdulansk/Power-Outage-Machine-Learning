# Introduction

The data in this website come from a dataset created by the Laboratory for Advancing Sustainable Critical Infrastructure at Purdue Univeristy (https://www.sciencedirect.com/science/article/pii/S2352340918307182). This dataset has a total of 1,534 rows, one for each power outage from Jan 2000 - July 2016 in the United States that impacted at least 50,000 customers or caused an unplanned firm load loss of atleast 300 MegaWatts. This dataset was used to perform for exploratory data analysis, assessment of missingness, and finally a permuatation test.

## Question

Does the Number of Power Outages per 100,000 people from States in the West and the East Come from the same Distribution?

## Purpose

It is important to understand the differences in the number of power outages between the East and West regions because it can help politicians and policymakers develop more rigorous strategies to prevent outages in the future. 

## Important Columns

Throughout this report there are a few relevant columns that are mentioned.

- OUTAGE.START.DATE: The day on which the given power outage started
- OUTAGE.START.TIME: The time at which the power outage started
- OUTAGE.RESTORATION.DATE: The day on which the power outage was restored
- OUTAGE.RESTORATION.TIME: The time at whch the power outage was restored
- OUTAGE.DURATION: The time the power outage lasted. Originally in minutes but is changed to hours for easier interpretation.
- PC.REALGSP.STATE: Per capita real gross state product (GSP) in the U.S. state (measured in 2009 chained U.S. dollars)
- POSTAL.CODE: Represents the postal code of the U.S. states, two letter abbreviation
- CLIMATE.REGION: U.S. Climate regions as specified by National Centers for Environmental Information (nine climatically consistent regions in continental U.S.A.)
- POPPCT_UC: Percentage of the total population of the U.S. state represented by the population of the urban clusters (in %)
- POPULATION: Population in the U.S. state in a year
- ANOMALY.LEVEL: his represents the oceanic El Niño/La Niña (ONI) index referring to the cold and warm episodes by season. It is estimated as a 3-month running mean of ERSST.v4 SST anomalies in the Niño 3.4 region (5°N to 5°S, 120–170°W) 

# Exploratory Data Analysis

How the power outage data was cleaned and explored to reach further depth on questions to be answered. 

## Data Cleaning

### 1.

The data from Purdue University's website is in a .xlsx excel sheet. In order to read it in certain rows and columns from the excel sheet had to be dropped in order to turn it into a usable dataframe in pandas.

### 2.

Each power outage had an entry for the given outage's start day and start time separately, as well as the restoration start day and start time. These were both joined together to create a single column for the outage start, OUTAGE.START, and a single column for the restoration date, OUTAGE.RESTORATION. These columns have the start time as a datetime object to the second of when the outage started, as well as when the restoration started, respectively. 

### 3.

The OUTAGE.DURATION column was divided by sixty in order to make it in minutes, which is a more understandable unit for the duration of power outages. After this was completed the outage dataframe was fully cleaned.

<div style ="width: 480 px; overflow-x: auto;">
    <table class="dataframe">
        <thead>
            <tr style="text-align: right;">
            <th></th>
            <th>YEAR</th>
            <th>MONTH</th>
            <th>U.S._STATE</th>
            <th>POSTAL.CODE</th>
            <th>NERC.REGION</th>
            <th>CLIMATE.REGION</th>
            <th>ANOMALY.LEVEL</th>
            <th>CLIMATE.CATEGORY</th>
            <th>OUTAGE.START.DATE</th>
            <th>OUTAGE.START.TIME</th>
            <th>OUTAGE.RESTORATION.DATE</th>
            <th>OUTAGE.RESTORATION.TIME</th>
            <th>CAUSE.CATEGORY</th>
            <th>CAUSE.CATEGORY.DETAIL</th>
            <th>HURRICANE.NAMES</th>
            <th>OUTAGE.DURATION</th>
            <th>DEMAND.LOSS.MW</th>
            <th>CUSTOMERS.AFFECTED</th>
            <th>RES.PRICE</th>
            <th>COM.PRICE</th>
            <th>IND.PRICE</th>
            <th>TOTAL.PRICE</th>
            <th>RES.SALES</th>
            <th>COM.SALES</th>
            <th>IND.SALES</th>
            <th>TOTAL.SALES</th>
            <th>RES.PERCEN</th>
            <th>COM.PERCEN</th>
            <th>IND.PERCEN</th>
            <th>RES.CUSTOMERS</th>
            <th>COM.CUSTOMERS</th>
            <th>IND.CUSTOMERS</th>
            <th>TOTAL.CUSTOMERS</th>
            <th>RES.CUST.PCT</th>
            <th>COM.CUST.PCT</th>
            <th>IND.CUST.PCT</th>
            <th>PC.REALGSP.STATE</th>
            <th>PC.REALGSP.USA</th>
            <th>PC.REALGSP.REL</th>
            <th>PC.REALGSP.CHANGE</th>
            <th>UTIL.REALGSP</th>
            <th>TOTAL.REALGSP</th>
            <th>UTIL.CONTRI</th>
            <th>PI.UTIL.OFUSA</th>
            <th>POPULATION</th>
            <th>POPPCT_URBAN</th>
            <th>POPPCT_UC</th>
            <th>POPDEN_URBAN</th>
            <th>POPDEN_UC</th>
            <th>POPDEN_RURAL</th>
            <th>AREAPCT_URBAN</th>
            <th>AREAPCT_UC</th>
            <th>PCT_LAND</th>
            <th>PCT_WATER_TOT</th>
            <th>PCT_WATER_INLAND</th>
            </tr>
        </thead>
        <tbody>
            <tr>
            <th>0</th>
            <td>2011</td>
            <td>7.0</td>
            <td>Minnesota</td>
            <td>MN</td>
            <td>MRO</td>
            <td>East North Central</td>
            <td>-0.3</td>
            <td>normal</td>
            <td>2011-07-01</td>
            <td>17:00:00</td>
            <td>2011-07-03</td>
            <td>20:00:00</td>
            <td>severe weather</td>
            <td>NaN</td>
            <td>NaN</td>
            <td>3060.0</td>
            <td>NaN</td>
            <td>70000.0</td>
            <td>11.60</td>
            <td>9.18</td>
            <td>6.81</td>
            <td>9.28</td>
            <td>2332915.0</td>
            <td>2114774.0</td>
            <td>2113291.0</td>
            <td>6562520.0</td>
            <td>35.549073</td>
            <td>32.225029</td>
            <td>32.202431</td>
            <td>2308736</td>
            <td>276286</td>
            <td>10673</td>
            <td>2595696</td>
            <td>88.944776</td>
            <td>10.644005</td>
            <td>0.411181</td>
            <td>51268</td>
            <td>47586</td>
            <td>1.077376</td>
            <td>1.6</td>
            <td>4802</td>
            <td>274182</td>
            <td>1.751391</td>
            <td>2.2</td>
            <td>5348119</td>
            <td>73.27</td>
            <td>15.28</td>
            <td>2279.0</td>
            <td>1700.5</td>
            <td>18.2</td>
            <td>2.14</td>
            <td>0.6</td>
            <td>91.592666</td>
            <td>8.407334</td>
            <td>5.478743</td>
            </tr>
            <tr>
            <th>1</th>
            <td>2014</td>
            <td>5.0</td>
            <td>Minnesota</td>
            <td>MN</td>
            <td>MRO</td>
            <td>East North Central</td>
            <td>-0.1</td>
            <td>normal</td>
            <td>2014-05-11</td>
            <td>18:38:00</td>
            <td>2014-05-11</td>
            <td>18:39:00</td>
            <td>intentional attack</td>
            <td>vandalism</td>
            <td>NaN</td>
            <td>1.0</td>
            <td>NaN</td>
            <td>NaN</td>
            <td>12.12</td>
            <td>9.71</td>
            <td>6.49</td>
            <td>9.28</td>
            <td>1586986.0</td>
            <td>1807756.0</td>
            <td>1887927.0</td>
            <td>5284231.0</td>
            <td>30.032487</td>
            <td>34.210389</td>
            <td>35.727564</td>
            <td>2345860</td>
            <td>284978</td>
            <td>9898</td>
            <td>2640737</td>
            <td>88.833534</td>
            <td>10.791609</td>
            <td>0.374820</td>
            <td>53499</td>
            <td>49091</td>
            <td>1.089792</td>
            <td>1.9</td>
            <td>5226</td>
            <td>291955</td>
            <td>1.790002</td>
            <td>2.2</td>
            <td>5457125</td>
            <td>73.27</td>
            <td>15.28</td>
            <td>2279.0</td>
            <td>1700.5</td>
            <td>18.2</td>
            <td>2.14</td>
            <td>0.6</td>
            <td>91.592666</td>
            <td>8.407334</td>
            <td>5.478743</td>
            </tr>
            <tr>
            <th>2</th>
            <td>2010</td>
            <td>10.0</td>
            <td>Minnesota</td>
            <td>MN</td>
            <td>MRO</td>
            <td>East North Central</td>
            <td>-1.5</td>
            <td>cold</td>
            <td>2010-10-26</td>
            <td>20:00:00</td>
            <td>2010-10-28</td>
            <td>22:00:00</td>
            <td>severe weather</td>
            <td>heavy wind</td>
            <td>NaN</td>
            <td>3000.0</td>
            <td>NaN</td>
            <td>70000.0</td>
            <td>10.87</td>
            <td>8.19</td>
            <td>6.07</td>
            <td>8.15</td>
            <td>1467293.0</td>
            <td>1801683.0</td>
            <td>1951295.0</td>
            <td>5222116.0</td>
            <td>28.097672</td>
            <td>34.501015</td>
            <td>37.365983</td>
            <td>2300291</td>
            <td>276463</td>
            <td>10150</td>
            <td>2586905</td>
            <td>88.920583</td>
            <td>10.687018</td>
            <td>0.392361</td>
            <td>50447</td>
            <td>47287</td>
            <td>1.066826</td>
            <td>2.7</td>
            <td>4571</td>
            <td>267895</td>
            <td>1.706266</td>
            <td>2.1</td>
            <td>5310903</td>
            <td>73.27</td>
            <td>15.28</td>
            <td>2279.0</td>
            <td>1700.5</td>
            <td>18.2</td>
            <td>2.14</td>
            <td>0.6</td>
            <td>91.592666</td>
            <td>8.407334</td>
            <td>5.478743</td>
            </tr>
            <tr>
            <th>3</th>
            <td>2012</td>
            <td>6.0</td>
            <td>Minnesota</td>
            <td>MN</td>
            <td>MRO</td>
            <td>East North Central</td>
            <td>-0.1</td>
            <td>normal</td>
            <td>2012-06-19</td>
            <td>04:30:00</td>
            <td>2012-06-20</td>
            <td>23:00:00</td>
            <td>severe weather</td>
            <td>thunderstorm</td>
            <td>NaN</td>
            <td>2550.0</td>
            <td>NaN</td>
            <td>68200.0</td>
            <td>11.79</td>
            <td>9.25</td>
            <td>6.71</td>
            <td>9.19</td>
            <td>1851519.0</td>
            <td>1941174.0</td>
            <td>1993026.0</td>
            <td>5787064.0</td>
            <td>31.994099</td>
            <td>33.543330</td>
            <td>34.439329</td>
            <td>2317336</td>
            <td>278466</td>
            <td>11010</td>
            <td>2606813</td>
            <td>88.895368</td>
            <td>10.682239</td>
            <td>0.422355</td>
            <td>51598</td>
            <td>48156</td>
            <td>1.071476</td>
            <td>0.6</td>
            <td>5364</td>
            <td>277627</td>
            <td>1.932089</td>
            <td>2.2</td>
            <td>5380443</td>
            <td>73.27</td>
            <td>15.28</td>
            <td>2279.0</td>
            <td>1700.5</td>
            <td>18.2</td>
            <td>2.14</td>
            <td>0.6</td>
            <td>91.592666</td>
            <td>8.407334</td>
            <td>5.478743</td>
            </tr>
            <tr>
            <th>4</th>
            <td>2015</td>
            <td>7.0</td>
            <td>Minnesota</td>
            <td>MN</td>
            <td>MRO</td>
            <td>East North Central</td>
            <td>1.2</td>
            <td>warm</td>
            <td>2015-07-18</td>
            <td>02:00:00</td>
            <td>2015-07-19</td>
            <td>07:00:00</td>
            <td>severe weather</td>
            <td>NaN</td>
            <td>NaN</td>
            <td>1740.0</td>
            <td>250.0</td>
            <td>250000.0</td>
            <td>13.07</td>
            <td>10.16</td>
            <td>7.74</td>
            <td>10.43</td>
            <td>2028875.0</td>
            <td>2161612.0</td>
            <td>1777937.0</td>
            <td>5970339.0</td>
            <td>33.982576</td>
            <td>36.205850</td>
            <td>29.779498</td>
            <td>2374674</td>
            <td>289044</td>
            <td>9812</td>
            <td>2673531</td>
            <td>88.821637</td>
            <td>10.811320</td>
            <td>0.367005</td>
            <td>54431</td>
            <td>49844</td>
            <td>1.092027</td>
            <td>1.7</td>
            <td>4873</td>
            <td>292023</td>
            <td>1.668704</td>
            <td>2.2</td>
            <td>5489594</td>
            <td>73.27</td>
            <td>15.28</td>
            <td>2279.0</td>
            <td>1700.5</td>
            <td>18.2</td>
            <td>2.14</td>
            <td>0.6</td>
            <td>91.592666</td>
            <td>8.407334</td>
            <td>5.478743</td>
            </tr>
        </tbody>
    </table>
</div>

### 4.

 From the outage dataframe, two separate dataframes were created from this cleaned data that would be used throughout the rest of the research process. First is grouped_state, which has columns: 'MEAN.POP', 'MEAN.POP.URBAN', 'MEAN.GSP $', and 'OUTAGES.POP.NORM', 'W or E'. Each row in grouped_state is a state. Grouped by POSTAL.CODE.

- MEAN.POP: The average population for each state over the instances of power outages. Derived from POPULATION
- MEAN.POP.URBAN: Average percentage of the state's population that is urban over the instances of power outages. Derived from POPPCT_UC.
- MEAN.GSP $: Average value of a given state's GSP over the instances of power outages
- OUTAGES.POP.NORM: The number of power outages per 100,000 people for the given dataset. 
- W or E: Specifies if the state is in the West ('Southwest', 'West', 'Northwest', 'West North Central') or in the East ('Southeast','Northeast','East North Central'). Derived from CLIMATE.REGION


The second dataframe was grouped_state_no_outliers, which was identical to grouped_state but without Delaware and Washington DC. These two states were taken out particularly because when visualized, they are clear outliers. Delaware was an outlier for the number of power outages that occurred, and Washington DC was an outlier for the GSP as shown in the plot below.

<div style="display: flex; justify-content: center;">
    <iframe src="assets/outliers_plot.html" width=1000 height=400 frameBorder=0></iframe>
</div>

The head of grouped_state and grouped_state_no_outliers is below (they have the same head):

<div style ="width: 480 px; overflow-x: auto;">
    <table class="dataframe">
        <thead>
            <tr style="text-align: right;">
            <th></th>
            <th>POSTAL.CODE</th>
            <th>NUMBER.OUTAGES</th>
            <th>MEAN.POP</th>
            <th>MEAN.POP.URBAN</th>
            <th>OUTAGES.POP.NORM</th>
            <th>MEAN.GSP $</th>
            <th>W or E</th>
            </tr>
        </thead>
        <tbody>
            <tr>
            <th>0</th>
            <td>AK</td>
            <td>1</td>
            <td>6.279630e+05</td>
            <td>21.56</td>
            <td>0.159245</td>
            <td>57401.000000</td>
            <td>None</td>
            </tr>
            <tr>
            <th>1</th>
            <td>AL</td>
            <td>6</td>
            <td>4.648740e+06</td>
            <td>10.39</td>
            <td>0.129067</td>
            <td>35446.833333</td>
            <td>East</td>
            </tr>
            <tr>
            <th>2</th>
            <td>AR</td>
            <td>25</td>
            <td>2.924665e+06</td>
            <td>16.62</td>
            <td>0.854799</td>
            <td>35929.280000</td>
            <td>None</td>
            </tr>
            <tr>
            <th>3</th>
            <td>AZ</td>
            <td>28</td>
            <td>6.321252e+06</td>
            <td>9.74</td>
            <td>0.442950</td>
            <td>38952.964286</td>
            <td>West</td>
            </tr>
            <tr>
            <th>4</th>
            <td>CA</td>
            <td>210</td>
            <td>3.714503e+07</td>
            <td>5.22</td>
            <td>0.565352</td>
            <td>53212.323810</td>
            <td>West</td>
            </tr>
        </tbody>
    </table>
</div>


## Univariate Analysis

The following plots show how the Gross State Product (GSP) and theoutage duration is distributed for each large power outage. It can be seen that the large majority of power outages occurred in states with GSP of less than 100k, but there are power outages with GSP of over 150k. All of these power outages are in Washington DC, where the GSP is significantly higher than any state. Washington DC was excluded as an outlier in most future calculations. Additionally, the vast majority of power outages lasted a relatively short amount of time, but there are some that lasted weeks.

<div style="display: flex; justify-content: center;">
    <iframe src="assets/Univarite_plot.html" width=1000 height=600 frameBorder=0></iframe>
</div>


## Bivariate Analysis

This plot is a visualization of OUTAGES.POP.NORM, which is a column from grouped_state_no_outliers. It contains an observation for each state on how many power outages there were per 100,000 people. It should be noted that outliers (DE and DC) were removed to allow better visualization and analysis. 

<div style="display: flex; justify-content: center;">
    <iframe src="assets/Bivariate_plot.html" width=1000 height=600 frameBorder=0></iframe>
</div>
From this plot it can be seen that the states with an above average number of power outagese per 100,000 residents are often located near the coast, or in the south. This could be a result of the more extreme weather in these areas. Though, none of these inferences are conclusive.

## Interesting Aggregates

The following pivot table is used to compare the average power outage duration in each region of the US with the cause of the given power outage. This can be used to infer how well regional support sources are able to recover the power grid, or how severly the power grid was damaged by a given storm. It was created by finding the mean value of power outage durate for each region by each power outage cause. 

<div style ="width: 480 px; overflow-x: auto;">
    <table class="dataframe">
        <thead>
            <tr style="text-align: right;">
            <th>CAUSE.CATEGORY</th>
            <th>equipment failure</th>
            <th>fuel supply emergency</th>
            <th>intentional attack</th>
            <th>islanding</th>
            <th>public appeal</th>
            <th>severe weather</th>
            <th>system operability disruption</th>
            </tr>
            <tr>
            <th>CLIMATE.REGION</th>
            <th></th>
            <th></th>
            <th></th>
            <th></th>
            <th></th>
            <th></th>
            <th></th>
            </tr>
        </thead>
        <tbody>
            <tr>
            <th>Central</th>
            <td>5.366667</td>
            <td>167.254167</td>
            <td>5.767647</td>
            <td>2.088889</td>
            <td>23.500000</td>
            <td>54.166792</td>
            <td>44.920000</td>
            </tr>
            <tr>
            <th>East North Central</th>
            <td>440.588889</td>
            <td>566.187500</td>
            <td>39.600833</td>
            <td>0.016667</td>
            <td>12.216667</td>
            <td>73.913622</td>
            <td>43.500000</td>
            </tr>
            <tr>
            <th>Northeast</th>
            <td>3.596667</td>
            <td>243.826190</td>
            <td>3.266412</td>
            <td>14.683333</td>
            <td>44.250000</td>
            <td>73.831714</td>
            <td>12.891667</td>
            </tr>
            <tr>
            <th>Northwest</th>
            <td>11.700000</td>
            <td>0.016667</td>
            <td>6.230196</td>
            <td>1.222222</td>
            <td>14.966667</td>
            <td>80.633333</td>
            <td>2.350000</td>
            </tr>
            <tr>
            <th>South</th>
            <td>4.929630</td>
            <td>291.375000</td>
            <td>5.426786</td>
            <td>8.225000</td>
            <td>19.399603</td>
            <td>73.189151</td>
            <td>14.434568</td>
            </tr>
            <tr>
            <th>Southeast</th>
            <td>9.241667</td>
            <td>0.000000</td>
            <td>8.411111</td>
            <td>0.000000</td>
            <td>47.756667</td>
            <td>44.376006</td>
            <td>2.821875</td>
            </tr>
            <tr>
            <th>Southwest</th>
            <td>1.896667</td>
            <td>1.266667</td>
            <td>4.427869</td>
            <td>0.033333</td>
            <td>37.916667</td>
            <td>192.881667</td>
            <td>5.487037</td>
            </tr>
            <tr>
            <th>West</th>
            <td>8.746825</td>
            <td>102.576667</td>
            <td>14.294624</td>
            <td>3.580952</td>
            <td>33.801852</td>
            <td>48.806219</td>
            <td>6.061111</td>
            </tr>
            <tr>
            <th>West North Central</th>
            <td>1.016667</td>
            <td>0.000000</td>
            <td>0.391667</td>
            <td>1.136667</td>
            <td>7.325000</td>
            <td>40.708333</td>
            <td>0.000000</td>
            </tr>
        </tbody>
    </table>
</div>

Specifically in this pivot table it can be seen that the East North Central Region had by far the longest periods without power compared to the other regions. This is mainly from power outages caused by equipment failure and fuel supply emergencies. These same causes played much less of a role in the length of power outages for most other regions. It can be seen that the southwest region had the longest average power outage duration for sever weather storms. This could likely be due to fires and wind destroying power plants, though it is not conclusive.

# Assessment of Missingness

This section highlights the process and findings of the missingness of various columns, and the dependency of this missingness.

## NMAR Analysis

I believe that the missingness of the ANOMALY.LEVEL column is not missing at random (NMAR). The missingness may depend on the number of customers affected by the given power outage (CUSTOMERS.AFFECTED), or the percentage of the total population of the U.S. state represented by the population of the urban clusters (POPPCT_UC). The following plots help to explain the missingness of ANOMALY.LEVEL.

<div style="display: flex; justify-content: center;">
    <iframe src="assets/missingness_plot.html" width=1000 height=500 frameBorder=0></iframe>
</div>

To determine if ANOMALY.LEVEL was dependent on either POPPCT_UC or CUSTOMERS.AFFECTED a permutation test was performed, by shuffling the ANOMALY.LEVEL column and finding the average of the other column with and without ANOMALY.LEVEL missing (POPPCT_UC or CUSTOMERS.AFFECTED). The test statistic that was used was a difference in group means. From the plot it can be seen that the ANOMALY.LEVEL column is MAR dependent on POPPCT_UC, but not on CUSTOMERS.AFFECTED. This was based on the p-value of 0.02 and 0.49 respectively, where the significance threshold of 0.05 was applied. 

- ANOMALY.LEVEL MAR dependent on POPPCT_UC (P-value: 0.02)
- ANOMALY.LEVEL not dependent on CUSTOMERS.AFFECTED (P-value: 0.5)

# Hypothesis Testing

## Question

Does the Number of Power Outages per 100,000 people from States in the West and the East Come from the same Distribution?

## Permutation Test

Null Hypothesis: The number of power outages per capita from states in the West and in the East comes from the same distribution.

Alternate Hypothesis: The number of power outages per capita from states in the West and in the East comes from different distributions.

Significant Level: 0.05. Type I error is not consequential. Scientific standard level of significance. 

Test Statistic: Difference of means of power outages per capita from the West and East. This is an effective statistic because it compares the central tendency of the two distributions, which is the main concern for the question.

Relevant Columns: This test was performed with the grouped_state_no_outliers data set, focusing on the 'OUTAGES.POP.NORM' and 'W or E' columns.

Process: The OUTAGES.POP.NORM column was shuffled 10,000 times and each shuffle the difference of means between the East and West groups was calculated to form the test statistic distribution.

<div style="display: flex; justify-content: center;">
    <iframe src="assets/perm_plot.html" width=1000 height=600 frameBorder=0></iframe>
</div>

P-value: 0.41

Conclusion: Fail to Reject the null hypothesis that power outages per 100,000 people from states in the West and in the East come from the same distribution.
