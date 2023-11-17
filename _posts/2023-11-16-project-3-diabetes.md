## ST 558 Project 3 -- Analyzing Diabetes Data

## The Project

For this project, I worked with another ST 558 student, Autumn Locklear, on conducting EDA and creating candidate models for the classification task of an individual having diabetes based on a number of categorical survey responses (i.e. pertaining to diet, activity level, smoking habits, etc.) and physiological information (e.g., Age, Sex).

A *number* of models were considered for this classification task, including (but, as we worked through the project, not limited to)

- Logistic Regression

- LASSO Regression

- Random Forests

- Classification Trees

- Naive Bayes Classifiers

- Flexible Discriminant Analysis (FDA)

The following links will take the reader to a [custom landing page](https://halljc76.github.io/ST558_Project_3/) for the project, including analysis on the diabetes dataset after partitioning the data based on education level. Furthermore, the [GitHub repository](https://github.com/halljc76/ST558_Project_3) is linked for interested users' perusal.



## Takeaways

**What would I do differently?** For myself, this came down to the prioritization of the project -- working on it earlier would have greatly benefitted myself and my groupmates, although we were able to come together in crunch time to achieve our goals! More tangibly, however, would be the exploratory data analysis -- my contributions included a number of summary statistics detailing univariate relationships amongst the data, but I feel that perhaps some additional analysis akin to PCA would have been more interesting. (See below on the potential use of parallelization to speed up the knitting process.)

**What was the most difficult part?** *Knitting.* (Ironically, I am knitting the final analyses as of typing this document.) Rather than difficult, per se, this part was especially tedious, although potentially using the `foreach` and `doParallel` packages to perform parallel computing may have saved us some time, had we had more analyses to conduct.

**What are the biggest takeaways from this project?** 

1. *Model fitting is easier said than done.* For starters, determining what predictors to include in potential candidate models, whether by intuition, curiosity, or a more robust variable selection method, is certainly no lighthearted task. Incorporating interaction terms is especially difficult if methods such as stepwise regression are used, and so the inclusion of these terms was attributed to my curiosity and potential intuitive understanding of what might put someone at risk for diabetes (though I am in no way a public health expert).

2. *All models are not created equal... in terms of speed.* This, obviously, goes without saying, but developing patience and faith in the model building was an interesting aspect of this project -- random forests, for example, are notoriously slow in comparison to other methods, but this in no way detracts from their capabilities (although it appears Logistic Regression and FDA are holding their own in our final model selections)!