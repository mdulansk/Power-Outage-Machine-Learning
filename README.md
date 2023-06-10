Author: Matt Dulansky

The Exploratory Data analysis for this project can be found here:
(https://mdulansk.github.io/power-outage-repo/)


# Framing the Problem

This model serves as a powerful tool in situations when a power outage has occurred, causing widespread impact, yet the source remains unidentified. It utilizes crucial variables such as the affected US region, the scale of the outage as indicated by the number of customers affected, the state's economic vitality, and the month of occurrence. With these inputs, our model is trained to predict the root cause of the outage, providing invaluable information for decision-making and timely response.

The following columns are untransformed features used for the multiclass prediction at use here.

- MONTH: (Quantitative Discrete - order is unimportant) Indicates the month when the outage event occurred
- CLIMATE.REGION: (Nominal) U.S. Climate regions as specified by National Centers for Environmental Information (nine climatically consistent regions in continental U.S.A.)
- CUSTOMERS.AFFECTED: (Quantitative Discrete) Number of customers affected by the power outage event
- PC.REALGSP.STATE: (Discrete Quantitative) Per capita real gross state product (GSP) in the U.S. state (measured in 2009 chained U.S. dollars)

The response variable description is as follows:

- CAUSE.CATEGORY.DETAIL: (Nominal) Detailed description of the event categories causing the major power outages (i.e Wnter Storm, Hurricane, fire etc.)


The performance index used to measure the success of the models presented below is accuracy:

$$
\text{Accuracy} = \frac{\text{Number of correct predictions}}{\text{Total number of predictions}}
$$

The start of the training data can be seen here before it is transformed for fitting can be seen here:

<div style ="width: 480 px; overflow-x: auto;">
    <body><table class="dataframe">
        <thead>
            <tr style="text-align: right;">
            <th></th>
            <th>MONTH</th>
            <th>CLIMATE.REGION</th>
            <th>PC.REALGSP.STATE</th>
            <th>CUSTOMERS.AFFECTED</th>
            </tr>
            </thead>
            <tbody>
            <tr>
            <th>2</th>
            <td>10.0</td>
            <td>East North Central</td>
            <td>50447</td>
            <td>70000.0</td>
            </tr>
            <tr>
            <th>3</th>
            <td>6.0</td>
            <td>East North Central</td>
            <td>51598</td>
            <td>68200.0</td>
            </tr>
            <tr>
            <th>5</th>
            <td>11.0</td>
            <td>East North Central</td>
            <td>50447</td>
            <td>60000.0</td>
            </tr>
            <tr>
            <th>6</th>
            <td>7.0</td>
            <td>East North Central</td>
            <td>50447</td>
            <td>63000.0</td>
            </tr>
            <tr>
            <th>7</th>
            <td>6.0</td>
            <td>East North Central</td>
            <td>52445</td>
            <td>300000.0</td>
            </tr>
        </tbody>
    </table></body>
</div>

The Format of the Variable can then be seen here:

<div style ="width: 480 px; overflow-x: auto;">
    <html><body><table class="dataframe">
        <thead>
            <tr style="text-align: right;">
            <th></th>
            <th>CAUSE.CATEGORY.DETAIL</th>
            </tr>
            </thead>
            <tbody>
            <tr>
            <th>2</th>
            <td>heavy wind</td>
            </tr>
            <tr>
            <th>3</th>
            <td>thunderstorm</td>
            </tr>
            <tr>
            <th>5</th>
            <td>winter storm</td>
            </tr>
            <tr>
            <th>6</th>
            <td>tornadoes</td>
            </tr>
            <tr>
            <th>7</th>
            <td>thunderstorm</td>
            </tr>
        </tbody>
    </table></body></html>
</div>
