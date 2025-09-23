# BELGICA-LAWRENCE-NATHAN-DC.--PA_4

# Programming Assignment (PA#4)  
**Course:** ECE 2112 – Advanced Computer Programming and Algorithms  

The purpose of this assignment is to practice **data wrangling, analysis, and visualization** using Python.  
This README explains the logic of each step in detail and provides **line-by-line explanations** of the code.  

---

## About the Files
- **board2.csv** → A CSV file containing the dataset of the ECE Board Exam 2.  
- **PA4_BELGICA.ipynb** → A Jupyter Notebook file that contains my solution to the assignment problem using **data wrangling** and **visualization**.  

---

## PA#4
> **Task:** Using data wrangling and visualization, create new DataFrames from the dataset based on given conditions, and generate visualizations that explain how chosen features (Track, Gender, Hometown) contribute to student performance.  

---

## 1. Import Libraries and Dataset  

```python
import pandas as pd    # Imports the pandas library for data handling
```

- **import pandas as pd** → Loads the pandas library, which is essential for handling tabular data.
- The alias **pd** is used to shorten function calls (**pandas.read_csv** → **pd.read_csv**).

```python
eceboard = pd.read_csv("board2.csv")   # Loads the dataset from board2.csv
```
- **pd.read_csv("board2.csv")** → Reads the CSV file into a DataFrame named **eceboard**.
- The DataFrame is like a table that allows row/column operations.

```python
print(eceboard.head())   # Displays the first 5 rows of the dataset
```
- **.head()** helps check if the dataset was loaded correctly and shows the column structure.

## 2. Creating DataFrame: **Instru**
Condition:
- Track = Instrumentation
- Hometown = Luzon
- Electronics > 70
Output Columns: Name, GEAS, Electronics

```python
Instru = eceboard.loc[
    (eceboard['Electronics'] > 70) &              # Selects rows where Electronics > 70
    (eceboard['Hometown'] == 'Luzon') &           # Selects rows where Hometown is Luzon
    (eceboard['Track'] == 'Instrumentation'),     # Selects rows where Track is Instrumentation
    ['Name', 'GEAS', 'Electronics']               # Keeps only the specified columns
]
```
### Explanation (line by line):

- **(eceboard['Electronics'] > 70)** → Finds all students with Electronics scores greater than 70.
  
- **(eceboard['Hometown'] == 'Luzon')** → Filters only those from Luzon.
  
- **(eceboard['Track'] == 'Instrumentation')** → Ensures they belong to the Instrumentation track.
  
- **eceboard.loc[ ... , ['Name', 'GEAS', 'Electronics']]** → Keeps only the Name, GEAS, and Electronics columns.
  
- Final DataFrame is saved as **Instru**.

## 3. Creating DataFrame: Mindy  

**Condition:**  
- Gender = Female  
- Hometown = Mindanao  
- Average ≥ 55  
- **Output Columns:** Name, Track, Electronics, Average  

---

#### Step 1: Create a new column `Average`  
This computes the mean score of all subjects (`Electronics`, `Math`, `GEAS`, `Communication`).  

```python
# First, create a new column 'Average' that computes the mean score of all subjects
eceboard['Average'] = eceboard[['Electronics', 'Math', 'GEAS', 'Communication']].mean(axis=1)
```
Explanation:

- **eceboard[['Electronics', 'Math', 'GEAS', 'Communication']]** → Selects the four subject columns.
- **.mean(axis=1)** → Computes the row-wise average (axis=1 means “across columns”).
- **eceboard['Average']** = ... → Stores the result in a new column called **Average**.

#### Step 2:Apply the filtering conditions
We now create a new DataFrame called Mindy that satisfies the given conditions.

```python
Mindy = eceboard.loc[
    (eceboard['Gender'] == 'Female') &            # Selects rows where Gender is Female
    (eceboard['Hometown'] == 'Mindanao') &        # Selects rows where Hometown is Mindanao
    (eceboard['Average'] >= 55),                  # Selects rows with Average score ≥ 55
    ['Name', 'Track', 'Electronics', 'Average']   # Keeps only the specified columns
]
```

Explanation:

- (eceboard['Gender'] == 'Female') → Filters only female students.
- (eceboard['Hometown'] == 'Mindanao') → Ensures their hometown is Mindanao.
- (eceboard['Average'] >= 55) → Keeps only those with average scores ≥ 55.
- ['Name', 'Track', 'Electronics', 'Average'] → Displays only the required columns.

The resulting DataFrame Mindy includes Name, Track, Electronics, and Average columns for students that match the conditions.

## 4. Visualization by Gender  

We analyze the performance differences between male and female students by plotting the **average scores by gender**.  

```python
import matplotlib.pyplot as plt   # Import matplotlib for plotting

plt.figure(figsize=(6,4))         # Sets the figure size
gender_avg = eceboard.groupby('Gender')['Average'].mean()   # Groups by Gender and computes mean Average

plt.bar(gender_avg.index, gender_avg.values)   # Creates a bar chart
plt.xlabel('Gender')                           # X-axis label
plt.ylabel('Average Score')                    # Y-axis label
plt.title('Average Scores by Gender')          # Title of the chart
plt.show()                                     # Displays the plot
```
Explanation:

- groupby('Gender') → Splits data into Male/Female groups.
- ['Average'].mean() → Computes the mean average score per gender.
- plt.bar(...) → Draws bars representing male vs. female performance.

## 5. Visualization by Hometown  

We visualize the **average scores by hometown** to identify geographical performance trends.  

```python
plt.figure(figsize=(6,4))
hometown_avg = eceboard.groupby('Hometown')['Average'].mean()

plt.bar(hometown_avg.index, hometown_avg.values)
plt.xlabel('Hometown')
plt.ylabel('Average Score')
plt.title('Average Scores by Hometown')
plt.show()
```

Explanation:

- groupby('Hometown') → Groups data based on students’ hometowns.
- ['Average'].mean() → Calculates the mean average score for each hometown.
- plt.bar(...) → Creates a bar chart comparing performance across different hometowns.

### 6. Visualization by Track  

We compare the **average scores of students across different academic tracks**.  

```python
plt.figure(figsize=(6,4))
track_avg = eceboard.groupby('Track')['Average'].mean()

plt.bar(track_avg.index, track_avg.values)
plt.xlabel('Track')
plt.ylabel('Average Score')
plt.title('Average Scores by Track')
plt.show()
```

Explanation:

- groupby('Track') → Groups students according to their academic track (e.g., Instrumentation, Communication).
- ['Average'].mean() → Computes the mean average score for each track.
- plt.bar(...) → Draws a bar chart that compares the performance of different tracks.

The resulting chart highlights which academic track performs best overall in terms of average scores.

## 7. Interpretation of Results  

- **Gender** → The bar chart shows performance differences between **male and female students**, highlighting how gender may influence average scores.  

- **Hometown** → Some hometowns have **consistently higher averages**, which may suggest **geographical or environmental factors** that impact performance.  

- **Track** → Certain tracks produce **higher average scores**, which may indicate the effect of **subject specialization** or stronger preparation in those areas.  

## 8. How to Run the Notebook  

1. **Install the required dependencies:**  
   - `pandas` → For handling and analyzing tabular data.  
   - `matplotlib` → For creating visualizations and charts.  
2. Prepare the dataset:
- Place the dataset file board2.csv in the same folder as the Jupyter Notebook.

3. Run the notebook:
- Open the notebook in Jupyter Notebook or JupyterLab.
- Execute all cells by pressing Shift + Enter (or use "Run All").

4. Expected Outputs  

- **DataFrames:**  
  - **Instru** → Students filtered by:  
    - Electronics > 70  
    - Hometown = Luzon  
    - Track = Instrumentation  
  - **Mindy** → Female students from Mindanao with **Average ≥ 55**  

- **Bar Charts:**  
  - By **Gender**  
  - By **Hometown**  
  - By **Track**


## 9. File Outputs  

- **Input:**  
  - `board2.csv` → ECE Board Exam dataset used as the source file.  

- **Output:**  
  - **DataFrame `Instru`** → Students filtered by:  
    - Electronics > 70  
    - Hometown = Luzon  
    - Track = Instrumentation  
  - **DataFrame `Mindy`** → Female students from Mindanao with **Average ≥ 55**.  
  - **Bar Charts** → Visualizations showing performance comparisons by:  
    - **Gender**  
    - **Hometown**  
    - **Track**  
