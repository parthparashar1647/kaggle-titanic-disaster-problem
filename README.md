# kaggle-titanic-disaster-problem
This is my first stab at a Kaggle script. I have chosen to work with the Titanic dataset after spending some time poking around on the site and looking at other scripts made by other Kagglers for inspiration. I will also focus on doing some illustrative data visualizations along the way. I’ll then use randomForest to create a model predicting survival on the Titanic. I am new to machine learning and hoping to learn a lot, so feedback is very welcome!

There are three parts to my script as follows:

Feature engineering
Missing value imputation
Prediction!


STEPS IN SOLVING THE PROBLEM:->
1.1 Load and check data
2.1 What’s in a name?
The first variable which catches my attention is passenger name because we can break it down into additional meaningful variables which can feed predictions or be used in the creation of additional new variables. For instance, passenger title is contained within the passenger name variable and we can use surname to represent families. Let’s do some feature engineering!
2.2 Do families sink or swim together?
Now that we’ve taken care of splitting passenger name into some new variables, we can take it a step further and make some new family variables. First we’re going to make a family size variable based on number of siblings/spouse(s) (maybe someone has more than one spouse?) and number of children/parents.
3 Missingness
Now we’re ready to start exploring missing data and rectifying it through imputation. There are a number of different ways we could go about doing this. Given the small size of the dataset, we probably should not opt for deleting either entire observations (rows) or variables (columns) containing missing values. We’re left with the option of either replacing missing values with a sensible values given the distribution of the data, e.g., the mean, median or mode. Finally, we could go with prediction. We’ll use both of the two latter methods and I’ll rely on some data visualization to guide our decisions.

3.2 Predictive imputation
Finally, as we noted earlier, there are quite a few missing Age values in our data. We are going to get a bit more fancy in imputing missing age values. Why? Because we can. We will create a model predicting ages based on other variables.

# Show number of missing Age values
sum(is.na(full$Age))
## [1] 263
We could definitely use rpart (recursive partitioning for regression) to predict missing ages, but I’m going to use the mice package for this task just for something different. You can read more about multiple imputation using chained equations in r here (PDF). Since we haven’t done it yet, I’ll first factorize the factor variables and then perform mice imputation.

4 Prediction
At last we’re ready to predict who survives among passengers of the Titanic based on variables that we carefully curated and treated for missing values. For this, we will rely on the randomForest classification algorithm; we spent all that time on imputation, after all.

4.1 Split into training & test sets
Our first step is to split the data back into the original test and training sets.

# Split the data back into a train set and a test set
train <- full[1:891,]
test <- full[892:1309,]
4.2 Building the model
We then build our model using randomForest on the training set.

4.4 Prediction!
We’re ready for the final step — making our prediction! When we finish here, we could iterate through the preceding steps making tweaks as we go or fit the data using different models or use different combinations of variables to achieve better predictions. But this is a good starting (and stopping) point for me now.
