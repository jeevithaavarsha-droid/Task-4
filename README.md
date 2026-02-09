# -------------------------------------------------
# Task 04: Analyze and Visualize Social Media Patterns
# Dataset: Students Social Media Addiction
# -------------------------------------------------

# Import libraries
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Load dataset
data = pd.read_csv(r"D:\Students Social Media Addiction.csv")

# Display basic info
print("Dataset Preview:")
print(data.head())

print("\nDataset Info:")
print(data.info())

# -------------------------------------------------
# Numerical Analysis
# -------------------------------------------------

numeric_cols = [
    'Age',
    'Avg_Daily_Usage_Hours',
    'Sleep_Hours_Per_Night',
    'Mental_Health_Score',
    'Conflicts_Over_Social_Media',
    'Addicted_Score'
]

# Histograms for numeric features
for col in numeric_cols:
    plt.figure(figsize=(7,4))
    sns.histplot(data[col], kde=True)
    plt.title(f"Distribution of {col}")
    plt.xlabel(col)
    plt.ylabel("Count")
    plt.show()

# -------------------------------------------------
# Categorical Analysis
# -------------------------------------------------

categorical_cols = [
    'Gender',
    'Academic_Level',
    'Most_Used_Platform',
    'Affects_Academic_Performance',
    'Relationship_Status'
]

for col in categorical_cols:
    plt.figure(figsize=(7,4))
    sns.countplot(y=data[col])
    plt.title(f"{col} Distribution")
    plt.xlabel("Count")
    plt.ylabel(col)
    plt.show()

# -------------------------------------------------
# Correlation Analysis
# -------------------------------------------------

plt.figure(figsize=(10,6))
sns.heatmap(data[numeric_cols].corr(), annot=True, cmap='coolwarm')
plt.title("Correlation Heatmap")
plt.show()

# -------------------------------------------------
# Relationship Analysis
# -------------------------------------------------

# Usage vs Addiction
plt.figure(figsize=(7,5))
sns.scatterplot(
    x='Avg_Daily_Usage_Hours',
    y='Addicted_Score',
    hue='Gender',
    data=data
)
plt.title("Daily Usage vs Addiction Score")
plt.show()

# Sleep vs Mental Health
plt.figure(figsize=(7,5))
sns.scatterplot(
    x='Sleep_Hours_Per_Night',
    y='Mental_Health_Score',
    hue='Academic_Level',
    data=data
)
plt.title("Sleep Hours vs Mental Health Score")
plt.show()
