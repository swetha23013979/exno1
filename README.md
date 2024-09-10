# Exno:1
Data Cleaning Process

# AIM
To read the given data and perform data cleaning and save the cleaned data to a file.

# Explanation
Data cleaning is the process of preparing data for analysis by removing or modifying data that is incorrect ,incompleted , irrelevant , duplicated or improperly formatted. Data cleaning is not simply about erasing data ,but rather finding a way to maximize datasets accuracy without necessarily deleting the information.

# Algorithm
STEP 1: Read the given Data

STEP 2: Get the information about the data

STEP 3: Remove the null values from the data

STEP 4: Save the Clean data to the file

STEP 5: Remove outliers using IQR

STEP 6: Use zscore of to remove outliers

# Coding and Output
```
import pandas as pd
df=pd.read_csv("/content/SAMPLEIDS.csv")
df
```
![image](https://github.com/user-attachments/assets/75855444-e439-4a95-97d7-546b3e25d8da)
```
df.shape
```
![image](https://github.com/user-attachments/assets/4092d6b6-3890-41a2-9790-d6855c18ae78)

```
df.describe()
```
![image](https://github.com/user-attachments/assets/fe118acd-66f7-426d-aeec-fc4895393752)
```
df.info()
```
![image](https://github.com/user-attachments/assets/991718e9-430b-4c61-a68a-ca2d7c5eada8)

```
df.tail()
```
![image](https://github.com/user-attachments/assets/8cbb9f1d-96fc-431c-879f-ab982e7a1042)

```
df.head()
```
![image](https://github.com/user-attachments/assets/f62b1533-ea37-4ac7-838e-2c476c5b0942)

```
df.isnull().sum()
```
![image](https://github.com/user-attachments/assets/ece53b89-4d84-4500-ae84-7d1e5e1324bd)

```
df.dropna(how='any').shape
```
![image](https://github.com/user-attachments/assets/1674e140-16bb-4f3a-b173-70a0bb12217d)

```
df.shape
```
![image](https://github.com/user-attachments/assets/74b8da59-5435-47b6-880e-d6e21ec14ca3)

```
ms=df.TOTAL.mean()
ms
```
![image](https://github.com/user-attachments/assets/1044326b-c0ef-438f-8840-3b164ede46e9)
```
df.TOTAL.fillna(ms,inplace=True)
df
```
![image](https://github.com/user-attachments/assets/75c1253d-ebd0-4efd-ab54-31dbac6eb4a0)

```
df['M1'].fillna(method='ffill',inplace=True)
```
![image](https://github.com/user-attachments/assets/0a977422-0905-45ce-a5ed-31ec55d2df85)

```
df.isna().sum()
```
![image](https://github.com/user-attachments/assets/6a1a3c05-3fcd-4f65-8a04-590368c6959b)

```
df.duplicated()
```
![image](https://github.com/user-attachments/assets/a8128eaa-bba4-4c0f-bdbf-0e70709ad75e)
```
df.drop_duplicates(inplace=True)
df
```
![image](https://github.com/user-attachments/assets/c05d208a-7277-4ec7-8063-d0fbb0641cad)
```
df.duplicated()
```
![image](https://github.com/user-attachments/assets/7a18e090-8ab1-4fcc-9067-422a9c388e5a)
```
df['DOB']
```
![image](https://github.com/user-attachments/assets/bc369818-6bc6-4ed3-abdd-e844ab0ec6d3)
```
import seaborn as sns
sns.heatmap(df.isnull(),yticklabels=False,annot=True)
```
![image](https://github.com/user-attachments/assets/a65abea1-b1aa-4544-a83e-c0e0f30c1ee7)

```
# Outliers Detection and Removal using IQR

import pandas as pd
import seaborn as sns
import numpy as np
swe=[1,3,28,27,25,92,30,39,40,50,26,24,29,94]
ms=pd.DataFrame(swe)
ms
```
![image](https://github.com/user-attachments/assets/a15b5b62-dda0-4264-bad9-745dbad2467d)

```
sns.boxplot(data=ms)
```
![image](https://github.com/user-attachments/assets/067e17e0-d457-49bc-8d68-ae23960f4612)

```
sns.scatterplot(data=ms)
```
![image](https://github.com/user-attachments/assets/669cf3de-3285-47a0-9896-ad88ae30cb23)

```
q1=ms.quantile(0.25)
q2=ms.quantile(0.05)
q3=ms.quantile(0.75)
IQR=q3-q1
IQR
```
![image](https://github.com/user-attachments/assets/767db89a-8f0f-4d28-81d0-727f5adf65c3)
```
q1=np.percentile(ms,25)
q2=np.percentile(ms,50)
q3=np.percentile(ms,75)
IQR=q3-q1
IQR
```
![image](https://github.com/user-attachments/assets/f1bbf64d-3334-4db1-91fb-9f4a618c1955)

```
low=q1-1.5*IQR
upp=q1+1.5*IQR
low
```
![image](https://github.com/user-attachments/assets/b500f511-19cc-4789-9603-e325775724b8)
```
upp
```
![image](https://github.com/user-attachments/assets/e0f51914-1203-4d10-88f6-69ef242ad6a8)
```
outliers=[x for x in swe if x<low or x>upp]
print("q1 : ",q1)
print("q3 : ",q3)
print("IQR : ",IQR)
print("low : ",low)
print("upp : ",upp)
print("outliers : ",outliers)
```

![image](https://github.com/user-attachments/assets/c49f676f-7167-4032-9153-2d61bbdfee61)

```
ms=ms[((ms>=low)&(ms<=upp))]
ms
```

![image](https://github.com/user-attachments/assets/a9549a4b-2244-4361-8e5e-e216ff9d6b5a)

```
ms.dropna()
```
![image](https://github.com/user-attachments/assets/82b863d4-623d-44ba-ad9d-f4ae5b5887bd)
```
data=[1,2,2,2,3,1,1,15,2,2,2,3,1,1,2]
mean=np.mean(data)
std=np.std(data)
print("MEAN : ",mean)
print("STANDARD DEVIATION : ",std)
```
![image](https://github.com/user-attachments/assets/0bd27427-274f-455a-a703-7a12ea61edb0)
```
thresh=3
outlier=[]
for i in data:
  z=(i-mean)/std
  if z > thresh:
    outlier.append(i)
print("outlier in dbs is",outlier)
```
![image](https://github.com/user-attachments/assets/94c4177d-9865-44ac-af0c-f6fdf3e380d4)
```
from scipy import stats
data={'weight':[12,15,18,21,24,27,30,33,36,39,42,45,48,51,54,57,60,63,66,69,202,72,75,78,81,84,232,87,90,93,96,99,258]}
ms=pd.DataFrame(data)
ms
```

![image](https://github.com/user-attachments/assets/013d4b85-c04e-4ba0-9e7f-3684f16fd2ab)

```
z=np.abs(stats.zscore(ms))
print(ms[z['weight']>3])
```

![image](https://github.com/user-attachments/assets/f09e2239-59b5-4ff5-a453-b8e3c842a7de)



# Result
         Thus we have cleaned the data and removed the outliers by detection using IQR and Z-score
method.
