## Evaluating the credit risk models 
Onur Baser
_________________
 

After downloading the file, we saw that there is 347 high risk loan and 68,740 low risk loan with total of 68,817 observations. We divided this dataset into training and test datasets. Training dataset contained 51,612 observation and the test dataset contained 17,205 dataset. 

We first used the oversampling techniques to predict the loan status from the variables in the dataset. 
### Naive Random Oversampling

With naive random oversamping, we balanced the two samples in our datsets, each group had 51,366 observation. We basicaly generated new samples by randomly sampling with replacement the current available samples.

Using 51,366 observation, we run a logistic regression to estimate the coefficients. 

Using these coefficients, we predicted the risk of loan with the test sample that contained 17, 205 applicants. Out of 17,205 applicants, actual high risk loan number was 101 and low risk low number was 17,104.


Below is the confusion matrix, which shows the performance of an algorithm.  

|Risk    |High Risk  |Low Risk  |
|--------|---------: |---------:|
High Risk|73         |28        | 
Low Risk |4960       |12144    |
 
From the table, we can calculate the balanced accuracy score as 0.716.

The table below shows the inbalance classification report. 

|                |pre   |   rec    |   spe   |     f1   |    geo   |    iba    |   sup    |
|----------------|-----:|---------:|--------:|---------:|---------:|----------:|---------:|
| high_risk      | 0.01 |     0.72 |    0.71 |     0.03 |   0.72   |   0.51   |   101    | 
|  low_risk      | 1.00 |     0.71 |    0.72 |     0.83 |    0.72  |    0.51  |  17104   |
| avg  total     | 0.99 |    0.71  |   0.71 |    0.82  |    0.72  |   0.51   | 17205    |

Precision score, which is the ratio of correctly predicted positive observations to the total predicted positive observations is in the first
column. Out of 5033 predicted high risk appicaant only 73 of them actually high risk, and out of 12172 predicted low risk applicant, 12144 of them is actually low risk. So the model does better job on predicting low risk applicant than the low risk applicant. 

Recall (Sensitivity) numbers are givine in the second column. Out of 101 high risk application, we were able ot predict 73 of them, and also out of 17104 low risk application we were able identify 12144 of them. 

f1 score is weighted average of the precision and recall. Accuracy score works best if false positives and folse negative have similar cost, otherwise f1 score gives a better measurement. f1 score is 0.82 which is higher than accuracy score. 


 ### SMOTE Oversampling
 Synthetic Minority Overampling Technique, SMOTE, works by selecting examples that are close in the feature space, drawing a line between examples in the feature space and drawing a new sample at a pint along that line. 
 
 Below is the confusion matrix, which shows the performance of an algorithm.  

|Risk    |High Risk  |Low Risk  |
|--------|---------: |---------:|
High Risk|69         |32       | 
Low Risk |4476      |12628    |

 
From the table, we can calculate the balanced accuracy score as 0.711.

The table below shows the inbalance classification report. 

|                |pre   |   rec    |   spe   |     f1   |    geo   |    iba    |   sup    |
|----------------|-----:|---------:|--------:|---------:|---------:|----------:|---------:|
| high_risk      | 0.02 |     0.68 |    0.74 |     0.03 |   0.71   |   0.50    |   101    | 
|  low_risk      | 1.00 |     0.74 |    0.68 |     0.85 |    0.71  |    0.51   |  17104   |
| avg  total     | 0.99 |    0.74  |   0.68  |    0.84  |    0.71  |   0.51   | 17205    |

*SMOT did a better job than navie random sampling because it had higher accuracy and f1 scores.*
# Undersampling

Using a Cluster Cetroids algoritm, we did apply undersampling to the data. We were able to sample 246 observations from each group to run the logistic regression. After running logistic regression for total of 492 observation, we estimated the coefficients and with those coefficients we predict the outcomes with our test sample of 17205 observations. The confusion matrix that compares actual and predicted outcomes:  

|Risk    |High Risk  |Low Risk  |
|--------|---------: |---------:|
High Risk|84        |17        | 
Low Risk |8874      |8230   |

Accuracy score was around 0.54 that was lower any of the scores we found under oversampling. 

The table below shows the inbalance classification report. 

|                |pre   |   rec    |   spe   |     f1   |    geo   |    iba    |   sup    |
|----------------|-----:|---------:|--------:|---------:|---------:|----------:|---------:|
| high_risk      | 0.01 |     0.83 |    0.48 |     0.02 |   0.63   |   0.41   |   101    | 
|  low_risk      | 1.00 |     0.48 |    0.83 |     0.65 |    0.63  |    0.39   |  17104   |
| avg  total     | 0.99 |    0.48  |   0.83  |    0.65  |    0.63  |   0.39    | 17205    |

f1 score was around 0.65, which was also lower than any of the oversampling techniques. 

# Combination (Over and Under Sampling)

Resampling the data with over- and under sampling using SMOTE and Edited Nearest Neigbours, yielded 68458 high risk applicanat and 62022 low risk applicant. The confusion matrix after plugging values from test observation set using the coefficients derived from the model that uses training observations are below:

|Risk    |High Risk  |Low Risk  |
|--------|---------: |---------:|
High Risk|73         |28       | 
Low Risk |4611     |12493  |

with the accuracy value 0.726 and f1 value 0.84 from the table below, we can see that combination was the best sampling techniques, that provided highest highest accuracy score and f1 value. 

|                |pre   |   rec    |   spe   |     f1   |    geo   |    iba    |   sup    |
|----------------|-----:|---------:|--------:|---------:|---------:|----------:|---------:|
| high_risk      | 0.02 |     0.72 |    0.73 |     0.03 |   0.73   |   0.53    |   101    | 
|  low_risk      | 1.00 |     0.73 |    0.72 |     0.84 |    0.73  |    0.53   |  17104   |
| avg  total     | 0.99 |    0.73  |   0.72  |    0.84  |    0.73 |   0.53    | 17205    |

## Ensemble Learning

First we used Balance Random Forest Classifier. For each iteration in random forest, we draw a bootstrap sample from the minority class and randomly draw the same number of cases with replacement from the majority class. Then we induce a classification tree from the the data to maximum size. We repeat this process 100 times. 

The confusion matrix after plugging values from test observation set using the coefficients derived from the model that uses training observations are below:

|Risk    |High Risk  |Low Risk  |
|--------|---------: |---------:|
High Risk|68        |33       | 
Low Risk |1749     |15355 |

with the accuracy value 0.786 and f1 value 0.94from the table below.

|                |pre   |   rec    |   spe   |     f1   |    geo   |    iba    |   sup    |
|----------------|-----:|---------:|--------:|---------:|---------:|----------:|---------:|
| high_risk      | 0.04 |     0.67 |    0.90 |     0.07 |   0.78   |   0.59   |   101    | 
|  low_risk      | 1.00 |     0.90 |    0.67 |     0.95 |    0.78  |    0.62   |  17104   |
| avg  total     | 0.99 |    0.90 |   0.67  |    0.94  |    0.78 |   0.62    | 17205    |

We list the features in terms of its importance. Variables such as total_rec_prncp, total_pymnt_inv and total_pymnt had the highest effect. Variables such as collection recovery fee, any home ownership had no effect. 

Next, we did easy ensemble adaboost classifier, and we did better interms of accuracy. The confusion matrix was 

|Risk    |High Risk  |Low Risk  |
|--------|---------: |---------:|
High Risk|93        |8      | 
Low Risk |983    |16121 |

with the accuracy score, 0.932. The f1-score was 0.97.


|                |pre   |   rec    |   spe   |     f1   |    geo   |    iba    |   sup    |
|----------------|-----:|---------:|--------:|---------:|---------:|----------:|---------:|
| high_risk      | 0.09 |     0.92 |    0.94 |     0.16 |   0.93  |   0.87   |   101    | 
|  low_risk      | 1.00 |     0.94 |    0.92 |     0.97 |    0.93  |    0.87   |  17104   |
| avg  total     | 0.99 |    0.94 |   0.92  |    0.97 |    0.93 |   0.87    | 17205    |