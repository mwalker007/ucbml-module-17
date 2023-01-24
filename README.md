### Business Understanding

#### Business Objective

The primary business objective is to determine whether a person is likely to subscribe to a term deposit when presented with marketing offers.

#### Data Mining Goals

Given the dataset of 426K vehicle purchases which includes the features (id, region, year, manufacturer, model, condition, cylinders,
fuel, odometer, title_status, transmission, VIN, drive, size, type, paint_color, state) along with the target selling price, determine which features are most important in determining the price paid for a used vehicle. The desired output is a list of the most important features in rank order.  

#### Project Plan

1) Aquire and explore the dataset for understanding
2) Prepare the data including cleaning and preprocessing
3) Try various modeling techniques in order to find the best model fit for the data and feature importance
4) Evaluate model outputs and repeat steps 3 & 4 as needed
5) Document analysis findings

### Data Understanding

#### Collect Initial Data
The provided dataset contains historical records that includes: demographics of the person, information about the offer(s), when the offers were made,
and broad economic indicators. 

#### Data Description

##### Dataset contains 41188  rows 
 
##### Identify Numeric and Categorical Columns
Numerical Columns: ['age', 'duration', 'campaign', 'pdays', 'previous', 'emp.var.rate', 'cons.price.idx', 'cons.conf.idx', 'euribor3m', 'nr.employed']
Categorical Columns: ['job', 'marital', 'education', 'default', 'housing', 'loan', 'contact', 'month', 'day_of_week', 'poutcome', 'y']

##### Explored Relationship of Numerical Columns
* Consider Dropping columns euribor3m and emp.var.rate since they are highly correlated with nr.employed\
* <img src="correl.png" width="400" height="400"/>

### Data Preparation

##### Data Selection
*  As instructed, Used just the bank information features (columns 1 - 7) and prepared the features and target column for modeling with appropriate encoding and transformations.
 
### Modeling
##### Established a baseline model

##### Trained basic (default settings) models for Logistic Regression, KNN, Decision Tree, and SVM with the following results:

<img src="basic_results.png" width="500" height="300"/>

##### Observations for basic models
- the difference in training times between LogReg, KNN, and Decision Tree is not significant since they are all < 1 sec.
- The SVM takes considerable longer to train
- They don't improve on the baseline model at least partly because the training data is heavily imbalanced.
Some potential ways to address this would be to a) gather more examples of subscription acceptance b) generate synthetic data with acceptance or c) reduce the number of non exceptance

##### Trained models using Hyperparamter Tuning, GridSearch, and Crossfold Validation with the following results:
<img src="grid_results.png" width="600" height="400"/>

##### Observations for the improved models
- the relationship between the training times is similar to the basic models 
- They extra hyperparameters has led to a small improve over the baselince and basic models
- More data columns and balancing the data would likely lead to higher accuracy
- The SVM model training ran very long which prevented me from trying additional hyperparameter options

##### Attempt to improve model accuracy by supplying addition marketing details info to the training dataset (
New training dataset includes: ['age','job','marital','education','default','housing','loan','contact','duration','campaign','pdays']

##### Trained models on the additional data using using Hyperparamter Tuning, GridSearch, and Crossfold Validation similar to above with the following results:
<img src="extra_data_results.png" width="600" height="400"/>

##### Observations for the models with additional data
- the relationship between the training times is similar to the basic models 
- the extra hyperparameters has led to a small improvement over the baselince and basic models
- the DecisionTree classifier was the most effective for the parameters tried since it had a relatively short training time and high accuracy compared
to the other models with the added bonus that it is easier to explain

### Evaluation
#### Summary of Results

##### Possible Next Steps
1. Balance the dataset either by collecting more samples where the person signed up for an account or generate synthetic data using values from rows where the person signed up.
2. Additional fields from the original dataset could be added such as economic indicators or temporal details regarding the when the offers were made.
3. Do additional data analysis to determine if some fields or values shoudl be ommited due anomolies or outliers

#### The Jupyter Notebook used to analyze the data can be found at [prompt_III.ipynb](./prompt_III.ipynb)
