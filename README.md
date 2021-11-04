# Application Fraud Analysis
## Fraud detection in a dataset containing application records.
### Background
The goal of this work is to detect fraudulent application records (e.g. credit card or cell phone applications) in a real world dataset. The dataset contains 1000000 application records with 10 features each, such as the date of the application, ssn, full name and zip code of the applicant, etc. The applications in the dataset took place in a duration of a calenda year. This is a supervised problem, i.e. each record in the dataset is labeled as either fraud (label 1 ) or normal (label 0). This is a heavily imbalanced dataset, as the percentage of frauds is a mere 1.44% of all the records. Finally, to simulate a real world scenario, in which our models would have to evaluate new incoming application records, we did not use as training and testing datasets the records of the last two months. The evaluation metric we used was the Fraud Detection Rate at 3% (FDR @ 3%) which is the precentage of frauds detected in the top 3% records ranked as frauds by our models. 
### Approach
#### Feature Engineering
As a first step, we substituted some frivolous values in the records with a unique value for each, such as the record number. Next, we performed feature engineering, to create more features using the ones in the dataset. Based on our domain knowledge, we built new features that relate to the periodicity and speed of applications as they pertain to detecting individual fraud and victim identity fraud are of great importance. Therefore, we built a number of candidate variables based on the data fields in the original dataset as they applied to the concepts of the speed in which applications were seen (velocity variables), the number of days since the last time an application was seen (days since variables), and the speed in which applications were seen over a certain period of time in relation to what was considered normal (relative velocity). In the feature engineering step, we created approximately 650 new features
#### Feature Selection
Following, we performed feature selection, to choose a subset of around 30 features to use as inputs for our models. First, we measured the correlation of each feature with the fraud distribution, using the Kolmogorov–Smirnov (KS) distance and the FDR @ 3% and we kept 1/3 of the features. Second we used recursive feature elimination using a logistic regression model with L2 regularization and the FDR @ 3$ metric and kept 30 features.
#### Statistical Models & Results
For fraud detection we used 4 models: Logistic regression, Boodted Trees, Neural Networks and Random Forests. We trained the models using different paraemeters and configurations each time. The FDR @ 3% for training, test and validation (out of time (OOT)) sets for the best parameter are presented below: 
| Model | Training | Test | OOT |
|---|---|---|---|
| Logistic regression | 0.55 | 0.54 | 0.52 |
| Boodted Tree | 0.57 | 0.56 | 0.549 |
| Neural Network | 0.57 | 0.56 | 0.547 |
| Random Forests | 0.56 | 0.57 | 0.548 |

The random forest model performed better in the test dataset, thus we chose this as our final model. 
