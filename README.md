Author: Matt Dulansky

The Exploratory Data analysis for this project can be found here:
(https://mdulansk.github.io/power-outage-repo/)


# Framing the Problem

The following Columns are features used for the multiclassification prediction at use here.

- MONTH: Indicates the month when the outage event occurred
- CLIMATE.REGION: U.S. Climate regions as specified by National Centers for Environmental Information (nine climatically consistent regions in continental U.S.A.)
- CUSTOMERS.AFFECTED: Number of customers affected by the power outage event
- PC.REALGSP.STATE: Per capita real gross state product (GSP) in the U.S. state (measured in 2009 chained U.S. dollars)

The response variable description is as follows:

- CAUSE.CATEGORY.DETAIL: Detailed description of the event categories causing the major power outages (i.e Wnter Storm, Hurricane, fire etc.)

This model serves as a powerful tool in situations when a power outage has occurred, causing widespread impact, yet the source remains unidentified. It utilizes crucial variables such as the affected US region, the scale of the outage as indicated by the number of customers affected, the state's economic vitality, and the month of occurrence. With these inputs, our model can accurately predict the root cause of the outage, providing invaluable information for decision-making and timely response.

The performance index used to measure the success of the models presented below is accuracy:

<script type="text/javascript" async
  src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.5/MathJax.js?config=TeX-MML-AM_CHTML">
</script>

<p>
\\[ \text{Accuracy} = \frac{\text{Number of correct predictions}}{\text{Total number of predictions}} \\]
</p>
