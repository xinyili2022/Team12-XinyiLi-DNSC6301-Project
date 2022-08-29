# Credit Limit Increase Model Card
### Basic Information

* **Person or organization developing model**: Xinyi Li, `xinyili0026@gwu.edu`
* **Model date**: August, 2022
* **Model version**: 1.0
* **License**: MIT
* **Model implementation code**: [DNSC_6301_0823.ipynb](DNSC_6301_0823.ipynb)

### Intended Use
* **Primary intended uses**: This model is the assignment in the GWU DNSC 6301 bootcamp. In this model, the probability of default classifier would be shown, determining eligibility for a credit limit increase.
* **Primary intended users**: Professor Johnston Hall.
* **Out-of-scope use cases**: Any other use is out-of-scope.

### Training Data


* Data dictionary: 

| Name | Modeling Role | Measurement Level| Description|
| ---- | ------------- | ---------------- | ---------- |
|**ID**| ID | int | unique row indentifier |
| **LIMIT_BAL** | input | float | amount of previously awarded credit |
| **SEX** | demographic information | int | 1 = male; 2 = female
| **RACE** | demographic information | int | 1 = hispanic; 2 = black; 3 = white; 4 = asian |
| **EDUCATION** | demographic information | int | 1 = graduate school; 2 = university; 3 = high school; 4 = others |
| **MARRIAGE** | demographic information | int | 1 = married; 2 = single; 3 = others |
| **AGE** | demographic information | int | age in years |
| **PAY_0, PAY_2 - PAY_6** | inputs | int | history of past payment; PAY_0 = the repayment status in September, 2005; PAY_2 = the repayment status in August, 2005; ...; PAY_6 = the repayment status in April, 2005. The measurement scale for the repayment status is: -1 = pay duly; 1 = payment delay for one month; 2 = payment delay for two months; ...; 8 = payment delay for eight months; 9 = payment delay for nine months and above |
| **BILL_AMT1 - BILL_AMT6** | inputs | float | amount of bill statement; BILL_AMNT1 = amount of bill statement in September, 2005; BILL_AMT2 = amount of bill statement in August, 2005; ...; BILL_AMT6 = amount of bill statement in April, 2005 |
| **PAY_AMT1 - PAY_AMT6** | inputs | float | amount of previous payment; PAY_AMT1 = amount paid in September, 2005; PAY_AMT2 = amount paid in August, 2005; ...; PAY_AMT6 = amount paid in April, 2005 |
| **DELINQ_NEXT**| target | int | whether a customer's next payment is delinquent (late), 1 = late; 0 = on-time |
* **Source of training data**: GWU Blackboard
* **How training data was divided into training and validation data**: 50% training, 25% validation, 25% test
* **Number of rows in training and validation data**:
  * Training rows: 15,000
  * Validation rows: 7,500

### Test Data
* **Source of test data**: GWU Blackboard
* **Number of rows in test data**: 7,500
* **State any differences in columns between training and test data**: None

### Model details
* **Columns used as inputs in the final model**: 'LIMIT_BAL',
       'PAY_0', 'PAY_2', 'PAY_3', 'PAY_4', 'PAY_5', 'PAY_6', 'BILL_AMT1',
       'BILL_AMT2', 'BILL_AMT3', 'BILL_AMT4', 'BILL_AMT5', 'BILL_AMT6',
       'PAY_AMT1', 'PAY_AMT2', 'PAY_AMT3', 'PAY_AMT4', 'PAY_AMT5', 'PAY_AMT6'
* **Column(s) used as target(s) in the final model**: 'DELINQ_NEXT'
* **Type of model**: Decision Tree 
* **Software used to implement the model**: Python, scikit-learn
* **Version of the modeling software**: Python version: 3.7.13 Sklearn version: 1.0.2
* **Hyperparameters or other settings of your model**: 
```
DecisionTreeClassifier(ccp_alpha=0.0, class_weight=None, criterion='gini',
                       max_depth=6, max_features=None, max_leaf_nodes=None,
                       min_impurity_decrease=0.0, min_impurity_split=None,
                       min_samples_leaf=1, min_samples_split=2,
                       min_weight_fraction_leaf=0.0, presort='deprecated',
                       random_state=12345, splitter='best')`
```
### Quantitative Analysis


#### Metrics used to evaluate your final model (AUC and AIR)
* Test AUC-0.7438


#### State the final values, neatly -- as bullets or a table, of the metrics for all data: training, validation, and test data
![corr](7.corr.png)
* **correlation**: This table shows the correlation between different factors, where the diagonal correlation is one, because the factor is perfectly correlated with itself.
![gap](8.gap.png)
* **gap**: 
This table shows the predicted and actual values for different races. For example, in the case of predictions for whites, both actual and predicted 1 occurred 176 times, both actual and predicted 0 occurred 1228 times, actual 0 predicted 1 813 times, and actual 1 predicted 0 72 times. The predicted acceptance of the combined white population was 0.568, while this table also makes a comparison of the acceptance between different racial groups.
![race](9.race.png)
* **race**: This table shows the predicted and actual values for different races. For example, in the case of predictions for whites, both actual and predicted 1 occurred 176 times, both actual and predicted 0 occurred 1228 times, actual 0 predicted 1 813 times, and actual 1 predicted 0 72 times. The predicted acceptance of the combined white population was 0.568, while this table also makes a comparison of the acceptance between different racial groups.
![sex](10.sex.png)
* **sex**:This table shows the predicted and actual values for different genders. 
![accuracy](11.accuracy.png)
* **accuracy**: As the cutoff value increases, the accuracy goes up.
![acceptair](12.acceptair.png)
* **acceptair**: This table shows the AIR data for different races。
#### Provide any plots related to your data or final model
![datacolumn](1.datacolumn.png)
* **data column**: The image shows the data for each factor, divided into continuous and discrete variables. Discrete variables, such as the number of payments are bars of their respective discrete distributions, and the length of the bars is determined by the frequency of payments; continuous variables, such as the number of loans repaid, are shown as ID data, but the size of the ID data has no practical significance.
![correlation](2.correlation.png)
* **correlation**: This figure graphically shows the correlation between different factors, and the correlation is divided into positive and negative correlation. The lighter the color, the closer the correlation is to a completely positive correlation; the darker the color, the closer the correlation is to a completely negative correlation.                       
![iterationplot](3.iterationplot.png)
* **iterationplot**: This figure shows the data of training AUC and validation AUC under 12 iterations。
![decisiontree](4.decisiontree.png)
* **decisiontree**: The picture is the decision tree of this model.
![variableimportance](5.variableimportance.png)
* **variableimportance**: This figure shows the importance of different factors, and the longer the length of the bar, the more important the factor is. The 0th payment is the most important of all variables.
![iterationplot2](6.iterationplot2.png)
* **iterationplot2**: This figure shows the data of training AUC and validation AUC under 12 iterations.

### Ethical considerations      

#### Describe potential negative impacts of using your model
* The model may be set up with moral hazard, e.g., the conclusion of this model contains that the repayment record of the 0th payment is the most important. It may lead to the failure of the model by repayers who place great importance on the earliest repayment in line in order to improve their creditworthiness, while they do not have the actual ability to repay the loan themselves.
#### Describe potential uncertainties relating to the impacts of using your model:
* The predicted and actual differences by gender and by race are analyzed in this model. This reflects that the model may have bias in predictions due to differences in different populations such as gender, race.
#### Describe any unexpected or results
* There is no way to predict the data completely, but it can be constantly approached by collecting a large amount of past data and correcting it at any time. If this is to happen, a large amount of data will be collected with government intervention. In the event of a data breach, this could have a significant impact on human data security. Illegal companies may also generate profits from these large amounts of data, jeopardizing the normal functioning of the market.


                       
