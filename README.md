# sales_analysis
sales analysis using data analysis libraries
# Using data sheet we analyse the following questions
1. what is the overall sales?
2. what are the top 10 product by sales?
3. what are the most selling products?
4. which is the most preferred shippment mode?

# libraries used 
pandas
### data manipulation
- numpy 
 ### data visulisation 
- seaborn
- matplotlib

# staritng the sales analysis

import pandas as pd 
import matplotlib.pyplot as plt
%matplotlib inline
import seaborn as sns

df= pd.read_excel('superstore_sales.xlsx')
df.head()
df.tail()
# exact no of rows and columns
df.shape
# information about data set
df.info()
# checking the missing values in data set
df.isnull().sum()
# getting discriptive statsdtical analysis
df.describe()
# exploratory data analysis 
# what is the sales trend?
df['order_date'].min()
df['order_date'].max()

# getting month year from the data sheet
df['month_year']=df['order_date'].apply(lambda x:x.strftime('%y-%m'))

# grouping month year
df_trend=df.groupby('month_year').sum()['sales'].reset_index()

# set the figure size first
plt.figure(figsize=(20,8))
plt.plot(df_trend['month_year'],df_trend['sales'])
plt.xticks(rotation='vertical',size=8)
plt.show()

# which are the top 10 products by sales??
df.head()

# grouping the product name 
df.groupby('product_name').sum()['sales']
pd.DataFrame(df.groupby('product_name').sum()['sales'])
prod_sales=pd.DataFrame(df.groupby('product_name').sum()['sales'])
prod_sales.sort_values('sales',ascending=False)

# sorting the product names by its sales in decending order
prod_sales=prod_sales.sort_values('sales',ascending=False)

# Top 10 products by sales
prod_sales[:10]

# which are the most selling products?
most_sell_product=pd.DataFrame(df.groupby('product_name').sum()['quantity'])
most_sell_product=prod_sales.sort_values('quantity',ascending=False)
most_sell_product[:10]

# what is the most preffered shipmode?
sns.countplot(df['ship_mode'])

