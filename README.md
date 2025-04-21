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

import pandas as pd
 
df = pd.read_csv("/content/SAMPLEIDS.csv")  

df

![Screenshot 2025-04-20 212944](https://github.com/user-attachments/assets/31560465-13a3-49f4-90ec-83201c1ffa9d)

df.isnull()

![Screenshot 2025-04-20 213158](https://github.com/user-attachments/assets/de82b717-c719-4ac1-8d41-9e84a1d076ce)

df.notnull()

![Screenshot 2025-04-20 213208](https://github.com/user-attachments/assets/407cc175-8ad5-468c-9d08-71d84ac5287e)

df.dropna(axis=1)

![Screenshot 2025-04-20 213218](https://github.com/user-attachments/assets/250a8bcb-84ee-4df7-b431-f7aa4c81bf7a)

df.dropna(axis=0)

![Screenshot 2025-04-20 213226](https://github.com/user-attachments/assets/64ceff09-8107-4768-834d-5cf7cf305594)

dfs = df[df['TOTAL'] > 270]

dfs

![Screenshot 2025-04-20 213233](https://github.com/user-attachments/assets/09cd277a-6785-4b19-8539-72b1715ef2bd)

dfs = df[df['NAME'].str.startswith(('A','C')) & (df['TOTAL'] > 250)]

df.iloc[:4]

df.iloc[0:4,1:4]

df.iloc[[1,3,5], [1,3]]

df

![Screenshot 2025-04-20 213240](https://github.com/user-attachments/assets/c64eb0c7-6517-4534-a6d2-8104af21fa2e)
![Screenshot 2025-04-20 213247](https://github.com/user-attachments/assets/0bf25221-1ffe-4ff6-a31e-1eef2092af27)
![Screenshot 2025-04-20 213251](https://github.com/user-attachments/assets/39411c2f-0dd5-4b1f-92aa-1fcc7a189864)
![Screenshot 2025-04-20 213259](https://github.com/user-attachments/assets/1317da55-1b48-4f5d-b336-5109fdccf398)
dff = df.fillna(0)

dff

![Screenshot 2025-04-20 213310](https://github.com/user-attachments/assets/1fa07358-c82d-40bb-b01e-96909e7d6e18)

df.fillna(method = 'ffill')

![Screenshot 2025-04-20 213320](https://github.com/user-attachments/assets/afe2865f-052d-412d-9ee4-25a2dfff79c1)

df.fillna(method='bfill')


![Screenshot 2025-04-20 213331](https://github.com/user-attachments/assets/7b17177e-13d8-4dff-b085-57cd31d7eafb)

df['TOTAL'].fillna(value=df['TOTAL'].mean())


![Screenshot 2025-04-20 213339](https://github.com/user-attachments/assets/8fad3493-7c41-44a0-9ce6-a5310cef1305)

import seaborn as sns

import numpy as np

age = [1, 3, 28, 27, 25, 92, 30, 39, 40, 50, 26, 24, 29, 94]

af = pd.DataFrame(age)

af

![Screenshot 2025-04-20 213354](https://github.com/user-attachments/assets/9c951355-3c4d-4a65-96b0-3b892b027d6d)

sns.boxplot(af)

![Screenshot 2025-04-20 213359](https://github.com/user-attachments/assets/b0a1f47d-c907-4d46-99ed-3a99da4a3d8b)

q1 = af.quantile(0.25)
q2 = af.quantile(0.50)
q3 = af.quantile(0.75)
iqr = q3-q1
iqr

![Screenshot 2025-04-20 213406](https://github.com/user-attachments/assets/de3afa65-1cdb-4dd4-8d74-e67fdadd7d87)

Q1 = np.quantile(age, 0.25)
Q2 = np.quantile(age, 0.50)
Q3 = np.quantile(age, 0.75)
IQR = Q3-Q1
IQR
     
np.float64(14.5)

lower_bound = Q1 - (1.5*IQR)

upper_bound = Q3 + (1.5*IQR)

upper_bound

np.float64(61.5)

lower_bound

np.float64(3.5)

outliers = [x for x in age if x < lower_bound or x > upper_bound]
     
print("Q1:",Q1)

print("Q2:",Q2)

print("Q3:",Q3)

print("IQR:",IQR)

print("Lower Bound:",lower_bound)

print("Upper Bound:",upper_bound)

print("Outliers:",outliers)
     
Q1: 25.25

Q2: 28.5

Q3: 39.75

IQR: 14.5

Lower Bound: 3.5

Upper Bound: 61.5

Outliers: [1, 3, 92, 94]

af = af[(af >= lower_bound) & (af <= upper_bound)]

af

![Screenshot 2025-04-20 213434](https://github.com/user-attachments/assets/64fd4c3c-15e0-4f04-bedf-01b421f869da)

af.dropna()


![Screenshot 2025-04-20 213440](https://github.com/user-attachments/assets/bf5c627e-de9e-48d2-808c-a065e74a664f)

sns.boxplot(data=af)


![Screenshot 2025-04-20 213446](https://github.com/user-attachments/assets/127fba15-e0e6-4011-862b-88ce3d8928c2)

sns.scatterplot(data=af)


![Screenshot 2025-04-20 213456](https://github.com/user-attachments/assets/02da00bb-5573-436c-a721-84dd8236bee0)
  
from scipy import stats

data = [1,2,2,2,3,1,1,15,2,2,2,3,1,1,2]

mean = np.mean(data)

std = np.std(data)

print(mean,std)
     
2.6666666666666665 
3.3598941782277745

threshold = 3

outliers = []

for i in data:

  z_score = (i-mean)/std
  
  if np.abs(z_score) > threshold:
  
    outliers.append(i)
    
print(outliers)

[15]

data = {'weight':[12,15,18,21,24,27,30,33,36,39,42,45,51,54,57,60,63,66,69,202,72,75,78,81,256,258,98,99,232,90,93,96]}

df = pd.DataFrame(data)

df

![Screenshot 2025-04-20 213532](https://github.com/user-attachments/assets/f2ed8465-a55c-4b54-84cd-3d9b5363a7f8)

val = [12,15,18,21,24,27,30,33,36,39,42,45,51,54,57,60,63,66,69,202,72,75,78,81,256,258,98,99,232,90,93,96]

out = []

def d_o(val):

  ts=3
  
  mean = np.mean(val)
  
  std = np.std(val)
  
  for i in val:
  
    z_score = (i-mean)/std
    
    if np.abs(z_score) > ts:
    
      out.append(i)
    
    return out

![Screenshot 2025-04-20 213541](https://github.com/user-attachments/assets/a91791f5-b2e3-44ff-84fe-21303945b17a)


op = d_o(val)

id = pd.read_csv("/content/iris.csv")

id

![Screenshot 2025-04-20 213541](https://github.com/user-attachments/assets/d1a2c8cc-d8e3-4821-8f1c-14ee12703f4b)

sns.boxplot(x = 'sepal_width',data=id)

![Screenshot 2025-04-20 213548](https://github.com/user-attachments/assets/d219750b-6b48-4c02-8e1d-145fffc7f15d)

c1 = id.sepal_width.quantile(0.25)

c3 = id.sepal_width.quantile(0.75)

iqr = c3-c1

print(c3)
     
3.3

rid = id[(id.sepal_width >= c1-1.5*iqr) & (id.sepal_width <= c3+1.5*iqr)]

rid

![Screenshot 2025-04-20 213555](https://github.com/user-attachments/assets/8fa8c997-d5b6-4d6f-b70c-fc9849f696a4)


delid=id[~((id.sepal_width<(c1-1.5*iqr))) | (id.sepal_width>( (3 + 1.5 * 19) )) ]

delid

![Screenshot 2025-04-20 213606](https://github.com/user-attachments/assets/e5594fb8-0c48-4034-bc2d-d39767bad358)

sns.boxplot(x = 'sepal_width',data = delid)

![Screenshot 2025-04-20 213611](https://github.com/user-attachments/assets/d74528a3-f398-4c20-bfdd-76024bd05723)

# Result

Performed Data Cleaning process and Saved the cleaned data to a file.
