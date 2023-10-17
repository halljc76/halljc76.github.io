## Exploratory Data Analysis (EDA): What, Why, and How?

> "All models are wrong, but some are useful."
> - George E.P. Box

Imagine this scenario: You are at your first job, and your boss hands you a dataset bigger than anything you have ever seen before, and asks you to create a model to predict some response. Intimidated, you boot up RStudio and read/connect to the dataset/database, and see that not only is it massive, it is incredibly *messy*, with lots of missing values, malformed cells, and unconventional names for variables!

To avoid losing your first job, you need a plan for tackling this *massive* (and important) project. You remember your data science courses, and the projects you worked on, when it hits you -- "EDA"! You remember "EDA" being a part of each project you had to complete, but *how* do you perform it?

This blog post will investigate performing **Exploratory Data Analysis** (EDA), what it is, *why* we, as statisticians, perform it, and *how* one might get started on it.

### What is EDA?

At a high level, EDA is analyzing the data one has available to them -- the 
foundation of modeling is *questioning* why relationships in the data or in 
real-world scenarios are why they are, and EDA helps enlighten data scientists on 
potential connections to whatever questions they are answering, or whatever a 
client has them investigating. 

### Why Do Statisticians Perform EDA?

There are a *number* of reasons why statisticians perform EDA! Generally, however, they can be summarized into the following:

1. **Understanding Data**: To gain preliminary understanding of the data one is working with, EDA is used to identify variable types, the meaning communicated by the variables, and potential distributions to which data may belong.

2. **Identifying Anomalous Observations (e.g., Outliers, Influential Points)**: EDA allows 
statisticians to detect anomalies 
within their dataset, whether they 
be the *outliers* (values far, far 
away from the rest of the data), 
*influential points* (values whose 
presence has a significant 
mathematical impact on the model 
generated), or the result of 
*errors in recording, data collection, or presentation* due to
machine error, lack of unit 
conversion, etc.

3. **Formulating Hypotheses**: 
Sometimes, research questions are 
formed *after* analyzing the data 
as the result of unexpected 
observations or relationships! EDA 
can make statisticians aware of 
avenues of questioning or modeling 
of which they were not previously 
aware, especially if the subject 
material is outside of their field 
of expertise! 

4. **Choosing Modeling Techniques**: EDA can help 
statisticians identify appropriate 
modeling techniques by identifying 
the types of responses or 
predictors in the dataset and determining if the problem(s) at-hand are ones of classification, prediction/estimation (i.e., regression), or a mix of the two.

5. **Visualizations**: In industry,
what often comes after statistical 
modeling is presentation to 
superiors, clients, or the general 
public. As such, EDA often has a 
graphical or visual component, 
wherein relationships are graphed 
through box plots, scatterplots, 
histograms, etc., in order to both 
reveal unseen insights about data 
or to visually present the 
efffectiveness of a model or 
statistical procedure.

6. **Data Cleaning and Preprocessing**: To improve model building, *preprocessing* is an extremely pivotal step in any data analysis. Some statistical models such as PCA, Neural Networks, or SVMs, desire **standardized** variables (variables with means of $0$ and variances of $1$). More generally, however, datasets are *cleaned* by having missing values addressed by *imputing* techniques, wherein the missing values are often replaced with a variable's measure(s) of center (i.e., mean, median, mode, etc.) or with values that are the result of separate analysis altogether (i.e., clustering to determine which level of a categorical variable is an observation likely to fall under). Data cleaning also extends to ensuring one's data aligns with their software requirements (e.g., *tidy* data in the `tidyr` R package). Separately, one might create new variables altogether based on the outputs of statistical modeling techniques (e.g., the creation of categorical response variables, rather than leaving them as string/character values)!

### How Do I Perform EDA: Common Strategies

While the EDA I perform may differ slightly from dataset-to-dataset, there are common strategies or overarching themes to my EDA efforts each time I perform the analysis.

**Step 0: Read in the Data**: Before *analyzing* the data, I need to read it in! This step will utilize whatever packages, functions, or other means I have of connecting to a dataset or querying a database. Upon reading it in, I also *structure* the dataset into whatever language-appropriate object is best for storing it (e.g., Pandas DataFrames or `R` data frames).

**Step 1: Get Variable Names** - While this might seem simple, I find it *incredibly* hard to model (impossible, even) without knowing at least the *names* of the variables with which I am working! Whether it be through `names()` or `colnames()` in `R`, or through some other language-appropriate medium, I first familiarize myself with the langauge of the data such that I can converse with others (and myself) about it, asking questions in-context and performing outside research to better understand a variable if its purpose or inclusion is unclear.

**Step 2**: **Get Variable Types** - Again, while this might seem incredibly simple, or immediate from reading in the data, but understanding if ones variables are non-numeric/numeric, ordinal/nominal (i.e., referring to rankings or not), and quantitative/qualitative (i.e., categorical) informs the choice of statistical model, as well as the need to create dummy variables to one-hot encode multi-level (i.e., $> 2$) categorical variables if need be!

**Step 3: Preprocess and Clean** - Next, I look for missing values and appropriately clean or impute values into my dataset through whatever tools the language(s) in which I work offers me, based on context! I may also derive smaller models here (e.g., classification or regression) models if I wish for a more 'informed' imputation. This step may involve first simply counting the number of missing variables, and asking questions as to *why* this value might be missing!

**Step 4: Visualize My Data** - Now that I know *how* to reference my data, and the *types* of data with which I am dealing, I plot univariate and bivariate relationships between the data, and ask myself questions such as

- *Can I see a relationship between variable $X_1$ and $X_2$?*
- *Which variables have noticeably strong correlation?*
- *Is my response bimodal/normally distributed/etc. (continuous), or what is the mode/prevalent categories of my response (discrete)?*

**Step 5: Choose Modeling Framework(s) and Perform Feature Engineering** - Based on the response variable(s) I want to model or characterize as functions of my predictors, I identify candidate modeling procedures and perform any additional *feature engineering* (creation of new variables to better describe existing variables or potentially highlight novel or important relationships) to allow these models to perform under their assumptions or desired modes of operations (re: standardization of variables). This step may also involve trying out a candidate model or performing variable selection procedures (forward/backward/best subset) to obtain feedback on whether my intuitions might lead me to a relatively successful model, or if more research or questioning is required!

**However,** I stress that while EDA is a preliminary step in the creation of a final, presented model, it is seldom a linear, one-size-fits-all approach! New questions, ideas, or hypotheses might elicit revisiting some of these steps, consulting literature or outside sources to obtain context, or diving further into any additional information that might accompany a dataset.

## Conclusion

This blog post introduces the idea of Exploratory Data Analysis (EDA), offers reasons for considering it in statistical modeling, and defines an example framework by which I perform my EDA.