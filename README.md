# Ex-09-Data-Visualization

## AIM :

To Perform Data Visualization on a complex dataset and save the data to a file. 

## Explanation :

Data visualization is the graphical representation of information and data. By using visual elements like charts, graphs, and maps, data visualization tools provide an accessible way to see and understand trends, outliers, and patterns in data.

## ALGORITHM :

### STEP 1 :

Read the given Data

### STEP 2 :

Clean the Data Set using Data Cleaning Process

### STEP 3 :

Apply Feature generation and selection techniques to all the features of the data set 

### STEP 4 :

Apply data visualization techniques to identify the patterns of the data.


## CODE :

##### DEVELOPED BY : RAKESH J.S
##### REG NO : 212222230115

### Loading the dataset :
``` python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
df=pd.read_csv("/content/Superstore (3).csv",encoding='unicode_escape')
df
```

### Removing unnecessary data variables :
``` python
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
```

### Detecting and removing outliers in current numeric data :
``` python
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
```

## Data visualization :

### line plots :
``` python
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
```

### Histogram :
``` python
sns.histplot(data = df,x = 'Region',hue='Ship Mode')
sns.histplot(data = df,x = 'Category',hue='Quantity')
sns.histplot(data = df,x = 'Sub-Category',hue='Category')
plt.xticks(rotation = 90)
plt.show()
sns.histplot(data = df,x = 'Quantity',hue='Segment')
plt.hist(data = df,x = 'Profit')
plt.show()
```

### count plot :
``` python
plt.figure(figsize=(10,7))
sns.countplot(x ='Segment', data = df,hue = 'Sub-Category')
sns.countplot(x ='Region', data = df,hue = 'Segment')
sns.countplot(x ='Category', data = df,hue='Discount')
sns.countplot(x ='Ship Mode', data = df,hue = 'Quantity')
```

### Barplot :
``` python
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
```

### KDE plot :
``` python
sns.kdeplot(x="Profit", data = df,hue='Category')
sns.kdeplot(x="Sales", data = df,hue='Region')
sns.kdeplot(x="Quantity", data = df,hue='Segment')
sns.kdeplot(x="Discount", data = df,hue='Segment')
#violin plot
sns.violinplot(x="Profit",data=df)
sns.violinplot(x="Discount",y="Ship Mode",data=df)
sns.violinplot(x="Quantity",y="Ship Mode",data=df)
```

### Point plot :
``` python
sns.pointplot(x=df["Quantity"],y=df["Discount"])
sns.pointplot(x=df["Quantity"],y=df["Category"])
sns.pointplot(x=df["Sales"],y=df["Sub-Category"])
```

### Pie Chart :
``` python
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
```

### encoding :
``` python
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
```

### Scaling :
``` python
from sklearn.preprocessing import RobustScaler
sc=RobustScaler()
df5=pd.DataFrame(sc.fit_transform(df4),columns=['Ship Mode', 'Segment', 'City', 'State','Region',
                                               'Category','Sub-Category','Sales','Quantity','Discount','Profit'])

```

### Heatmap :
``` python
plt.subplots(figsize=(12,7))
sns.heatmap(df5.corr(),cmap="PuBu",annot=True)
plt.show()
```


## OUTPUT :

![Screenshot 2023-05-20 223746](https://github.com/Abrinnisha6/Ex-08-Data-Visualization_1/assets/118889454/e55f0fb5-9b2e-4a1b-ba59-f1ffd99ca293)

![Screenshot 2023-05-20 223801](https://github.com/Abrinnisha6/Ex-08-Data-Visualization_1/assets/118889454/0f9b6643-7156-4abf-8552-21e46c8f1f10)

![Screenshot 2023-05-20 224948](https://github.com/Abrinnisha6/Ex-08-Data-Visualization_1/assets/118889454/3380e0a8-c548-4adc-bb34-1fa9dcc81952)

![Screenshot 2023-05-20 225005](https://github.com/Abrinnisha6/Ex-08-Data-Visualization_1/assets/118889454/98bae237-a135-471a-8899-6572532d286f)

![Screenshot 2023-05-20 225109](https://github.com/Abrinnisha6/Ex-08-Data-Visualization_1/assets/118889454/394b5ffb-7829-4fa9-b38d-9cb5c5a7ecab)

![Screenshot 2023-05-20 225117](https://github.com/Abrinnisha6/Ex-08-Data-Visualization_1/assets/118889454/eca60e47-722a-4f6d-b1ec-fb0dd3a62777)

![Screenshot 2023-05-20 225217](https://github.com/Abrinnisha6/Ex-08-Data-Visualization_1/assets/118889454/d3a0556f-9187-47bf-86e7-ffd8cfe7b80d)

![Screenshot 2023-05-20 225402](https://github.com/Abrinnisha6/Ex-08-Data-Visualization_1/assets/118889454/b8221933-3d77-493b-8322-43bea0d1682c)

![Screenshot 2023-05-20 225411](https://github.com/Abrinnisha6/Ex-08-Data-Visualization_1/assets/118889454/6adce382-4d78-46bc-b981-25dbe027446c)

![Screenshot 2023-05-20 225613](https://github.com/Abrinnisha6/Ex-08-Data-Visualization_1/assets/118889454/ede38fc3-2928-4735-9e64-608a559b33d3)

![Screenshot 2023-05-20 225622](https://github.com/Abrinnisha6/Ex-08-Data-Visualization_1/assets/118889454/0e6b2928-b6f4-4b2c-9910-cddaf3661fe6)

![Screenshot 2023-05-20 225630](https://github.com/Abrinnisha6/Ex-08-Data-Visualization_1/assets/118889454/4a45194d-aaf4-464a-8525-6b4e45528aec)

![Screenshot 2023-05-20 225712](https://github.com/Abrinnisha6/Ex-08-Data-Visualization_1/assets/118889454/6778ba2e-ddd7-4051-86d9-c656d17a8979)

![Screenshot 2023-05-20 225720](https://github.com/Abrinnisha6/Ex-08-Data-Visualization_1/assets/118889454/6efe83e4-9c33-4548-a716-38e48cd503b3)

![Screenshot 2023-05-20 225753](https://github.com/Abrinnisha6/Ex-08-Data-Visualization_1/assets/118889454/e8fbd98e-0e86-468d-a1c4-ab97241b9803)

![Screenshot 2023-05-20 225803](https://github.com/Abrinnisha6/Ex-08-Data-Visualization_1/assets/118889454/0421861b-66aa-4ec9-a1c1-05855ecb637b)

![Screenshot 2023-05-20 225812](https://github.com/Abrinnisha6/Ex-08-Data-Visualization_1/assets/118889454/3ffafb66-036d-4d86-86ea-84b316c29931)

![Screenshot 2023-05-20 225901](https://github.com/Abrinnisha6/Ex-08-Data-Visualization_1/assets/118889454/ce9614c1-9bf5-41ab-9c00-7988a1fbfd3e)

![Screenshot 2023-05-20 225909](https://github.com/Abrinnisha6/Ex-08-Data-Visualization_1/assets/118889454/7115953f-fc6b-42dd-8c5d-761df1281b46)

![Screenshot 2023-05-20 225951](https://github.com/Abrinnisha6/Ex-08-Data-Visualization_1/assets/118889454/e4a86a5d-67d6-4749-b4d5-e34924ba8c41)

![Screenshot 2023-05-20 230000](https://github.com/Abrinnisha6/Ex-08-Data-Visualization_1/assets/118889454/2e224949-8f0e-4c1f-b845-6f608a1db02c)

![Screenshot 2023-05-20 230055](https://github.com/Abrinnisha6/Ex-08-Data-Visualization_1/assets/118889454/ee51ab9c-b532-4bfe-8b49-f8abefab0b9e)

![Screenshot 2023-05-20 230103](https://github.com/Abrinnisha6/Ex-08-Data-Visualization_1/assets/118889454/d3ba40ee-e04f-47bb-b63f-0fc4809237fe)

![Screenshot 2023-05-20 230149](https://github.com/Abrinnisha6/Ex-08-Data-Visualization_1/assets/118889454/e72e0784-0e9d-4db8-b0b1-f188b0031009)

![Screenshot 2023-05-20 230157](https://github.com/Abrinnisha6/Ex-08-Data-Visualization_1/assets/118889454/bcf24d1f-a663-4dc1-aa99-fc186dc7e4d1)

![Screenshot 2023-05-20 230232](https://github.com/Abrinnisha6/Ex-08-Data-Visualization_1/assets/118889454/3c886e91-ff0b-4ab9-bd38-6f03d7c03f9b)

![Screenshot 2023-05-20 230243](https://github.com/Abrinnisha6/Ex-08-Data-Visualization_1/assets/118889454/87ee88ca-522c-4143-b2b7-ce85a6273f11)

![Screenshot 2023-05-20 230251](https://github.com/Abrinnisha6/Ex-08-Data-Visualization_1/assets/118889454/1360109b-45ea-40ba-872f-96d661b12c0d)

![Screenshot 2023-05-20 230340](https://github.com/Abrinnisha6/Ex-08-Data-Visualization_1/assets/118889454/54c56b6e-5b8d-4c06-8048-f3f8a9d18cb0)

![Screenshot 2023-05-20 230351](https://github.com/Abrinnisha6/Ex-08-Data-Visualization_1/assets/118889454/9a1640f4-86e4-487d-a19a-8172d54d848b)

![Screenshot 2023-05-20 230402](https://github.com/Abrinnisha6/Ex-08-Data-Visualization_1/assets/118889454/7856ccc2-d303-4b24-b899-e3d285e4dab1)

![Screenshot 2023-05-20 230409](https://github.com/Abrinnisha6/Ex-08-Data-Visualization_1/assets/118889454/28503e6a-7630-446b-86da-24a4b1480b65)

![Screenshot 2023-05-20 230535](https://github.com/Abrinnisha6/Ex-08-Data-Visualization_1/assets/118889454/13563f33-c5ef-493c-acdb-0010bf019a70)

![Screenshot 2023-05-20 230549](https://github.com/Abrinnisha6/Ex-08-Data-Visualization_1/assets/118889454/ee4af932-ed4a-4e53-8ef5-d934d343e153)

![Screenshot 2023-05-20 230631](https://github.com/Abrinnisha6/Ex-08-Data-Visualization_1/assets/118889454/21607649-b28e-4644-b296-b89604640744)

## Result :

Hence,Data Visualization is applied on the complex dataset using libraries like Seaborn and Matplotlib successfully and the data is saved to file.
