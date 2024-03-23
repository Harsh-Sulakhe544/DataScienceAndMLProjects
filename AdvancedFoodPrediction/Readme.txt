STEPS FOLLOWED FOR THE PROJECT 
1 load the dataset 
2 Handling missing values from the columns 
3 Save the cleaned dataset to a new file
4 Analyze Based on Gender and Plot Pie Chart
5 CLASSIFY BASED ON OCCUPATION
6 Classify Based on Marital Status and Plot Horizontal Bar Plot
=> tight_layout() will also adjust spacing between subplots to minimize the overlaps.(2 cols in a single row )
7: Classify Based on Monthly Income and Plot Bar Plot - FAILED 
7: Classify Based on health-concerned or not-concerned and Plot Bar Plot -  
8 classification idea: Education Level.
9 Classify Monthly Income distribution
10 Classify Family Size distribution => hue=family_size_distribution.index is the most important error 
solved  
11 Classify Age distribution,  kde => kernel estimate data => add curve for data
12 Classify less Delivery Time =>  palette=colors[:5] => out of 10 use only 5 => o resolve pallette warning 
13 Classify Long Delivery Time =>  palette=colors[:5] => out of 10 use only 5 => o resolve pallette warning 
14  Classify Order Time 
15  Classify Maximum wait time 
16  classify Freshness, spacing matters =>column-name is  (Freshness-)
17 classify Good Taste , space matters again here in csv file
18 Classify Good Quantity , 
19 Classify Google Maps Accuracy 
20 Classify More Offers and Discount
21 Classify Good Food quality
22 Classify Good Tracking system
23 Classify Easy Payment option
24 Classify Self Cooking
25 # Pie Chart for Influence of Rating
26 # Histogram for Unaffordable
27 # Classify Unavailability
28 # Classify Bad past experience

ERRORS FOR THIS PROJECT : 

PATCHES-ERROR = DUE TO SEABORN LIBRARY COUNTPLOT() => WILL PRODUCE MALE AND FEMALE WITH A SAME COLORED BAR , 
WHICH IS NOT PROPER AND NOT DISTINGUISHABLE  => HUE="GENDER" , DODGE="FALSE" , SOLVES THE ERROR, ALLOWS 
SEABORN TO CREATE A DIFFERENT CLUSTERS WITH DIFF COLORS TO DIFFERENTITATE  

FUTURE -WARNING => IS ALSO SOLVED DUE TO DODGE="FALSE"
frameon=False  => optimized space and proper visulization 

FORMULA ANALYSIS FOR GRAPHS TO DISPLAY : 

Percentage Calculation:

percentage = '{:.1f}%'.format(100 * p.get_width() / len(df_cleaned)): This calculates the percentage of the 
total orders represented by the width of the bar (p.get_width()). It uses the formula (width of the bar / 
total number of orders) * 100. The '{:.1f}%'.format(...) formats the result as a string with one decimal 
place followed by a percentage sign.

Label Position (x and y):

x = p.get_width() + 0.02 * len(df_cleaned): This determines the x-coordinate of the data label. It positions 
the label just slightly to the right of the end of the bar. The 0.02 * len(df_cleaned) is added to provide a 
small offset for better aesthetics.
y = p.get_y() + p.get_height() / 2: This determines the y-coordinate of the data label. It positions the 
label at the vertical center of the bar.

ax.text Function:

ax.text(x, y, percentage, ha='left', va='center'): This adds the text (percentage) to the plot at the 
specified x and y coordinates. ha='left' sets the horizontal alignment to left, and va='center' sets the 
vertical alignment to the center.

DIFFICULT TO READ THAT INCOME , Below Rs.10000 , OR NO-INCOME , MORE THAN 50000, = so cancel 

7: Classify Based on health-concerned or not-concerned and Plot Bar Plot -
percentage = '{:.1f}%'.format(100 * p.get_height() / total_orders_by_health[p.get_x()]) 
The pandas groupby() function is used to group similar data into groups and execute aggregate
operations like size/count on the grouped dat

=> Certainly! The warning suggests that using integer keys directly with total_orders_by_health is 
deprecated. To avoid this warning, you can use the iloc indexer to access the value by position. Here's the 
updated code: => 

percentage = '{:.1f}%'.format(100 * p.get_height() / total_orders_by_health.iloc[round(p.get_x())])

8 classification idea: Education Level. => using iLoc 

The Pandas library provides a unique method to retrieve rows from a DataFrame. Dataframe.iloc[] method is 
used when the index label of a data frame is something other than numeric series of 0, 1, 2, 3….n or in case 
the user doesn’t know the index label. Rows can be extracted using an imaginary index position that isn’t 
visible in the Dataframe.

What does bins mean in histogram?
A histogram displays numerical data by grouping data into "bins" of equal width. Each bin is plotted as a bar 
whose height corresponds to how many data points are in that bin. Bins are also sometimes called "intervals", 
"classes", or "buckets".

why co-relation-matrix 
A correlation matrix is a statistical tool used to evaluate the strength and direction of the linear 
relationship between two quantitative variables. Each cell in the matrix represents the correlation 
coefficient between two variables. The correlation coefficient can take values between -1 and 1:

1: Perfect positive correlation
0: No correlation
-1: Perfect negative correlation


while performing data-standardization ==> 

from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler, OneHotEncoder

harsh - 0 , Sula = 1 , ...
One-Hot Encoding is the process of creating dummy variables. In this encoding technique, each category is 
represented as a one-hot vector. Let's see how to implement one-hot encoding in Python: # importing one hot 
encoder. from sklearn from sklearn.