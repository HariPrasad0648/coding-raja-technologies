import json
import os
from datetime import datetime

# Initialize an empty task list
tasks = []

# Load tasks from a JSON file if it exists
def load_tasks():
    global tasks
    if os.path.exists("tasks.json"):
        with open("tasks.json", "r") as file:
            tasks = json.load(file)

# Save tasks to a JSON file
def save_tasks():
    with open("tasks.json", "w") as file:
        json.dump(tasks, file)

# Add a new task to the list
def add_task():
    task_name = input("Enter task name: ")
    priority = input("Enter task priority (high/medium/low): ")
    due_date = input("Enter due date (YYYY-MM-DD): ")

    task = {
        "name": task_name,
        "priority": priority,
        "due_date": due_date,
        "completed": False,
    }

    tasks.append(task)
    print("Task added successfully.")

# Remove a task from the list by task name
def remove_task():
    task_name = input("Enter the name of the task to remove: ")
    for task in tasks:
        if task["name"] == task_name:
            tasks.remove(task)
            print("Task removed successfully.")
            return
    print("Task not found.")

# Mark a task as completed by task name
def mark_task_completed():
    task_name = input("Enter the name of the task to mark as completed: ")
    for task in tasks:
        if task["name"] == task_name:
            task["completed"] = True
            print("Task marked as completed.")
            return
    print("Task not found.")

# Display the list of tasks with details
def list_tasks():
    for index, task in enumerate(tasks, start=1):
        print(f"{index}. Name: {task['name']}")
        print(f"   Priority: {task['priority']}")
        print(f"   Due Date: {task['due_date']}")
        print(f"   Completed: {'Yes' if task['completed'] else 'No'}")
        print()

# Main loop
def main():
    load_tasks()
    while True:
        print("\nTo-Do List Application")
        print("1. Add Task")
        print("2. Remove Task")
        print("3. Mark Task as Completed")
        print("4. List Tasks")
        print("5. Quit")
        choice = input("Enter your choice: ")

        if choice == "1":
            add_task()
        elif choice == "2":
            remove_task()
        elif choice == "3":
            mark_task_completed()
        elif choice == "4":
            list_tasks()
        elif choice == "5":
            save_tasks()
            print("Goodbye!")
            break
        else:
            print("Invalid choice. Please try again.")

if __name__ == "__main__":
    main()
