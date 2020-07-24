**scikit-learn** is a Python module for machine learning built on top of
SciPy and is distributed under the 3-Clause BSD license.

The project was started in 2007 by David Cournapeau as a Google Summer
of Code project, and since then many volunteers have contributed. See
the `About us <https://scikit-learn.org/dev/about.html#authors>`__ page
for a list of core contributors.

It is currently maintained by a team of volunteers.

Website: https://scikit-learn.org

**Added New Functionality**
================================

from sklearn.metrics import fcost_score

fcost_score function is added in sklearn.metrics

The F-Cost score is the product of cost function to the weighted harmonic mean of precision and recall,
trying to reach its optimal value of positive real number and its worst 
value at 0.

This score accounts the **cost** for identifying True Values
from Predicted Values. These costs are related to False Positive (FP), False Negative (FN) and True Positive (TP) values.

--True Negative(TN) is not taken as it is not involved in either Precision or Recall.
The `beta` parameter determines the weight of recall in the combined
score. ``beta < 1`` lends more weight to precision, while ``beta > 1``
favors recall (``beta -> 0`` considers only precision, ``beta -> +inf``
only recall).

The F1 score (also F-score or F-measure) is a measure of a test's accuracy. 
It considers both the precision 'P' and the recall 'R' of the test to compute the score 
(Source -- Wiki)

beta = 1, which assumes the distribution is equally distributed.
A smaller beta value, e.g 0.5, gives more weight to precision and less to recall, 
whereas a larger beta value,e.g 2.0, gives less weight to precision and more weight to recall in the calculation of the score.
It is a useful metric to use when both precision and recall are important but slightly more attention is needed on one or the other, 
such as when false negatives are more important than false positives


The F-cost score comes in role to assess the cost associated with missing critical elements, which varies from one requirement to other.

**Let's understand it with some examples:**
-------------------------------------------------------------
A pharmaceutical company conducting test on rare disease which has occurance probabilty of 0.2% will want "High recall".
and in order to optimize their model, the pharma company can choose the beta value and they would associate a cost factor with  FP, FN and TP.
since they are focussed on finding the rare disease, there following can be the cost associated:

- cost_FP = 5
- cost_FN = 100
- cost_TP = 0.01

Here the actual values are not important (as they are chosed by user according to their requirements, but the ratio between the cost should be in focus)
Since, the pharma company can afford to have some False Positive (FP), which they can eventually re-test, but having False Negative would be costly for them since the probabilty of the disease is 0.2%.


*Lets take another example*, suppose you own a telemarketing company, who sells insurance to customers, and there are 20 employees involved with each of them can call 10 customers/day i.e total of 6000 customer/month (30 day month). 
And Each month they call customers of particular reigon.(for sake of simplicity, there are 5 reigons in this example)
Now, lets say out of the 6000 customers,  

- TP --> Customers who needed insurance and recieved a call.
- TN --> Customers who don't need insurance and didn't recieve a call.
- FP --> Customers who don't need insurance and recieved a call.
- FN --> Customers who needed insurance and didn't recieve a call.

and since, selling insurance is a competitive business and you have many other rivals, who are doing the same thing.
So, here we need **high recall**
Therefor you want to develop a cost model which will penalize the FN heavilly, FP lightly and TP also lightly and choose beta accordingly.
*Once we have that we can calculate the f_cost and in further steps it can be optimized.*

Similary, any process which has very high cost to perform but is not critical, will have high cost for FP, and low cost for FN. **High Precison**.

- cost_FP =  100
- cost_FN = 05
- cost_TP  = 0.1


**FUTURE WORK**
===================

Thus we can think of many scenarios, when we can choose the cost function according to requirements, and then in further step we can optimze the threshold, thus minimizing the cost associated.

*e.g*
For a certain function

- cost_FP =  100
- cost_FN =  05
- cost_TP  = 0.1

therefore, for a given beta function, and  cost_FP, cost_FN, cost_TP which are chosen according to requirements, we will have

the **cost_precision** would be = (cost_TP*TP)/((cost_TP * TP) + (cost_FP * FP))

the **cost_recall** would be = (cost_TP*TP) / ((cost_TP * TP) + (cost_FN * FN))

We can use, **Fcost_score** = ((1 + beta^2)*(cost_precision * cost_recall))/((beta^2 * cost_precision) * (cost_recall))

Thus we can optimize the Fcost_score by varying the threshold, thus varying FP,FN and TP.



