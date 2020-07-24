.. -*- mode: rst -*-

**scikit-learn** is a Python module for machine learning built on top of
SciPy and is distributed under the 3-Clause BSD license.

The project was started in 2007 by David Cournapeau as a Google Summer
of Code project, and since then many volunteers have contributed. See
the `About us <https://scikit-learn.org/dev/about.html#authors>`__ page
for a list of core contributors.

It is currently maintained by a team of volunteers.

Website: https://scikit-learn.org

**Adding new functionality**
=============================

**Disclaimer -- Current function support on binary input classification**

The function will print out the terminology and derivation from a confusion matrix

In scikit-learn we have to call different functions seperatly for various deriavtion as Accuracy, F1 score, Precision, Recall and many other.

By calling this function we can get 16 metrics which can be used accoriding to the scenarios.


**Following terminology and derivation would be printed**
      *False Positive / Type I error* 
      *False Negative / Type II error*
      *Sensitivity / Recall / Hit Rate / True Positive Rate (TPR)*
      *Specificity / Selectivity / True Negative Rate (TNR)*
      *Precision / Positive Predictive Value (PPV)*
      *Negative Predictive Value (NPV)*
      *Miss Rate / False Negative Rate (FNR)*
      *Fall-out / False Positive Rate (FPR)*
      *False Discovery Rate (FDR)*
      *False Omission Rate (FOR)*
      *Threat Score / Critical Success Index (CSI)*
      *Accuracy (ACC)*
      *F1 Score*
      *Matthews Correlation Coefficient (MCC)*
      *Informedness / Bookmaker Informediness (BM)*
      *Markedness (MK)*

           
    **Example**
    --------
    from sklearn.metrics import show_confusion_matrix_desc
    y_true = [0, 1, 1, 1, 0, 1, 0]
    y_pred = [0, 1, 1, 0, 0, 0, 1]
    show_confusion_matrix_desc(y_true, y_pred):     
                  
   >>>INFORMATION 
      ------------ 
      Type I error =  2 
      Type II error =  1 
      Sensitivity / Recall / Hit Rate / True Positive Rate (TPR) = 0.75 
      Specificity / Selectivity / True Negative Rate (TNR) =  0.5 
      Precision / Positive Predictive Value (PPV) =  0.6 
      Negative Predictive Value (NPV) =  0.6666666666666666 
      Miss Rate / False Negative Rate (FNR) =  0.25 
      Fall-out / False Positive Rate (FPR) =  0.5 
      False Discovery Rate (FDR) =  0.4 
      False Omission Rate (FOR) =  0.3333333333333333 
      Threat Score / Critical Success Index (CSI) =  0.5 
      Accuracy (ACC) =  0.625 
      F1 Score =  0.6666666666666666 
      Matthews Correlation Coefficient (MCC) =  0.2581988897471611 
      Informedness / Bookmaker Informediness (BM) =  0.25 
      Markedness (MK) =  0.2666666666666666
      
      
    *References*
    ----------
    .. [1]  Balayla, Jacques (2020). "Prevalence Threshold and the Geometry of Screening Curves". 
            arXiv:2006.00398.
    .. [2]  `Wikipedia entry for the confusion-matrix
           <https://en.wikipedia.org/wiki/Confusion_matrix>`_  
     
     
     **FUTURE WORK**
     =============================
        1) Currently it is limited to binary classification, in future it can be scaled for multiclass classification.
        2) More Functionality can be added
     
           
