# Homework 3 Solutions 

## Problem 1

### Import and explore the district-level fiscal data from 2015-16.Rank and visualize the states that take in the most federal funding (revenue).

For district level fiscal data, I loaded the file 'Sdf16_1a.txt' with the columns giving state name and total federal revenue. Since missing values were denoted by negative numbers, this data was filtered for federal revenue >=0. These revenues were summed up for each state to visualize the federal funding for each state. The figure below represents the top 15 states in descending order of federal revenue intake.

![](/images/Q1a.png)

As we can see, California, Texas and New York are the top 3 states that receive the highest federal fundings.

### Which states spend the most federal funding per student?

To get the states with most federal funding per student, the TOTALEXP column was used along with V33 which indicated the number of students admitted in Fall in each district. These values were aggregated state-wise. The total expenditure per state was then divided by total number of students in each state.
The graph below shows the top 15 states which provide the most federal funding per student arranged in descending order.

![](/images/Q1b.png)

As we can see, District of Columbia, New York and Wyonming are among the top 3 states here. 

## Problem 2

### Visualize the relationship between school districts’ total revenue and expenditures.

to get toal revenue and expenditure data, I extracted the columns 'STNAME', 'TOTALREV', 'TOTALEXP', 'V33' fromt he file 'Sdf16_1a.txt' which contains the fiscal data. The columns 'TOTALREV', 'TOTALEXP' and 'V33' were filtered for values >=0 to remove missing values.
A scatter plot was used to visualize the relationship between total revenue and expenditure between school districts as seen in the graph below.

![](/images/Q2a.png)

The total revenue and expenditure is almost linearly propotional.

### Which states have the most debt per student?

To find out which states have the most debt per student, I calculated debt using the formula:  
DEBT = (total expenditure- total revenue)/ number of students funded  
States with ngative debt (which means no debt) were filtered out.
The plot below shows the top 15 states which have the most debt per student arranged in descending order. North Dakota, District of Columbia and Alaska are ranked highest in this case.

![](/images/Q2b.png)

## Problem 3

### Write and explain a function for processing a single column of “blurred” metrics into usable numeric values.

The below function was written to process a 'blurred' column in a dataframe into usable numeric values.

![](/images/Q3a.png)

The blurred columns consisted of the following different types:  
1. Integers,
2. Range of integers denoted with 2 integers and a hyphen between them,
3. Values Less Than(LT), Greater Than(GT), Less than Equal to(LE), Greater than equal to(GE)
4. 'PS', '.', 'nan'

The function blurred_resolve() shown above handles all the 4 cases above to impute data in the blurred column.    
If the value in the column is an integer, the same number will remian in interger form.  
If the value is a range of integers, the average of the 2 integers is calculated and replaced by value.  
If the value contains LT, a random integer is generated from the range (0, value-1)  
If the value contains LE, a random integer is generated from the range (0, value)  
If the value contains GT, a random integer is generated from the range (value+1, 100)  
If the value contains GE, a random integer is generated from the range (value, 100)
If the value contains 'PS', '.' or 'nan', athe value is replaced by np.nan

### Use it to process and then visualize the distribution of a performance metric of your choice

To visualize a performance metric, 'math-achievement-lea-sy2015-16.csv' file was downloaded to visualize 'MAM_MTH00PCTPROF_1516' column.
The above function was called on the math data on the blurred column 'MAM_MTH00PCTPROF_1516':  
blurred_resolve(math_data, 'MAM_MTH00PCTPROF_1516')  

To visualize this column after unblurring, a histogram was plotted to view the distribution of the performance metric (Proficiency Percentage in Mathematics across all grades for the year 2015-16) after removing na values.

![](/images/Q3b.png)

As we can see from the graph, there are high number of students with high proficiency in Math, especially around 30%.

# Problem 4:

### Choose which school districts will have their funding cut and how this will be done.

Total U.S. federal budget for funding school districts: $55602742000
15% of the U.S. federal budget for funding school districts:  *$8340411300*

To find out which school districts must have their funding cut, the debt was calculated for each districts. Debts greater than 0 means that the district has extra revenue compared to their expense, so revenue could be reduced here. So, the districts with debt<0 were considered where sum of excess revenue for all districts together summed up to $26211614000. Depending on how much excess revenue a district has, funding will be reduced accordingly.

The table representing the leaids vs federal revenue cuts is as belows:

![](/images/Q4.png)

###### Figure 6: LEAID-CUT 

# Problem 5:

### Provide a statement for your supervisor justifying your decisions on which school districts will lose funding.

It would not be ideal to reduce equal amount of funding from each district because districts which have a small excess amount of revenue might go into debt if a large amount of funding is cut, and vice versa. So, depending on the amount of excess revenue held by each district, federal funding can be reduced accordingly.
