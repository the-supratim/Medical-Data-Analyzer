# Medical Data Visualizer

This is the boilerplate for the Medical Data Visualizer project. Instructions for building your project can be found at https://www.freecodecamp.org/learn/data-analysis-with-python/data-analysis-with-python-projects/medical-data-visualizer

### Project Description: Medical Data Analyzer

The Medical Data Analyzer project involves analyzing medical data from a dataset containing patient information. You will create a function to read the dataset, perform various calculations to derive insights, and return these insights in a structured format.

### Objectives

1. **Read the dataset**: Load the dataset from a CSV file into a pandas DataFrame.
2. **Calculate various medical statistics**: Compute specific metrics based on the dataset.
3. **Return results in a dictionary**: Output the results in a structured format.

### Dataset

The dataset contains medical information about patients with columns such as age, sex, BMI, number of children, smoker status, and insurance charges.

### Function Specifications

1. **Input**: Path to the CSV file.
2. **Output**: A dictionary containing the following keys and their corresponding calculated values:
   - `'average_age'`: Average age of patients.
   - `'male_count'`: Count of male patients.
   - `'female_count'`: Count of female patients.
   - `'average_bmi'`: Average BMI of patients.
   - `'smokers_count'`: Count of smokers.
   - `'non_smokers_count'`: Count of non-smokers.
   - `'average_charges_smokers'`: Average insurance charges for smokers.
   - `'average_charges_non_smokers'`: Average insurance charges for non-smokers.
   - `'average_charges_by_age_group'`: Average insurance charges by age group (e.g., <30, 30-60, >60).
   - `'bmi_category_counts'`: Count of patients in different BMI categories (e.g., underweight, normal weight, overweight, obese).

### Steps to Follow

1. **Load the Data**:
   - Use pandas to read the CSV file into a DataFrame.

2. **Calculate Medical Statistics**:
   - **Average Age**: Calculate the mean age of patients.
   - **Count of Males and Females**: Use the `value_counts()` method to count the number of males and females in the dataset.
   - **Average BMI**: Calculate the mean BMI of patients.
   - **Count of Smokers and Non-Smokers**: Use the `value_counts()` method to count the number of smokers and non-smokers in the dataset.
   - **Average Insurance Charges for Smokers**: Calculate the mean insurance charges for smokers.
   - **Average Insurance Charges for Non-Smokers**: Calculate the mean insurance charges for non-smokers.
   - **Average Insurance Charges by Age Group**: Categorize patients into age groups and calculate the mean insurance charges for each group.
   - **BMI Category Counts**: Categorize patients into BMI categories and count the number of patients in each category.

3. **Return the Results**:
   - Store each calculated value in a dictionary and return it.

### Example Implementation

```python
import pandas as pd

def calculate_medical_data_statistics(file_path, print_data=True):
    # Read data from file
    df = pd.read_csv(file_path)
    
    # Average age of patients
    average_age = df['age'].mean()

    # Count of males and females
    gender_counts = df['sex'].value_counts()
    male_count = gender_counts.get('male', 0)
    female_count = gender_counts.get('female', 0)

    # Average BMI of patients
    average_bmi = df['bmi'].mean()

    # Count of smokers and non-smokers
    smoker_counts = df['smoker'].value_counts()
    smokers_count = smoker_counts.get('yes', 0)
    non_smokers_count = smoker_counts.get('no', 0)

    # Average insurance charges for smokers and non-smokers
    average_charges_smokers = df[df['smoker'] == 'yes']['charges'].mean()
    average_charges_non_smokers = df[df['smoker'] == 'no']['charges'].mean()

    # Average insurance charges by age group
    age_groups = pd.cut(df['age'], bins=[0, 30, 60, 100], labels=['<30', '30-60', '>60'])
    average_charges_by_age_group = df.groupby(age_groups)['charges'].mean().to_dict()

    # BMI category counts
    bmi_categories = pd.cut(df['bmi'], bins=[0, 18.5, 24.9, 29.9, float('inf')], labels=['underweight', 'normal weight', 'overweight', 'obese'])
    bmi_category_counts = df['bmi'].groupby(bmi_categories).count().to_dict()

    if print_data:
        print("Average age of patients:", average_age)
        print("Number of male patients:", male_count)
        print("Number of female patients:", female_count)
        print("Average BMI of patients:", average_bmi)
        print("Number of smokers:", smokers_count)
        print("Number of non-smokers:", non_smokers_count)
        print("Average insurance charges for smokers:", average_charges_smokers)
        print("Average insurance charges for non-smokers:", average_charges_non_smokers)
        print("Average insurance charges by age group:", average_charges_by_age_group)
        print("BMI category counts:", bmi_category_counts)

    return {
        'average_age': average_age,
        'male_count': male_count,
        'female_count': female_count,
        'average_bmi': average_bmi,
        'smokers_count': smokers_count,
        'non_smokers_count': non_smokers_count,
        'average_charges_smokers': average_charges_smokers,
        'average_charges_non_smokers': average_charges_non_smokers,
        'average_charges_by_age_group': average_charges_by_age_group,
        'bmi_category_counts': bmi_category_counts
    }

# Example usage:
result = calculate_medical_data_statistics('medical_data.csv', print_data=True)
```

### Expected Output

The expected output will be a dictionary with the calculated values, and if `print_data` is set to `True`, the calculated metrics will be printed to the console.

This project provides practice with data analysis using pandas, including filtering, grouping, and calculating various statistics based on conditions. It also helps in understanding and manipulating medical data to derive meaningful insights.
