
import csv
import os
from datetime import datetime

FILE_NAME = "expenses.csv"


def add_expense():
    print("\n--- Add New Expense ---")

    category = input("Enter category: ").strip()
    if not category:
        print("Category cannot be empty.")
        return

    try:
        amount = float(input("Enter amount (RM): "))
        if amount <= 0:
            print("Amount must be greater than zero.")
            return
    except ValueError:
        print("Please enter a valid number.")
        return

    description = input("Enter description: ").strip()
    date = datetime.now().strftime("%Y-%m-%d")

    file_exists = os.path.exists(FILE_NAME)

    with open(FILE_NAME, "a", newline="", encoding="utf-8") as file:
        writer = csv.writer(file)

        if not file_exists or os.path.getsize(FILE_NAME) == 0:
            writer.writerow(["Date", "Category", "Amount", "Description"])

        writer.writerow([date, category, amount, description])

    print("Expense added successfully!")


def view_expenses():
    print("\n--- All Expenses ---")

    if not os.path.exists(FILE_NAME):
        print("No expenses recorded yet.")
        return

    with open(FILE_NAME, "r", newline="", encoding="utf-8") as file:
        reader = csv.DictReader(file)
        expenses = list(reader)

    if not expenses:
        print("No expenses recorded yet.")
        return

    for expense in expenses:
        print(
            f"{expense['Date']} | "
            f"{expense['Category']} | "
            f"RM{float(expense['Amount']):.2f} | "
            f"{expense['Description']}"
        )


def show_summary():
    print("\n--- Expense Summary ---")

    if not os.path.exists(FILE_NAME):
        print("No expenses recorded yet.")
        return

    totals = {}
    grand_total = 0

    with open(FILE_NAME, "r", newline="", encoding="utf-8") as file:
        reader = csv.DictReader(file)

        for expense in reader:
            category = expense["Category"]
            amount = float(expense["Amount"])

            totals[category] = totals.get(category, 0) + amount
            grand_total += amount

    if not totals:
        print("No expenses recorded yet.")
        return

    for category, total in totals.items():
        print(f"{category}: RM{total:.2f}")

    print("-----------------------")
    print(f"Total Expenses: RM{grand_total:.2f}")


def main():
    while True:
        print("\n==========================")
        print("     EXPENSE TRACKER")
        print("==========================")
        print("1. Add Expense")
        print("2. View All Expenses")
        print("3. Show Expense Summary")
        print("4. Exit")

        choice = input("Choose an option (1-4): ")

        if choice == "1":
            add_expense()
        elif choice == "2":
            view_expenses()
        elif choice == "3":
            show_summary()
        elif choice == "4":
            print("Thank you for using Expense Tracker!")
            break
        else:
            print("Invalid option. Please try again.")


if __name__ == "__main__":
    main()
