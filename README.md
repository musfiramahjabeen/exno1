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
## Data Cleaning
```python
import pandas as pd
# READ CSV FILE HERE
df=pd.read_csv('Data_set.csv')
df
```
![Screenshot 2024-08-22 215203](https://github.com/user-attachments/assets/8cbe9116-c92c-4b01-9fb2-2cdb6d0f306b)

```python
# CHECK OUT NULL VALUES IN DATA SET USING FUNCTION
df_null=df.isnull()
df_null
```
![image](https://github.com/user-attachments/assets/b66be31e-e6a4-4fa4-ba8e-fe4a9b11c38e)


```python
# DISPLAY THE SUM ON NULL VALUES IN EACH ROWS
df_null_sum=df.isnull().sum()
df_null_sum
```
![image](https://github.com/user-attachments/assets/5f359e21-cf0d-4c49-8d75-857a0df0c7a6)

```python
# DROP NULL VALUES
df_dropna=df.isnull().dropna()
df_dropna
```
![image](https://github.com/user-attachments/assets/40780ff9-c331-44f1-8060-5ca362b3149c)

```python
# FILL NULL VALUES WITH CONSTANT VALUE "O"
df_nafill_0=df.fillna(0)
df_nafill_0
```
![image](https://github.com/user-attachments/assets/27126c1f-36cf-4dea-9c6f-76adb4fa8d3e)

```python
# FILL NULL VALUES WITH ffill METHOD
df_ffill=df.ffill()
df_ffill
```
![image](https://github.com/user-attachments/assets/aff4eb3c-21c3-4158-bf9f-541c3bd4101b)

```python
# FILL NULL VALUES WITH bfill METHOD
df_bfill=df.bfill()
df_bfill
```
![image](https://github.com/user-attachments/assets/d86b061a-859a-4973-9497-2812f336dbd9)

```python
# CALCULATE MEAN VALUE OF A COLUMN AND FILL IT WITH NULL VALUES
df_mean1=df['num_episodes'].fillna(df['num_episodes'].mean())
df_mean1
```
![image](https://github.com/user-attachments/assets/ff5eae28-0aa7-47eb-b55b-2c9426f41556)

```python
df_mean2=df['rating'].fillna(df['rating'].mean())
df_mean2
```
![image](https://github.com/user-attachments/assets/b19225ab-bd0e-4364-b9a0-124408a16691)

```python
df_mean3=df['current_overall_rank'].fillna(df['current_overall_rank'].mean())
df_mean3
```
![image](https://github.com/user-attachments/assets/a43c7427-54f9-457f-97db-55288d3ce170)

```python
df_mean4=df['lifetime_popularity_rank'].fillna(df['lifetime_popularity_rank'].mean())
df_mean4
```
![image](https://github.com/user-attachments/assets/d53ce17c-7ee5-408f-8c5d-31f7759d22b7)

```python
df_mean5=df['watchers'].fillna(df['watchers'].mean())
df_mean5
```
![image](https://github.com/user-attachments/assets/1cd4cdba-c3bd-43bc-9f17-5e39473369cf)

```python
# DROP NULL VALUES
df_dropna=df.dropna()
df_dropna
```
![image](https://github.com/user-attachments/assets/419106ad-e27d-4791-9044-ddc7cf522cd6)

## Outlier Detection and Removal
### IQR
```python
import pandas as pd
import seaborn as sns

age=[1,3,28,27,25,92,30,39,40,50,26,24,29,94]
af=pd.DataFrame(age)
af
```
![image](https://github.com/user-attachments/assets/e9c67107-7ead-42cd-a17d-605a6d391720)

```python
# USE BOXPLOT FUNCTION HERE TO DETECT OUTLIER
sns.boxplot(af)
```
![image](https://github.com/user-attachments/assets/071df396-d3cc-4189-8c2d-fe30d39ff2d7)

```python
sns.scatterplot(af)
```
![image](https://github.com/user-attachments/assets/46d3ae5e-03ff-465e-81d4-b17012f18fe6)

```python
q1=af.quantile(0.25)
q2=af.quantile(0.5)
q3=af.quantile(0.75)
iqr=q3-q1
iqr
```
![image](https://github.com/user-attachments/assets/207ffd0a-1b68-4998-b854-52b1f0f5b6c1)

```python
import numpy as np
Q1=np.percentile(af,25)
Q2=np.percentile(af,50)
Q3=np.percentile(af,75)
IQR=Q3-Q1

lower_bound=Q1-1.5*IQR
upper_bound=Q3+1.5*IQR

outliers=[x for x in age if x < lower_bound.iloc[0] or x > upper_bound.iloc[0]]
```
![image](https://github.com/user-attachments/assets/a607fbe4-e862-4b7c-9d16-95fb1753aa83)

```python
print('Q1:',Q1)
print('Q3:',Q3)
print('IQR:',IQR)
print('Lower bound:',lower_bound)
print('Upper bound:',upper_bound)
print('Outliers:',outliers)
```
![image](https://github.com/user-attachments/assets/0a883253-1a5c-4345-8fe5-1b7444825271)

```python
af=af[((af>=lower_bound)&(af<=upper_bound))]
af
```
![image](https://github.com/user-attachments/assets/cb588902-ae6b-4a74-8efe-8dd11f5f2ebe)

```python
af.dropna()
```
![image](https://github.com/user-attachments/assets/d8d09821-fdac-4f85-9625-dbcd1f5fba52)

```python
sns.boxplot(af)
```
![image](https://github.com/user-attachments/assets/99cefbc3-b9cc-4457-9317-0cd9a840ef2f)

```python
sns.scatterplot(af)
```
![image](https://github.com/user-attachments/assets/4c48136a-1b22-41e4-bc74-b6a7dae985a0)
### Z Score
```python
from scipy import stats #STATS METHOD IS USED TO IMPLEMENT Z SCORE METHOD
import numpy as np
import pandas as pd
import seaborn as sns
data=[1,12,15,18,21,24,27,30,33,36,39,42,45,48,51,54,57,60,63,66,69,72,75,78,81,84,87,90,93,96,99,158]
df=pd.DataFrame(data)

# USE BOXPLOT FUNCTION HERE TO DETECT OUTLIER
sns.boxplot(df)
```
![image](https://github.com/user-attachments/assets/a47878f6-cd0a-4068-87d5-35c756d44d21)

```python
mean=np.mean(data)
mean

std=np.std(data)
std

# PERFORM Z SCORE METHOD AND DETECT OUTLIER VALUES
z=np.abs(stats.zscore(df))
z
```
![image](https://github.com/user-attachments/assets/e2eb086f-8450-4b38-ad62-f1cbcf32e088)

```python
threshold=3
outliers = df[abs(df) > 3]
print("Outliers:")
print(outliers)
```
![image](https://github.com/user-attachments/assets/32a06acd-3a7c-429f-9970-6fb6f6c77768)

```python
# Remove outliers
df_cleaned = df[(z <= threshold)]
df_cleaned
```
![image](https://github.com/user-attachments/assets/53d445b6-4a67-47c4-8ea8-65fc2970e027)

```python
# USE BOXPLOT FUNCTION HERE TO CHECK OUTLIER IS REMOVED
sns.boxplot(df_cleaned)
```
![image](https://github.com/user-attachments/assets/9e7360ee-dbfe-48fb-a27b-f98692c112eb)

```python
sns.scatterplot(df_cleaned)
```
![image](https://github.com/user-attachments/assets/aba75e49-cd64-4477-bdbd-9847916dbc2c)

# Result
Thus we have cleaned the data and removed the outliers by detection using IQR and Z-score method.
