# Introduction

IEEE-CIS fraud detection challenge is about building a machine learning model to detect fraudulent activities. The dataset is from Vesta corporation which has the transaction ID, transaction amount, details about the cardholder and the location etc. 

The data is very noisy, even absent in many cases. This data had to be preprocessed to make it a standard format and then fed into the machine learning model. The model used is a tree based extreme gradient boosting method, which outputs satisfactory results.

# Approach

## Merging

The data was split into two parts. The transaction informations and the identity informations. These two parts have been merged into one so that we can get the whole picture during data analysis.

After the merging, some name mismatches between the train and test data have been taken care of, by renaming the mismatched fields.


## Missing values and correlation

Dealing with missing values is a cruicial job in this task. Many fields have almost all the records as null. So, at first the percentage have been counted.

Correlation is not significant in this case, as the target values are binary. So if there is strong correlation between a feature and the target field, then thats good, but if there is not, that does not give us a clear picture. I have taken correlation into account for this purpose, as well as the fraud : not_fraud ratio. The idea is, if the ratio of fraud : not_fraud is same for the null values in each column, then the null values or the not null values do not have any significant contribution towards the target variable.

The fraud count ratio for the raw data is 3%. So I have taken the boundary to be 2-5% while the null_value ratio is above 20%. I have also considered correlation as correlation less than 0.03 does not contribute significantly to the data.

After specifying the criteria, I have deleted 318 columns and were left with 115 columns. 

## Filling up the null values

Now that I have the columns I need to work with, I have to deal with the null values. Here I used the pipeline function to specify data imputation. I have separated the numerical and categorical columns. The numerical null values would be filled with median value of the column. The categorical null values would have a separate category as their filling value. Along with filling the missing value records, these also transform data. For numerical data, it scales the data using usual . For categorical data, label_encoder was applied to encode the data into distinct numbers according to their categories.

## Splitting and training the data

The data was split into 80% : 20% ratio for train : val set. The it was fed into oversampler, so that the ratio discrimination between classes are taken care of. Then the whole model is fed into xgboost classifier.

# Result

Based on the predictions made from the validation set,

 **f1_score** = .71

 **AUC** = .97

 **Accuracy** = .98
 
After that the test set predictions were made and submitted. The score was 0.856.

## Conclusion

The statistics I have got from the data, the prediction score is satisfactory. But there are better and less conservative scores that might be more expensive but also more rewarding in predictions.

