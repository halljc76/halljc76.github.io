## Variable Selection: What, Why, and How?

> "The greatest value of a picture is when it forces us to notice what we never expected to see." 
> - John W. Tukey

Referencing my last blog post [here](https://halljc76.github.io/2023/10/16/eda-what-why-how.html), suppose you,
now having conducted an EDA on this new dataset, must *choose* the 
variables/features to predict some response. While you might consider this a new,
unrelated task, your EDA is in-fact one piece of the puzzle! **Analyzing one's data without any response or goal in mind, other than to gain insight, is more effective in gaining an understanding of the data than context-less, arbitrary model creation!** 

The real question, naturally, is "Where do I go from here?" Now that I 
*understand* (to some degree) the data with which I am working, how do I find 
variables and transformations of variables that best predict my response? This 
idea, called **variable selection** in statistics, will be explored in this blog 
post.

### What is Meant by "Variable Selection?"

At a high level, **variable selection** (alternatively *feature* selection) is the process of identifying the most relevant variables that characterize a response 
while omitting irrelevant variables. The goal with variable selection is to obtain a set of predictors that perform well on a *training set* (a random subset of the 
data, usually $80\%$ of the number of observations) and generalize to 
never-before-seen data in a *testing set* (the remaining $20\%$).

### Why Do Statisticians Perform Variable Selection?

In the context of *generalization*, the idea that a statistical model should 
perform reasonably well on unseen data, as it had on the data on which it was 
trained, is the consequence of realizing that **the more variables, predictors, or transformations fed into a statistical model, the better that model will predict on the training set.** More formally, an increase in the number of predictors $p$ 
lowers the *training error*, usually the average squared distance between any 
response value and its prediction (i.e., the MSE); this happens because the 
increase in complexity allows the model to capture more complex, 
higher-dimensional relationships in the training set, **but** generally results in poor performance on the testing set due to *overfitting*. (This is an example of 
the [curse of dimensionality](https://en.wikipedia.org/wiki/Curse_of_dimensionality).)

As for **planning** to determine the variables used in a regression model, I, 
personally, create such a plan *during my Exploratory Data Analysis!* If I happen 
to have domain knowledge over the research questions or datasets, that separately 
affords me insight into which variables to include in my regression model, as I 
would quite literally know a priori that which I am investigating. Utilizing **unsupervised learning techniques** such as PCA (discussed in a later section), 
for example, afford me two things: *first*, the technique investigates the 
relative importance of variables in the dataset (not w.r.t. the response 
of-interest) and can supply visualizations indicating the strength of the 
relationships between the variables (see the `fviz_pca_var` function in `R`), and 
*second*, the **loading vectors** obtained from PCA can be used as predictors in a regression model -- addressing the aforementioned curse of dimensionality through 
dimension reduction, the *goal* of PCA! At an even higher level, however, I rely 
on correlation analysis to inform me of variables that have a strong linear 
relationship with my response, as not only must I be cognizant of the variables in my dataset, but of how they relate with the response under whatever modeling 
paradigm I use.

### Preferred Techniques for Variable Selection

While by no means are the techniques presented in this section exhaustive with respect to variable selection, they are methods which I consider using in any scenario that calls for determining important predictors in a model.

#### Principal Component Analysis

**What is Principal Component Analysis (PCA)?** PCA is a dimension-reduction technique -- given $p$ predictors that jointly explain the variability in a response, PCA looks for *linear combinations* of these variables that account for most of the variability in the dataset. The $m < p$ linear combinations we find are referred to as the *principal components*, which are orthogonal vectors that capture large proportions of the variance and, more importantly, reduce the dimension of the predictor space.

**Why PCA?** Projecting the variables onto lower-dimensional representations through PCA does multiple things, in the context of variable selection: 

1. It highlights variables that are closely related with one another, indicating possible *multicollinearity*. 

2. It is often performed after **standardizing** each variable (subtracting every observation by the variable's mean and dividing the obtained quantity by the standard deviation), thereby addressing the possibility of misinterpreting variable importance, otherwise due to deviations in variables on larger orders of magnitude inflating/deflating measures such as the mean squared error.

3. In the case of obtaining the resulting principal components from PCA, one may use these as **predictors** in a regression model -- this technique is called **Principal Components Regression**! Using these components is a form of noise reduction, reducing the impact of noise or uninformative predictors on the response variable. (*However*, it should be important to note that we lose interpretability of the model, as the principal components seldom have real-world interpretations.)

#### Elastic Net Regularization

**What is Elastic Net Regularization?** Commonly referred to as *elastic net*, this technique combines two famous variable selection techniques in regression models, namely [**Ridge Regression**](https://en.wikipedia.org/wiki/Ridge_regression) and the [**LASSO**](https://en.wikipedia.org/wiki/Lasso_(statistics)). Using a weighted average of the optimization criterion of Ridge and LASSO (i.e., L2 and L1 penalizations, respectively), elastic net overcomes noted limitations of the aforementioned methods by both shrinking regression coefficients and grouping related variables.

**Why Elastic Net?** In the case of a *large* number of predictors, elastic net can be quite useful through its hyperparameter, $\alpha$ -- the value controls what proportion of the cost/optimization function is controlled by the LASSO or Ridge criterion (smaller values of $\alpha$ prioritize Ridge). This control of regression coefficients can result in more sparse estimates that simplify the prediction of a response down to a few relevant variables; additionally, multicollinearity is controlled by the algorithm being able to adjust the magnitude of the coefficients. Lastly, the method lends itself to cross-validation approaches, thereby being more robust.

#### Best Subset Selection

**What is Best Subset Selection?** Best Subset Selection is a variable selection technique used in determining predictors for regression models. It involves an exhaustive search of all possible combinations of predictor variables to find the subset that minimizes a selected model criterion, whether it be the **AIC** (Akaike Information Criterion), **BIC** (Bayesian Information Criterion), **VIF** (Variance Inflation Factor), or maximizing $R^2$ (the proportion of variability explained by the response). This method is an alternative to *Forward Regression*, *Backward Regression*, and *Stepwise Regression* (and is typically used in tandem with these methods by comparing resultant model fits).

However, a notable drawback of this method is the difficulty including interaction terms or transformations of predictors -- these would need to be specified a priori in a dataset to be considered.

**Why Best Subset Selection?** 

1. **Exhaustive Search** If the regression model desired uses only the supplied variables, then Best Subset Selection provides the best possible subset of predictors by evaluating combinations of these variables. (Nonlinear terms, however, are not to be ignored due to their complexity and difficulty to include in these methods!)

2. **Interpretability** Being that the model fit includes variables already present in the dataset, the interpretability of resultant models is often immediate and feasible! This feature lends itself to research in disciplines within the social sciences, where often the models are created with specific applications, questions, or interpretations in mind.

3. **Customized Criterion** As mentioned earlier, the criterion with which the algorithm is conducted can be changed, allowing users to prioritize certain properties of the resulting fit based on how criterion are defined.

### Conclusion

This blog post introduces the idea of Variable Selection, offers the techniques I often find myself using in and outside of coursework, as well as why statisticians use the methodology when constructing models.
