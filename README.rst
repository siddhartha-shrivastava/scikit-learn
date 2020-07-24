.. -*- mode: rst -*-

|Azure|_ |Travis|_ |Codecov|_ |CircleCI|_ |PythonVersion|_ |PyPi|_ |DOI|_

.. |Azure| image:: https://dev.azure.com/scikit-learn/scikit-learn/_apis/build/status/scikit-learn.scikit-learn?branchName=master
.. _Azure: https://dev.azure.com/scikit-learn/scikit-learn/_build/latest?definitionId=1&branchName=master

.. |Travis| image:: https://api.travis-ci.org/scikit-learn/scikit-learn.svg?branch=master
.. _Travis: https://travis-ci.org/scikit-learn/scikit-learn

.. |Codecov| image:: https://codecov.io/github/scikit-learn/scikit-learn/badge.svg?branch=master&service=github
.. _Codecov: https://codecov.io/github/scikit-learn/scikit-learn?branch=master

.. |CircleCI| image:: https://circleci.com/gh/scikit-learn/scikit-learn/tree/master.svg?style=shield&circle-token=:circle-token
.. _CircleCI: https://circleci.com/gh/scikit-learn/scikit-learn

.. |PythonVersion| image:: https://img.shields.io/badge/python-3.6%20%7C%203.7%20%7C%203.8-blue
.. _PythonVersion: https://img.shields.io/badge/python-3.6%20%7C%203.7%20%7C%203.8-blue

.. |PyPi| image:: https://badge.fury.io/py/scikit-learn.svg
.. _PyPi: https://badge.fury.io/py/scikit-learn

.. |DOI| image:: https://zenodo.org/badge/21369/scikit-learn/scikit-learn.svg
.. _DOI: https://zenodo.org/badge/latestdoi/21369/scikit-learn/scikit-learn

.. image:: doc/logos/scikit-learn-logo.png
  :target: https://scikit-learn.org/

<p color='red'> DISCLAIMER: </p> This library is built on top of a well established scikit learn library. You can check the original library link :https://github.com/scikit-learn/scikit-learn

**scikit-learn** is a Python module for machine learning built on top of SciPy and is distributed under the 3-Clause BSD license. The project was started in 2007 by David Cournapeau as a Google Summer
of Code project, and since then many volunteers have contributed. See
the `About us <https://scikit-learn.org/dev/about.html#authors>`__ page
for a list of core contributors. It is currently maintained by a team of volunteers. Website: https://scikit-learn.org

**Introduction  of New Functionalities**
------------------------------------------

**1. F-Cost**
---------------

`fcost_score` function is introduced to `sklearn.metrics` module.
The F-Cost score is the product of cost function to the weighted harmonic mean of precision and recall, trying to reach its optimal value.

This score accounts the **cost** for identifying True Values
from Predicted Values. These costs are related to False Positive (FP), False Negative (FN) and True Positive (TP) values. Assuming user is interested in identifying positives, we have chosen F-Score as our basis function.

The F1 score (also F-score or F-measure) is a measure of a test's accuracy.  It considers both the precision 'P' and the recall 'R' of the test to compute the score 

The `beta` parameter determines the weight of recall in the combined score. `beta < 1` lends more weight to precision, while `beta > 1` favors recall (`beta -> 0` considers only precision, `beta -> +inf` only recall).

- `beta = 1`, which assumes the distribution is equally distributed.
- `beta < 1`, A smaller beta value, e.g 0.5, gives more weight to precision and less to recall, 
- `beta > 1`, A larger beta value,e.g 2.0, gives less weight to precision and more weight to recall in the calculation of the score.

It is a useful metric to use when both precision and recall are important but slightly more attention is needed on one or the other, such as when false negatives are more important than false positives.

The F-cost score comes in role to assess the cost associated with missing critical elements, which varies from one requirement to other.

Understanding with Examples
-------------------------------------------------------------
**To Diagnose Or Not To Diagnose is the Question**

A group of doctors are conducting tests, with a pharma company, on diagnosing a rare and chronic disease which has occurrence probability of 0.2%. They are focused on **High recall**.

To optimize their model, the pharma company can choose the beta value and they would associate a cost factor with  FP, FN and TP. Since they are focussed on finding the rare disease, lets assume the following can be the cost associated:

   - `cost_FP = 5`
   - `cost_FN = 100`
   - `cost_TP = 0.01`

Here the actual values are not important (as they are chosen by user according to their requirements, but the ratio between the cost should be in focus) Since, the pharma company can afford to have some False Positive (FP), which they can eventually re-test, but cannot afford to miss False Negative.

**Hello Sir! We are selling insurance at discounted rate.**

*Lets take another example*, suppose you own a telemarketing company, which sells insurance to customers, and there are 20 employees involved with each of them can call 10 customers/day i.e total of 6000 customer/month (30 day month). 
And Each month they call customers of particular region.(and we know there are many regions for this domain)
Now, lets say out of the 6000 customers the team can reach we define,  

- `TP --> Customers who needed insurance and recieved a call.`
- `TN --> Customers who don't need insurance and didn't recieve a call.`
- `FP --> Customers who don't need insurance and recieved a call.`
- `FN --> Customers who needed insurance and didn't recieve a call.`

Selling insurance is a competitive business and you have many other rivals, who are doing the same thing. With limited number of man power and _infinite_ customers out there you would need **high precision** to have conversion rate.

Therefore you want to develop a cost model which will penalize the FP heavilly, FN lightly and TP also lightly and choose beta accordingly.

*Once we have that we can calculate the f_cost and in further steps it can be optimized.*

Similarly, any process which has very high cost to perform but is not critical, will have high cost for FP, and low cost for FN. **High Precision**.

    - `cost_FP  =  100`
    - `cost_FN  = 05`
    - `cost_TP  = 0.1`

FUTURE WORK
---------------
Thus we can think of many scenarios, when we can choose the cost function according to requirements, and then in further step we can optimize the threshold for binary classification, thus minimizing the cost associated.

*e.g* For a certain function with variables (TP,FP,FN,TN)

    - `beta    = 3.5`
    - `cost_FP =  100`
    - `cost_FN =  05`
    - `cost_TP = 0.1`

Therefore, for a given beta function, and  `cost_FP`, `cost_FN`, `cost_TP` which are chosen according to requirements, we will have

    cost_precision = (cost_TP*TP)/((cost_TP * TP) + (cost_FP * FP))
    
    cost_recall = (cost_TP*TP) / ((cost_TP * TP) + (cost_FN * FN))

And hence we introduce, **F-Cost Score** 

    fcost_score = ((1 + beta^2)*(cost_precision * cost_recall))/((beta^2 * cost_precision) * (cost_recall))

Thus we can optimize the F-cost score by varying the threshold, thus varying FP,FN and TP.

--------------------------------------------------------------------------------

**2. show_confusion_matrix_desc**
----------------------------------

**Disclaimer -- Current function support only binary input classification**

The function will print out the terminology and derivation from a confusion matrix.

In scikit-learn we have to call different functions separately for various derivation as Accuracy, F1 score, Precision, Recall and many other.

By calling this function we can get **16** metrics which can be used according to the scenarios, also we get a sense of complete picture.

**Following terminology and derivation would be printed**

      *1. False Positive / Type I error* 
      
      *2. False Negative / Type II error*
      
      *3. Sensitivity / Recall / Hit Rate / True Positive Rate (TPR)*
      
      *4. Specificity / Selectivity / True Negative Rate (TNR)*
      
      *5. Precision / Positive Predictive Value (PPV)*
      
      *6. Negative Predictive Value (NPV)*
      
      *7. Miss Rate / False Negative Rate (FNR)*
      
      *8. Fall-out / False Positive Rate (FPR)*
      
      *9. False Discovery Rate (FDR)*
      
      *10. False Omission Rate (FOR)*
      
      *11. Threat Score / Critical Success Index (CSI)*
      
      *12. Accuracy (ACC)*
      
      *13. F1 Score*
      
      *14. Matthews Correlation Coefficient (MCC)*
      
      *15. Informedness / Bookmaker Informediness (BM)*
      
      *16. Markedness (MK)*
      
    
**References**
---------------

[1]  Balayla, Jacques (2020). "Prevalence Threshold and the Geometry of Screening Curves". arXiv:2006.00398.

[2]  `Wikipedia entry for the confusion-matrix <https://en.wikipedia.org/wiki/Confusion_matrix>`_  


**FUTURE WORK**
----------------
1) Currently it is limited to binary classification, in future it can be scaled for multiclass classification.

2) More derivations can be added


    
