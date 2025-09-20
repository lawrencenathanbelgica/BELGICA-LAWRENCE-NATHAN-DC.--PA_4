# BELGICA-LAWRENCE-NATHAN-DC.--PA_4


# Programming Assignment (PA#4)

The purpose of this assignment is to practice **data analysis, visualization, and handling CSV/Excel files** using Python. This README serves as a guide to explain what each notebook does, the logic behind the solutions, and how to run them.  

This repository contains my submission for **Programming Assignment #4** in  
**ECE 2112: Advanced Computer Programming and Algorithms**.  

---

## 1. Data Importing  
**Goal:** Load CSV/Excel files into Python for analysis.  

**Process:**  
1. Use the **`pandas`** library to read data.  
2. Display the first few rows using `.head()`.  
3. Verify dataset information using `.info()` and `.describe()`.  

**Code Snippet:**  
```python
import pandas as pd

data = pd.read_csv("data.csv")   # or pd.read_excel("data.xlsx")
print(data.head())
print(data.info())
```

## 2. Compute Average Scores
We create a new column **Average** which is the mean of the four subjects:

```python

subs = ['Electronics', 'Math', 'GEAS', 'Communication']
df['Average'] = df[subs].mean(axis=1)
```

## 3. Visualization by Gender
We group by **Gender** and compute the mean of the average scores.
```python
plt.figure(figsize=(6,4))
gender_avg = df.groupby('Gender')['Average'].mean()

plt.bar(gender_avg.index, gender_avg.values)

plt.xlabel('Gender')
plt.ylabel('Average Score')
plt.title('Average Scores by Gender')
plt.show()
```

## 4. Visualization by Hometown
We group by **Hometown** and plot the results.

```python
plt.figure(figsize=(6,4))
hometown_avg = df.groupby('Hometown')['Average'].mean()

plt.bar(hometown_avg.index, hometown_avg.values)

plt.xlabel('Hometown')
plt.ylabel('Average Score')
plt.title('Average Scores by Hometown')
plt.show()
```

## 5. Visualization by Track
We group by **Track** and plot the results.


## 6. Interpretation

- The Gender chart shows differences in average performance between male and female students.
- The Hometown chart reveals which places have higher or lower average scores.
- The Track chart highlights how students from different tracks perform on average.
