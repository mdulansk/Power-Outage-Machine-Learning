Author: Matt Dulansky

The Exploratory Data analysis for this project can be found here:
(https://mdulansk.github.io/power-outage-repo/)


# Framing the Problem

This model serves as a powerful tool in situations when a power outage has occurred, causing widespread impact, yet the source remains unidentified. It utilizes crucial variables such as the affected US region, the scale of the outage as indicated by the number of customers affected, the state's economic vitality, and the month of occurrence. With these inputs, our model is trained to predict the root cause of the outage, providing invaluable information for decision-making and timely response.

The performance index used to measure the success of the models presented below is accuracy:

![Accuracy Formula](/assets/AccuracyEquation.png)

The data used for training was 608 observations long after removing rows that were missing values in any of the feature or response columns. The test data was 152 observations. The start of the training data can be seen here before it is transformed for fitting can be seen here:

<div style ="width: 480 px; overflow-x: auto;">
    <body><table class="dataframe">
        <thead>
            <tr style="text-align: right;">
            <th>MONTH</th>
            <th>CLIMATE.REGION</th>
            <th>PC.REALGSP.STATE</th>
            <th>CUSTOMERS.AFFECTED</th>
            </tr>
            </thead>
            <tbody>
            <tr>
            <td>10.0</td>
            <td>East North Central</td>
            <td>50447</td>
            <td>70000.0</td>
            </tr>
            <tr>
            <td>6.0</td>
            <td>East North Central</td>
            <td>51598</td>
            <td>68200.0</td>
            </tr>
            <tr>
            <td>11.0</td>
            <td>East North Central</td>
            <td>50447</td>
            <td>60000.0</td>
            </tr>
            <tr>
            <td>7.0</td>
            <td>East North Central</td>
            <td>50447</td>
            <td>63000.0</td>
            </tr>
            <tr>
            <td>6.0</td>
            <td>East North Central</td>
            <td>52445</td>
            <td>300000.0</td>
            </tr>
        </tbody>
    </table></body>
</div>

A sample of the response variable can be seen here:

<div style ="width: 480 px; overflow-x: auto;">
    <html><body><table class="dataframe">
        <thead>
            <tr style="text-align: right;">
            <th>CAUSE.CATEGORY.DETAIL</th>
            </tr>
            </thead>
            <tbody>
            <tr>
            <td>heavy wind</td>
            </tr>
            <tr>
            <td>thunderstorm</td>
            </tr>
            <tr>
            <td>winter storm</td>
            </tr>
            <tr>
            <td>tornadoes</td>
            </tr>
            <tr>
            <td>thunderstorm</td>
            </tr>
        </tbody>
    </table></body></html>
</div>

There are a total of 25 unique values in the entire response column, though many only very few or one time, and are never predicted by the model.

All of the feature and response data was split into training and test data, leaving 20% of the data for testing. All models were trained on the same data. 

# Baseline Model

In order to initially predict the cause of a power outage, a KNeighborsClassifier was used with n_neighbors = 10. This parameter was chosen rather arbitrary as this model was used to improve upon in further iterations.

## Features

The following columns are untransformed features used for the multiclass prediction at use here.

- MONTH: (Quantitative Discrete - order is unimportant) Indicates the month when the outage event occurred
- CLIMATE.REGION: (Nominal) U.S. Climate regions as specified by National Centers for Environmental Information (nine climatically consistent regions in continental U.S.A.)
- CUSTOMERS.AFFECTED: (Quantitative Discrete) Number of customers affected by the power outage event
- PC.REALGSP.STATE: (Discrete Quantitative) Per capita real gross state product (GSP) in the U.S. state (measured in 2009 chained U.S. dollars)

The response variable description is as follows:

- CAUSE.CATEGORY.DETAIL: (Nominal) Detailed description of the event categories causing the major power outages (i.e Wnter Storm, Hurricane, fire etc.)

## Encodings

In order to format these features to be setup for the KNEighborsClassifier only one transormation was performed. The CLIMATE.REGION feature is the only qualitative nominal feature. In order to make it quantitative for the model it was one hot encoded. The rest of the features were already quantitative, and for the baseline model they were left as is. 

## Performance

After training the baseline model on the training data, it was 40.8% accurate at predicting the testing split. This is not a very strongly performing model, it is better than random but is not very accurate at all. The following heatmap of the confusion matrix for this model can be seen here.

<div style="display: flex; justify-content: center;">
    <iframe src="assets/Baseline_Heatmap.html" width=1000 height=400 frameBorder=0></iframe>
</div>

The diagonal blocks on this heatmap are the occurrences where the model predicted the correct cause. It can be seen that the diagonal part of the heatmap is sparsly populated, but contains the darkest blocks. The model often predicts the same two causes repeatedly, but they are some of the most common causes so it performs decently accurately. There are a decent amount of mislabeled causes,  due to the lack of sufficient training data. Given new test data this model would perform best if the actual cause of the power outage from the new data is either a thunderstorm or vandalism. Though this response variable would not be known for the future unseen data. The realistic way to better improve this model would be to give it more training data to learn from and make better predictions off of.

# Final Model

The final model was chosen after optimizing the hyperparameters for two different models, a KNearestNeighbor and a DecisionTreeClassifier. They were both trainined on the same transformed data, but the KNearestNeighbor was ultimately chosen as the final model. 

## Feature Engineering

From the original features used in training the original KNearestNeighbors, most were transformed. First, the CUSTOMERS.AFFECTED column was broken into 5 quantiles. This is because the CUSTOMERS.AFFECTED column is a good measurement of the impact of the power outage. Given there are a discrete number of causes possible for a power outage, a feature that is able to capture the relative category of impact is useful in breaking down the data into more categorical chunks. The second feature that was engineered was the PC.REALGSP.STATE column. This was scaled using StandardScaler in order to standardize this column. This was done to help the convergence speed of the KNeighborsClassifier, as well as make the weights of the features more balanced. 

## Algorithm. 

A KNearestNeighbor classifier was used as the final predictive classifier model. The hyperparameters were chosen using a GridSearchCV from an extensive list of the reasonable hyperparameters to be used in this classification. The hyperparameters are as follows:

- metric: 'manhattan'
- n_neighbors: 21
- weights: 'distance'

## Results 

Compared to the baseline KNearestNeighbors model this model peformed at 55% accuracy on the testing split, a 15% increase in performance. This can largely be attributed for the transformation of the CUSTOMERS.AFFECTED column as well as the optimization of the hyperparameters in the creation of this model. The following heatmap of the confusion matrix for this model can be seen here.

<div style="display: flex; justify-content: center;">
    <iframe src="assets/heatmap.html" width=1000 height=400 frameBorder=0></iframe>
</div>

This heatmap can be directly compared with the heatmap of the baseline model. It can be seen that there are two more diagonal blocks that have high frequency. This shows that after adding new features and optimizing the hyperparameters the KNearestNeighbor classifier was effective at classifying thunderstorms, vandalism, hurricanes and winter storms. 


# Fairness Analysis
 
 The Fairness Analysis of this model was tested between power outages that occurred in the East vs the West of the United States. The information of East and West was derived from the CLIMATE.REGION column. The mapping of west to east from the CLIMATE.REGION column is shown below. 

 - West: 'Southwest', 'West', 'Northwest', 'West North Central'
 - East: 'Southeast','Northeast','East North Central'

## Hypothesis Testing

Null Hypothesis: The accuracy of the prediction from the KNearestNeighbor classifier is the same between power outages from the East and the West. 

Alternate Hypothesis: The accuracy of the prediction from the KNearestNeighbor classifier is different same between power outages from the East and the West. 

Significant Level: 0.05. Type I error is not consequential. Scientific standard level of significance. 

Test Statistic: Absoulte difference of accuracy between the East and the West. This is an effective statistic because it compares the central tendency of the two distributions, which is the main concern for the question.

Relevant Columns: This test was performed with the test data that was originally split off when the training and test data was created. The columns relevant in this analysis are all of the feature columns, and especially the CLIMATE.REGION column because it determines the group East or West for the power outage observation.

Process: The W or E column, which corresponds to the West or East mapping of the power outages was shuffled 10,000 times. Each shuffle the absolute difference of accuracy between the East and West groups was calculated to form the test statistic distribution.

<div style="display: flex; justify-content: center;">
    <iframe src="assets/perm_plot.html" width=1000 height=600 frameBorder=0></iframe>
</div>

P-value: 0.27

Conclusion: Fail to Reject the null hypothesis that the KNearestNeighbor classifier is the same between outages in the East and West. 