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

# Coding and Output:
```
import pandas as pd
import numpy as np
import seaborn as sns
import scipy.stats as stats
import matplotlib.pyplot as plt

# Read dataset
df = pd.read_csv("SAMPLEIDS.csv")
df
df.head()
df.tail()
df.info()
df.describe()
df.isnull().sum()
df.isnull().any()

df.dropna()
df.fillna(0)
df.fillna(method='ffill')
df.fillna({'GENDER':'MALE','NAME':'SRI'})

# Iris dataset
ir = pd.read_csv("iris.csv")
ir
ir.describe()

# ------------------- BOXPLOT BEFORE OUTLIER REMOVAL -------------------
sns.boxplot(x='sepal_width', data=ir)
plt.title("Boxplot Before Removing Outliers")
plt.show()

# ------------------- SCATTER PLOT BEFORE CLEANING -------------------
ir.plot.scatter(x='sepal_length', y='sepal_width', title="Before Removing Outliers")
plt.show()

# ------------------- IQR METHOD -------------------
Q1 = ir.sepal_width.quantile(0.25)
Q3 = ir.sepal_width.quantile(0.75)
IQR = Q3 - Q1
print(IQR)

# Outliers
ran = ir[((ir.sepal_width < (Q1 - 1.5 * IQR)) | (ir.sepal_width > (Q3 + 1.5 * IQR)))]
ran['sepal_width']

# Remove outliers
ran = ir[~((ir.sepal_width < (Q1 - 1.5 * IQR)) | (ir.sepal_width > (Q3 + 1.5 * IQR)))]
ran['sepal_width']

# ------------------- BOXPLOT AFTER IQR -------------------
sns.boxplot(x='sepal_width', data=ran)
plt.title("Boxplot After IQR")
plt.show()

# ------------------- SCATTER AFTER IQR -------------------
ran.plot.scatter(x='sepal_length', y='sepal_width', title="After IQR Outlier Removal")
plt.show()

# ------------------- Z-SCORE METHOD -------------------
z = np.abs(stats.zscore(ir['petal_length']))
z

ir1 = ir[z < 3]
ir1

# ------------------- SCATTER AFTER Z-SCORE -------------------
ir1.plot.scatter(x='petal_length', y='petal_width', title="After Z-score Outlier Removal")
plt.show()
```

<img width="510" height="425" alt="Screenshot 2026-05-13 162108" src="https://github.com/user-attachments/assets/50f9824f-a6cb-4a1f-8b4a-d4f83830359c" />
<img width="1007" height="716" alt="Screenshot 2026-05-13 162150" src="https://github.com/user-attachments/assets/24734dde-4a45-4c7f-b61d-af365bb8b7cb" />
<img width="505" height="302" alt="Screenshot 2026-05-13 162157" src="https://github.com/user-attachments/assets/410270bb-b6e6-46de-8a1e-b52656ac78dc" />
<img width="838" height="537" alt="Screenshot 2026-05-13 162206" src="https://github.com/user-attachments/assets/88fa6524-b758-48fa-af74-64d996779b35" />
<img width="892" height="551" alt="Screenshot 2026-05-13 162218" src="https://github.com/user-attachments/assets/29f22491-bd51-4cbf-81cd-988d5f0da2c4" />
<img width="173" height="77" alt="Screenshot 2026-05-13 162224" src="https://github.com/user-attachments/assets/8148e82c-bef5-4ed6-8fbe-eab2d148f66f" />
<img width="347" height="137" alt="Screenshot 2026-05-13 162232" src="https://github.com/user-attachments/assets/05eef976-4f0e-4a43-ac4d-e8dc6b0c36a1" />
<img width="615" height="286" alt="Screenshot 2026-05-13 162241" src="https://github.com/user-attachments/assets/06dd4d92-5918-449e-9d62-759b878faf68" />
<img width="842" height="570" alt="Screenshot 2026-05-13 162248" src="https://github.com/user-attachments/assets/f89b9cd0-6dbd-4715-b241-4e8f385b6a0b" />
<img width="827" height="585" alt="Screenshot 2026-05-13 162256" src="https://github.com/user-attachments/assets/9f2edf82-c237-4f8a-a528-b1c968c415ea" />
<img width="722" height="422" alt="Screenshot 2026-05-13 162305" src="https://github.com/user-attachments/assets/4e8c3de8-19d7-414a-a04b-06fa0ac0b0ec" />
<img width="828" height="587" alt="Screenshot 2026-05-13 162318" src="https://github.com/user-attachments/assets/13ae58eb-c424-4a6c-87af-d9dd527e85b6" />


























# Result
          The given data has been successfully read, cleaned by handling duplicates and missing values, and saved to a new file named cleaned_data.csv.
