SPECIAL MODULES/PACKAGES : 

Warnings (import warnings):
Purpose: The warnings module is used to handle warning messages that may be issued by other modules or 
libraries. In your code, you are using warnings.filterwarnings('ignore') to suppress warning messages. 

handle the errors raised by other modules 
warnings.filterwarnings('ignore')

Pipeline (from sklearn.pipeline import Pipeline, make_pipeline):

Purpose: The Pipeline class in Scikit-Learn is used to streamline a lot of routine processes by putting 
together a sequence of data processing steps. It's commonly used for constructing workflows in machine 
learning, especially when you have a series of data transformations and a final model.

GridSearchCV (from sklearn.model_selection import GridSearchCV):

Purpose: GridSearchCV is a module in Scikit-Learn that performs an exhaustive search over a specified 
parameter grid, evaluating all possible combinations of hyperparameters to find the best ones for a given 
model.

WE WILL USE ONY THE BELOW FEATURES FROM OUR DATASET
the age of the client
marital status of the client
occupation of the client
monthly income of the client
educational qualification of the client
family size of the client
latitude and longitude of the location of the client
pin code of the residence of the client
did the client order again (Output)
remarks on the most recent order (Positive or Negative)

CLEAN THE DATA :
isnull() : : This part of the code generates a DataFrame of the same shape as the original data , For 
example, if a value is missing in the original DataFrame, the corresponding entry in the new DataFrame will 
be True; otherwise, it will be False, 

When sum() is called on a Boolean DataFrame, it treats True as 1 and False as 0 , it gives the number of 
missing values in each column.
so use => data.isnull().sum() # no empty values

VISUALIZE THE DATA 
palette = Set3, hue="Output"  , hue->color mapping
Set3" is a qualitative color palette with a set of distinct colors suitable for categorical data.
The "Output" column is used to color the bars based on different categories. 

CLASSIFY BASED ON 
AGE , FAMILY-SIZE , EDUCATIONAL CATEGORIES OF CUSTOMER, OCCUPATION

OBSERVATONS FROM ABOVE VISULAIZATION :
20-25 AGE , FAMILY-SIZE = 3 , PG, (STUDENT, EMPLOYEE, SELF-EMPLOYED) => ALWAYS ORDER MOST  

NOW CLASSIFY BASED ON GENDER (MALE/FEMALE)
plot a PIE-CHART  => OBSERVATONS male > female (slight)

The number of male customer in the data is slightly higher than the number of female customer. Let's look at 
the distribution of occupation and gender and reordering by gender.
ex:Student(Male/Female) , Employee(Male/Female), ...

observations => sudents(Male) are most 

CREATE A PIE-CHART FOR FUTURE PREDICTION ORDERS : 
using fig.update_traces(marker->dict-of-colors)
initialize a figure object => fig = Figure() , then 
value_counts() => counts the unique gender = amle and female 
hover-on-pie-chart to get Female/Percentage or Male/Percentage

NOW CLASSIFY BASED ON INCOME 
OBSERVATONS => no income - students => MORE ORDERS 

NOW CLASSIFY BASED ON MARITIAL-STATUS : YES, NO/NOT-PERFER TO SAY 
OBSERVATIONS=>SINGLE are MORE

PREPARE THE DATA 
unique() => to check only unique things from whole column 

# map the data , and change the values to 0 , 1 , 2 => easy to move and classification for more CUSTOMERS, 
easy for ML-MODEL TO TRAIN 
using map() , replace()

BUILD A PREDICTION MODEL NOW , SEPARATE THE DATA => 20% for TEST and 80% for TRAINING MODEL
Y->OUTPUT(dependent variable) , X-REMAINING FEATURES(independent variables )

use RANDOM-FOREST-CLASSIFIER MODEL ,(it cannot handle nan-values ) => use Imputer on X_train and X_test and 
fill the NAN values with mean of the column 
what is NAN ? => missing , or NOT-A-NUMBER(SPECIAL FLOATING NUMBER) => 0/0 , or None


use fit() => This method takes the features (X_train) and corresponding labels (y_train) from the training 
dataset and adjusts the internal parameters of the model to learn the patterns in the data. After calling 
fit, the model is trained and ready to make predictions on new, unseen data.

use score() => The score method is used to evaluate the performance of the trained model on a separate 
dataset (often a validation or test dataset).

key-code : 
# use random-forest-classifier MODEL, i want atleast 100 trees => n_estimators=100
rfc = RandomForestClassifier(n_estimators=100)

# train the model using 80%data by rfc above 
rfc.fit(X_train, y_train)

# Use trained model above => for getting SCORE of the TEST-Model below => score()
print(rfc.score(X_test, y_test))

use predict() => to predict the rfc on test_ data 

use confusion_matrix : 
The confusion matrix is a table that is often used to evaluate the performance of a classification algorithm. 
it can also be used for features like 
Performance Evaluation(my-project), Model Validation(unseen data), Decision-Making Insights, Error Analysis:

True Positive (TP): The number of instances correctly predicted as positive.
True Negative (TN): The number of instances correctly predicted as negative.
False Positive (FP): The number of instances incorrectly predicted as positive (Type I error).
False Negative (FN): The number of instances incorrectly predicted as negative (Type II error).

                Actual Positive    Actual Negative
Predicted Positive      TP               FP
Predicted Negative      FN               TN

perform CROSS-VALIDATION 
The cross_val_score function from scikit-learn is used to perform cross-validated scoring of your Random 
Forest Classifier.
It takes the classifier (rfc), the features (X_train), the target variable (y_train), and the number of folds 
for cross-validation (cv=5 in this case).

why cv=5 ? 100 is not safe => not proper answer 
The cv=5 parameter in cross_val_score represents the number of folds used in cross-validation. In our case, 
it's set to 5, meaning the training data is split into 5 equal parts (or folds), and the model is trained and 
evaluated 5 times, each time using a different fold as the test set and the remaining folds as the training 
set.

i want more perfomance of the model 
Confidence Interval = Average Score ± 2 × Standard Deviation

PERFORM PARAMETER SEARCH NOW : 
parameters = {
    'randomforestclassifier__n_estimators': (20, 50, 100)
}

n_estimators in RandomForestClassifier
The n_estimators hyperparameter in RandomForestClassifier represents the number of decision trees that are 
included in the random forest. Each tree contributes to the final classification decision, and having more 
trees can lead to better generalization and improved performance, up to a certain point.

why values 20, 50, 100: These values are chosen as they represent a range of options for the number of trees 
in the forest.
A lower number like 20 may lead to simpler models, quicker training times, but it might not capture complex 
relationships in the data as effectively.
A higher number like 100 may potentially capture more complex patterns in the data but may require more 
computational resources.

Starting with a small number (20) allows you to explore simpler models.
Intermediate value (50) gives a balance between simplicity and complexity.
A larger value (100) explores a more complex model.

using grid-searchCV  with pipeline created above 
make_pipeline(RandomForestClassifier()). It represents the sequence of data processing steps followed by 
the model. that (20,50,100)

The verbose parameter controls the verbosity of the output during the grid search. Setting it to 1 means you 
will get detailed output about the progress of the search.

Parallelization (n_jobs=-1):
Setting n_jobs to -1 enables parallelization during cross-validation. This means that multiple combinations 
of hyperparameters are tested simultaneously using multiple processors if available, which can speed up the 
grid search process.

gridsearch.fit(X_train,y_train) => # execute the grid-search now , 
it follows 5 steps 
Grid Search Execution , Cross-Validation, Score Calculation , Best Hyperparameters, Accessing Results

i want the best-estimator(model)=> consider best PARAMETERS AND Best-SCORE from above grid-search 
gridsearch.best_score_ , gridsearch.best_estimator

GENERATE A RANDOM FAKE CUSTOMER HAS APP => WILL HE ORDER , 
use function with (ONE-HOT-TECHNIQUE) to avoid the error of values => float to string => male/Female

OUT OF 7 FEATURES => 4 DISMATCHED(AGE, FAMILY-SIZE, MARRIED, FEMALE ) => SO 0 => NOT ORDER MORE 

// TODO ADD CODE 