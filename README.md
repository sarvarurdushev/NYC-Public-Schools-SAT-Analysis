# NYC-Public-Schools-SAT-Analysis
This project analyzes New York City public school SAT performance using a dataset of schools. The SAT has three sections — Math, Reading, and Writing, each with a maximum score of 800 points. These tests play a pivotal role in college admissions, making school-level performance analysis valuable for students, parents, researchers, and policymakers.

# 📂 Dataset

The dataset provided is ```schools.csv```, which includes:

**school_name** → Name of the school

**borough** → NYC borough where the school is located

**average_math** → Average Math SAT score

**average_reading** → Average Reading SAT score

**average_writing** → Average Writing SAT score

# 🛠️ Project Workflow
**1. Importing Data**
```import pandas as pd```

# Read in the data
```schools = pd.read_csv("schools.csv")```

# Preview the data
```schools.head()```

**2. Best Schools for Math**

We look at schools with average math scores above 640 and sort them in descending order.
```
best_math_schools = schools[schools["average_math"] >= 640][["school_name", "average_math"]].sort_values("average_math", ascending=False)
```
**3. Top 10 Performing Schools Overall**

We calculate the total SAT score (Math + Reading + Writing) and find the top 10 schools.

# Calculate total_SAT per school
```
schools["total_SAT"] = schools["average_math"] + schools["average_reading"] + schools["average_writing"]
```
# Who are the top 10 performing schools?
```
top_10_schools = schools.sort_values("total_SAT", ascending=False)[["school_name", "total_SAT"]].head(10)
```
**4. Borough with Highest Score Variation**

We check which NYC borough has the highest standard deviation in SAT performance.

# Group by borough
```
boroughs = schools.groupby("borough")["total_SAT"].agg(["count", "mean", "std"]).round(2)
```
# Borough with largest variation
```
largest_std_dev = boroughs[boroughs["std"] == boroughs["std"].max()]
```
# Rename for clarity
```
largest_std_dev = largest_std_dev.rename(columns={"count": "num_schools", "mean": "average_SAT", "std": "std_SAT"})
```
# Move borough back to column
```
largest_std_dev.reset_index(inplace=True)
```
# 📊 Key Insights

Some schools excel in Math SATs with averages above 640.

The Top 10 schools by overall SAT score significantly outperform others.

The borough with the highest standard deviation indicates the greatest disparity in school performance.

# 🚀 Technologies Used

Python 3

Pandas for data manipulation
```
git clone https://github.com/yourusername/nyc-schools-sat-analysis.git
cd nyc-schools-sat-analysis
```

**Install dependencies:**
```
pip install pandas
```

**Run the script:**
```
python analysis.py
```

✨ This project highlights data-driven insights into NYC public school SAT performance to better understand educational outcomes across boroughs.
