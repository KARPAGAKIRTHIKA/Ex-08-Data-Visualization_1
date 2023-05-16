# Ex-08-Data-Visualization-

## AIM
To Perform Data Visualization on a complex dataset and save the data to a file. 

# Explanation
Data visualization is the graphical representation of information and data. By using visual elements like charts, graphs, and maps, data visualization tools provide an accessible way to see and understand trends, outliers, and patterns in data.

# ALGORITHM
### STEP 1
Read the given Data
### STEP 2
Clean the Data Set using Data Cleaning Process
### STEP 3
Apply Feature generation and selection techniques to all the features of the data set
### STEP 4
Apply data visualization techniques to identify the patterns of the data.


# CODE
```
#loading the dataset
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
df=pd.read_csv("Superstore.csv")
df
#removing unnecessary data variables
df.drop('Row ID',axis=1,inplace=True)
df.drop('Order ID',axis=1,inplace=True)
df.drop('Customer ID',axis=1,inplace=True)
df.drop('Customer Name',axis=1,inplace=True)
df.drop('Country',axis=1,inplace=True)
df.drop('Postal Code',axis=1,inplace=True)
df.drop('Product ID',axis=1,inplace=True)
df.drop('Product Name',axis=1,inplace=True)
df.drop('Order Date',axis=1,inplace=True)
df.drop('Ship Date',axis=1,inplace=True)
print("Updated dataset")
df

df.isnull().sum()
#detecting and removing outliers in current numeric data
plt.figure(figsize=(12,10))
plt.title("Data with outliers")
df.boxplot()
plt.show()

plt.figure(figsize=(12,10))
cols = ['Sales','Quantity','Discount','Profit']
Q1 = df[cols].quantile(0.25)
Q3 = df[cols].quantile(0.75)
IQR = Q3 - Q1
df = df[~((df[cols] < (Q1 - 1.5 * IQR)) |(df[cols] > (Q3 + 1.5 * IQR))).any(axis=1)]
plt.title("Dataset after removing outliers")
df.boxplot()
plt.show()
#data visualization
#line plots
import seaborn as sns
sns.lineplot(x="Sub-Category",y="Sales",data=df,marker='o')
plt.title("Sub Categories vs Sales")
plt.xticks(rotation = 90)
plt.show()

sns.lineplot(x="Category",y="Profit",data=df,marker='o')
plt.xticks(rotation = 90)
plt.title("Categories vs Profit")
plt.show()

sns.lineplot(x="Region",y="Sales",data=df,marker='o')
plt.xticks(rotation = 90)
plt.title("Region area vs Sales")
plt.show()

sns.lineplot(x="Category",y="Discount",data=df,marker='o')
plt.title("Categories vs Discount")
plt.show()

sns.lineplot(x="Sub-Category",y="Quantity",data=df,marker='o')
plt.xticks(rotation = 90)
plt.title("Sub Categories vs Quantity")
plt.show()
#bar plots
sns.barplot(x="Sub-Category",y="Sales",data=df)
plt.title("Sub Categories vs Sales")
plt.xticks(rotation = 90)
plt.show()

sns.barplot(x="Category",y="Profit",data=df)
plt.title("Categories vs Profit")
plt.show()

sns.barplot(x="Sub-Category",y="Quantity",data=df)
plt.title("Sub Categories vs Quantity")
plt.xticks(rotation = 90)
plt.show()

sns.barplot(x="Category",y="Discount",data=df)
plt.title("Categories vs Discount")
plt.show()

plt.figure(figsize=(12,7))
sns.barplot(x="State",y="Sales",data=df)
plt.title("States vs Sales")
plt.xticks(rotation = 90)
plt.show()

plt.figure(figsize=(25,8))
sns.barplot(x="State",y="Sales",hue="Region",data=df)
plt.title("State vs Sales based on Region")
plt.xticks(rotation = 90)
plt.show()
#Histogram
sns.histplot(data = df,x = 'Region',hue='Ship Mode')
sns.histplot(data = df,x = 'Category',hue='Quantity')
sns.histplot(data = df,x = 'Sub-Category',hue='Category')
plt.xticks(rotation = 90)
plt.show()
sns.histplot(data = df,x = 'Quantity',hue='Segment')
plt.hist(data = df,x = 'Profit')
plt.show()
#count plot
plt.figure(figsize=(10,7))
sns.countplot(x ='Segment', data = df,hue = 'Sub-Category')
sns.countplot(x ='Region', data = df,hue = 'Segment')
sns.countplot(x ='Category', data = df,hue='Discount')
sns.countplot(x ='Ship Mode', data = df,hue = 'Quantity')
#Barplot 
sns.boxplot(x="Sub-Category",y="Discount",data=df)
plt.xticks(rotation = 90)
plt.show()
sns.boxplot( x="Profit", y="Category",data=df)
plt.xticks(rotation = 90)
plt.show()
plt.figure(figsize=(10,7))
sns.boxplot(x="Sub-Category",y="Sales",data=df)
plt.xticks(rotation = 90)
plt.show()
sns.boxplot(x="Category",y="Profit",data=df)
sns.boxplot(x="Region",y="Sales",data=df)
plt.figure(figsize=(10,7))
sns.boxplot(x="Sub-Category",y="Quantity",data=df)
plt.xticks(rotation = 90)
plt.show()
sns.boxplot(x="Category",y="Discount",data=df)
plt.figure(figsize=(15,7))
sns.boxplot(x="State",y="Sales",data=df)
plt.xticks(rotation = 90)
plt.show()
#KDE plot
sns.kdeplot(x="Profit", data = df,hue='Category')
sns.kdeplot(x="Sales", data = df,hue='Region')
sns.kdeplot(x="Quantity", data = df,hue='Segment')
sns.kdeplot(x="Discount", data = df,hue='Segment')
#violin plot
sns.violinplot(x="Profit",data=df)
sns.violinplot(x="Discount",y="Ship Mode",data=df)
sns.violinplot(x="Quantity",y="Ship Mode",data=df)
#point plot
sns.pointplot(x=df["Quantity"],y=df["Discount"])
sns.pointplot(x=df["Quantity"],y=df["Category"])
sns.pointplot(x=df["Sales"],y=df["Sub-Category"])
#Pie Chart
df.groupby(['Category']).sum().plot(kind='pie', y='Discount',figsize=(6,10),pctdistance=1.7,labeldistance=1.2)
df.groupby(['Sub-Category']).sum().plot(kind='pie', y='Sales',figsize=(10,10),pctdistance=1.7,labeldistance=1.2)
df.groupby(['Region']).sum().plot(kind='pie', y='Profit',figsize=(6,9),pctdistance=1.7,labeldistance=1.2)
df.groupby(['Ship Mode']).sum().plot(kind='pie', y='Quantity',figsize=(8,11),pctdistance=1.7,labeldistance=1.2)

df1=df.groupby(by=["Category"]).sum()
labels=[]
for i in df1.index:
    labels.append(i)  
plt.figure(figsize=(8,8))
colors = sns.color_palette('pastel')
plt.pie(df1["Profit"],colors = colors,labels=labels, autopct = '%0.0f%%')
plt.show()

df1=df.groupby(by=["Ship Mode"]).sum()
labels=[]
for i in df1.index:
    labels.append(i)
colors=sns.color_palette("bright")
plt.pie(df1["Sales"],labels=labels,autopct="%0.0f%%")
plt.show()
#HeatMap
df4=df.copy()

#encoding
from sklearn.preprocessing import LabelEncoder,OrdinalEncoder,OneHotEncoder
le=LabelEncoder()
ohe=OneHotEncoder
oe=OrdinalEncoder()

df4["Ship Mode"]=oe.fit_transform(df[["Ship Mode"]])
df4["Segment"]=oe.fit_transform(df[["Segment"]])
df4["City"]=le.fit_transform(df[["City"]])
df4["State"]=le.fit_transform(df[["State"]])
df4['Region'] = oe.fit_transform(df[['Region']])
df4["Category"]=oe.fit_transform(df[["Category"]])
df4["Sub-Category"]=le.fit_transform(df[["Sub-Category"]])

#scaling
from sklearn.preprocessing import RobustScaler
sc=RobustScaler()
df5=pd.DataFrame(sc.fit_transform(df4),columns=['Ship Mode', 'Segment', 'City', 'State','Region',
                                               'Category','Sub-Category','Sales','Quantity','Discount','Profit'])

#Heatmap
plt.subplots(figsize=(12,7))
sns.heatmap(df5.corr(),cmap="PuBu",annot=True)
plt.show()
```

# OUPUT

Initial Dataset:

![image](https://github.com/KARPAGAKIRTHIKA/Ex-08-Data-Visualization_1/assets/103020162/2ae5f626-f0a1-47e4-ae0f-e9b3cffbe5e3)


Cleaned Dataset:

![image](https://github.com/KARPAGAKIRTHIKA/Ex-08-Data-Visualization_1/assets/103020162/a8fc5da5-7ae4-426a-b75b-f84721deee33)


Removing Outliers:
![image](https://github.com/KARPAGAKIRTHIKA/Ex-08-Data-Visualization_1/assets/103020162/1e2d658b-f83a-42ef-9343-f15a913555b1)
![image](https://github.com/KARPAGAKIRTHIKA/Ex-08-Data-Visualization_1/assets/103020162/f02f9b71-da3e-475e-8557-f8a3d1a65d65)


Line PLot:
![image](https://github.com/KARPAGAKIRTHIKA/Ex-08-Data-Visualization_1/assets/103020162/b546ff21-0d78-4fa0-89ba-4b7a65f436b1)
![image](https://github.com/KARPAGAKIRTHIKA/Ex-08-Data-Visualization_1/assets/103020162/0817e2e8-bdd7-4c5a-80b7-acaa41e1eb3b)

![image](https://github.com/KARPAGAKIRTHIKA/Ex-08-Data-Visualization_1/assets/103020162/d035aa7f-ba05-46be-ae7c-498901f22420)

![image](https://github.com/KARPAGAKIRTHIKA/Ex-08-Data-Visualization_1/assets/103020162/5f0725a0-69fb-4f69-b74c-7a18c089598d)

Bar Plots:

![image](https://github.com/KARPAGAKIRTHIKA/Ex-08-Data-Visualization_1/assets/103020162/63c97d52-721b-4a28-a9a2-6f9eb6ca0c11)
![image](https://github.com/KARPAGAKIRTHIKA/Ex-08-Data-Visualization_1/assets/103020162/24a68eb5-e83e-408c-8d19-ef4dbbcefd17)
![image](https://github.com/KARPAGAKIRTHIKA/Ex-08-Data-Visualization_1/assets/103020162/7862674d-2621-4816-adb3-8e39d288a9eb)
![image](https://github.com/KARPAGAKIRTHIKA/Ex-08-Data-Visualization_1/assets/103020162/ac3aa170-ff08-4e3f-a04b-1a2f4f675191)
![image](https://github.com/KARPAGAKIRTHIKA/Ex-08-Data-Visualization_1/assets/103020162/ef0b4422-064c-427d-a4c1-71990cf8e951)
![image](https://github.com/KARPAGAKIRTHIKA/Ex-08-Data-Visualization_1/assets/103020162/71bbdf42-2a63-4e44-b025-cc2fa8a14a47)
![image](https://github.com/KARPAGAKIRTHIKA/Ex-08-Data-Visualization_1/assets/103020162/3421d244-566b-44ff-9c51-cf20c51cc1d9)

Histograms:
![image](https://github.com/KARPAGAKIRTHIKA/Ex-08-Data-Visualization_1/assets/103020162/556ba177-daca-40a2-aa31-62c937538656)
![image](https://github.com/KARPAGAKIRTHIKA/Ex-08-Data-Visualization_1/assets/103020162/c3a99c7c-baf2-45b5-9d96-18aaaee22159)
![image](https://github.com/KARPAGAKIRTHIKA/Ex-08-Data-Visualization_1/assets/103020162/f716427a-27e8-4655-be32-ff36d5a78cf7)


Count plots:
![image](https://github.com/KARPAGAKIRTHIKA/Ex-08-Data-Visualization_1/assets/103020162/a4481007-866b-47ad-bb69-4900fc1f3a69)
![image](https://github.com/KARPAGAKIRTHIKA/Ex-08-Data-Visualization_1/assets/103020162/b6827725-d64b-4e2f-807d-ba2d53c41b64)
![image](https://github.com/KARPAGAKIRTHIKA/Ex-08-Data-Visualization_1/assets/103020162/083ef5d0-e778-4235-b965-96d4b898b835)
Bar Charts:
![image](https://github.com/KARPAGAKIRTHIKA/Ex-08-Data-Visualization_1/assets/103020162/9147d564-7e93-43d9-bf67-2bf0798cc84d)
![image](https://github.com/KARPAGAKIRTHIKA/Ex-08-Data-Visualization_1/assets/103020162/61a1600f-d4eb-45e6-82a9-7a6f080d8df2)
![image](https://github.com/KARPAGAKIRTHIKA/Ex-08-Data-Visualization_1/assets/103020162/4bea3570-db1a-441d-b0fe-23334bfe8401)
![image](https://github.com/KARPAGAKIRTHIKA/Ex-08-Data-Visualization_1/assets/103020162/b845ebce-7a2d-492a-a70b-10c947577ae6)
![image](https://github.com/KARPAGAKIRTHIKA/Ex-08-Data-Visualization_1/assets/103020162/d2dd46eb-c39e-48d3-b99a-3f0b3036bb51)


KDE Plots:
![image](https://github.com/KARPAGAKIRTHIKA/Ex-08-Data-Visualization_1/assets/103020162/9bb965d3-13af-4b33-9b31-fc1178d12637)
![image](https://github.com/KARPAGAKIRTHIKA/Ex-08-Data-Visualization_1/assets/103020162/4c69b948-46ff-4811-ada1-7a58d5b4ef4c)
![image](https://github.com/KARPAGAKIRTHIKA/Ex-08-Data-Visualization_1/assets/103020162/47c0b5dc-fa3f-452c-8e15-50dcb9d74e1d)


Violin Plot:
OUTPUT-31 OUTPUT-32 OUTPUT-33

Point Plots:
OUTPUT-34

Pie Charts:
OUTPUT-35 OUTPUT-36 OUTPUT-37 OUTPUT-38 OUTPUT-39

HeatMap:
OUTPUT-40

# Result:
Hence,Data Visualization is applied on the complex dataset using libraries like Seaborn and Matplotlib successfully and the data is saved to file.

