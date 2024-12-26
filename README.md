# tax-calculator
#this make your tax calculation very easy 
import pandas as pd
import numpy as np

# Define the tax brackets and rates
tax_brackets = pd.DataFrame({
    'Lower Limit': [0, 10000, 30000, 60000, 100000],  # Income limits for each bracket
    'Upper Limit': [9999, 29999, 59999, 99999, np.inf],  # Upper limits, last one is infinity for the top bracket
    'Tax Rate': [0.1, 0.2, 0.3, 0.4, 0.5]  # Tax rates corresponding to each bracket
})

# Function to calculate tax based on income
def calculate_tax(income):
    tax = 0
    for _, row in tax_brackets.iterrows():
        if income > row['Lower Limit']:
            taxable_income = min(income, row['Upper Limit']) - row['Lower Limit']
            tax += taxable_income * row['Tax Rate']
        else:
            break
    return tax

# User Input
def get_user_input():
    try:
        income = float(input("Enter your income:$"))
        if income < 0:
            print("Income cannot be negative.")
            return None
        return income
    except ValueError:
        print("Invalid input. Please enter a valid number.")
        return None

# Main function to run the app
def main():
    income = get_user_input()
    if income is not None:
        tax = calculate_tax(income)
        print(f"\nTax Calculation for an income of ${income:.2f}:")
        print(f"Total Tax: ${tax:.2f}")
    else:
        print("Please restart the app and enter a valid income.")

# Run the app
if __name__ == "__main__":
    main()
