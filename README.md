# FinTech-ETL-Analysis

![](intro.image.jpeg)

## Introduction:

This data is a customer data for a fintech company. The goal is to understand the data, transform the data using various techniques, analyse the data in order to come up with inferences that could provide more insights into the firm’s customer profiles and then load the transformed data into an SQL database.


## Skills/Concepts Demonstrated:
The following are the Python concepts that were incorporated into this project:
- EDA
- Feature Engineering
- Functions Definition
- Data Cleaning
- Data Wrangling
- Loop Optimization
- Null/Fill Techniques
- ETL

## Libraries Used:
Some of the libarries used in this project were:
- Numpy 
- Seaborn 
- Pandas 
- Matplotlib 



## Exploratory Data Analysis - EDA

I used the following functions to understand my data such as its structure, each data point, the standard deviation, the maximum value on each column, the data types of each column, if there were null values, the minimum value of each column, as well as percentiles of each column.

- data.head(30)
- data.describe().T
- data.isnull().sum()
- data.shape
- data.info
- data.dtypes

[link]

- It showed that about 8 columns had null values such as name, monthly inland salary, type of loan, num credit inquires, credit history age,amount invested monthly.
Although other columns appeared inconsistent and dirty.

- It also showed that columns that were suppose to be float or integers were identified as object columns.


## Data cleaning:
1. Handling unwanted symbols 
I created a list to hold the specific columns that had unwanted symbols like - or _ 
Then defined a loop to iterate over the columns that are in the list and replace the values with nothing

[link]

2. Handling Data type/defining functions
I defined a function that converted specified columns in a created list that were identified as objects to float64
In this function I used a for loop so that it iterates over each column and where there seems to be an error for a column, it returns the column so I can dig further.

3. Null/NaN
For the Name column, I used forward fill to take care of this. This was possible because the customer_id column gave me an insight into how the name column was structured in relation to it.
By counting each occurrence of a customer id using the value count, I was able to see that each customer id appeared 4 times and the length count was 12,500
And by using the shape function, it showed that my rows were 50,000. Given 50,000/12,500 that gives 4.
In order  to confirm this theory, I used the .Isnull on the name and customer_id column to find out the data points that were empty in the name column. Picked a random customer_id and filtered it to all the occurrences and it showed they all belonged to a name - 4 entries (3 names  with one NaN)
Then I ran data_edited.head to see how the names were positioned and with this I got the idea of using forward fill.

4. Filling Numerical columns (Float and integers)
I created a numerical list that held all columns except the object columns. And went ahead to fill them with the mean of the column 

5. Payment min amount column had some data points as Nm instead of No. I used the .replace to take care of this.

6. The Occupation also had some inconsistency. Of which I  replaced each consistency with NaN so I am able to fill the cells.
I then applied a group by function to group each customer by their name and fill NaN cells in the occupation column by the most occurring occupation(mode) of each group.

7. Data governance: I choose not to tamper with the Type of  loan column to maintain more data quality, as it appears to be a very sensitive column holding sensitive information. Each data point can be retrieved by contacting the customer in question.
For each customer, we can retrieve the data point either through direct contact with the customer or from a specific source.

[Link to code]


### Feature Engineering:
1. Credit History Age
I transformed the credit history age column into an integer column by extracted the numerical elements in the column, using the regex(regular expressions). By this I searched for a 2 digit numeric and then retrieved its match. Then I converted it from a string to an integer by combining them as decimals using division 12.

This new column was called Credit history age edit. I then went ahead to fill it with the mean but only group to each 4 occurrence of the customer name for more uniformity.


## Analysis/Insights:
The report comprises 4 Insights:
1. Average  income by occupation
2. Correlation between Monthly salary and Amount invested  
3. Occurrences of Payment 
4. Distribution of Credit utilisation ratio.

1. Average  income by occupation: 
 [image]

The store currently have a total of 1765 customers
330K orders were made in the current year.

2. Correlation between Monthly salary and Amount invested:
[image]

There are 128 products in the stores with a worth of 140 million dollars.
Each product II streamyard.com is sharing your screen.

3. Occurrences of Payment:
[image]


4. Distribution of Credit utilisation ratio:
[image]

## Challenges encountered 
1.For the average annual  income by occupation, I initially visualized it by grouping the occupations such as teacher, engineer, writer. However I realized that each customer had 4 rows related to them and the annual income but have been the same.
So I optimized the code to also select the distinct customer_id so it returns each value for each customer when grouping the occupation way 

2. I tried convert specified columns in a list to a float, however a column appeared stubborn. I need introduced new blocks into the loop so that it return the die if column that had error, its index and  value. 

3. Changed Credit Limit: for empty cells, I could not fill the column with its mean. And this was due to the fact that the column was recognized as an object so I had to convert it to a numeric column first. However when I tried to convert the column to a numeric column (float64), it couldn’t and returned error due to the empty cells that was in the column 

4. I tried to create a defined loop that converts the change credit limit column to a float and yet ignore any cell that refuses to convert. however, it did not work due to the empty cells. So, I created a defined loop instead that fills the empty cells with NaN ( Not a Number) in case it refuses to convert 

5. For the credit history age. There were some cases of data ceiling, therefore, in order to maintain a data governance system, I ensured to round the conversion to at least 2 decimal places. 
 

## ETL
After Extracting form the web and transforming, I loaded the transformed data to a postgreSQL database 

[SQL code]
[im\ges of table


## Conclusion
Data Cleaning is the most essential part of analysis, Bad data = bad insights. And the good thing is, there are some cools tricks that make data cleaning less rigorous.
- Using loops: it helps you iterate over columns and see your data for what it really is 
- Defining function: defining functions helps you set functions ahead of time, especially for repetitive task. And by this you can merch few process into it and call it whenever you need it 
- Pipelines: pipelines are also one way to handle data cleaning/ transformation process by storing it into a container.


