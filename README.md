import json
import os

FILE_NAME = "tasks.json"

def load_tasks():
    if not os.path.exists(FILE_NAME):
        return []
    with open(FILE_NAME, "r") as f:
        return json.load(f)

def save_tasks(tasks):
    with open(FILE_NAME, "w") as f:
        json.dump(tasks, f, indent=4)

def show_tasks(tasks):
    if not tasks:
        print("\nNo tasks found.\n")
        return
    print("\nYour Tasks:")
    for i, task in enumerate(tasks, start=1):
        status = "✔" if task["done"] else "✘"
        print(f"{i}. [{status}] {task['title']}")
    print()

def add_task(tasks):
    title = input("Enter task: ")
    tasks.append({"title": title, "done": False})
    save_tasks(tasks)
    print("Task added!\n")

def complete_task(tasks):
    show_tasks(tasks)
    try:
        num = int(input("Enter task number to mark complete: "))
        tasks[num-1]["done"] = True
        save_tasks(tasks)
        print("Task completed!\n")
    except:
        print("Invalid task number.\n")

def delete_task(tasks):
    show_tasks(tasks)
    try:
        num = int(input("Enter task number to delete: "))
        removed = tasks.pop(num-1)
        save_tasks(tasks)
        print(f"Deleted task: {removed['title']}\n")
    except:
        print("Invalid task number.\n")

def main():
    tasks = load_tasks()

    while True:
        print("1. Show tasks")
        print("2. Add task")
        print("3. Complete task")
        print("4. Delete task")
        print("5. Exit")

        choice = input("Choose an option: ")

        if choice == "1":
            show_tasks(tasks)
        elif choice == "2":
            add_task(tasks)
        elif choice == "3":
            complete_task(tasks)
        elif choice == "4":
            delete_task(tasks)
        elif choice == "5":
            break
        else:
            print("Invalid choice.\n")

if __name__ == "__main__":
    main()
