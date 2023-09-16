import json

# Initialize budget data
budget_data = {
    "income": 0,
    "expenses": []
}

# File to store data
data_file = "budget_data.json"

# Load existing data if available
try:
    with open(data_file, "r") as file:
        budget_data = json.load(file)
except FileNotFoundError:
    pass

def save_data():
    # Save data to the file
    with open(data_file, "w") as file:
        json.dump(budget_data, file)

def show_menu():
    print("\n===== Personal Budget Tracker =====")
    print("1. Enter Income")
    print("2. Enter Expense")
    print("3. Calculate Budget")
    print("4. Expense Analysis")
    print("5. Exit")

def enter_income():
    income = float(input("Enter your income: $"))
    budget_data["income"] = income
    save_data()
    print(f"Income of ${income} added successfully!")

def enter_expense():
    category = input("Enter expense category: ")
    amount = float(input(f"Enter expense amount for {category}: $"))
    budget_data["expenses"].append({"category": category, "amount": amount})
    save_data()
    print(f"Expense of ${amount} for {category} added successfully!")

def calculate_budget():
    total_income = budget_data["income"]
    total_expenses = sum(expense["amount"] for expense in budget_data["expenses"])
    remaining_budget = total_income - total_expenses
    print(f"Total Income: ${total_income}")
    print(f"Total Expenses: ${total_expenses}")
    print(f"Remaining Budget: ${remaining_budget}")

def expense_analysis():
    expense_categories = set(expense["category"] for expense in budget_data["expenses"])
    print("\nExpense Analysis:")
    for category in expense_categories:
        category_total = sum(expense["amount"] for expense in budget_data["expenses"] if expense["category"] == category)
        print(f"{category}: ${category_total}")

# Main loop
while True:
    show_menu()
    choice = input("Enter your choice: ")
    
    if choice == "1":
        enter_income()
    elif choice == "2":
        enter_expense()
    elif choice == "3":
        calculate_budget()
    elif choice == "4":
        expense_analysis()
    elif choice == "5":
        print("Exiting the budget tracker. Goodbye!")
        break
    else:
        print("Invalid choice. Please try again.")
