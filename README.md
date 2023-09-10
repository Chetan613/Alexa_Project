# Alexa_Project



class Task:
    def __init__(self, task_name, date, completed=False):
        self.task_name = task_name
        self.date = date
        self.completed = completed

class TaskManager:
    def __init__(self):
        self.tasks = []

    def add_task(self, task_name, date):
        task = Task(task_name, date)
        self.tasks.append(task)

    def update_task(self, task_name, date, completed):
        for task in self.tasks:
            if task.task_name == task_name and task.date == date:
                task.completed = completed
                return True
        return False

    def view_percentage_completed(self, date):
        completed_tasks = sum(1 for task in self.tasks if task.date == date and task.completed)
        total_tasks = sum(1 for task in self.tasks if task.date == date)
        if total_tasks == 0:
            return 0.0
        return (completed_tasks / total_tasks) * 100

    def delete_task(self, task_name, date):
        self.tasks = [task for task in self.tasks if not (task.task_name == task_name and task.date == date)]

# Sample usage:
task_manager = TaskManager()

while True:
    print("Options:")
    print("1. Add Task")
    print("2. Update Task Completion Status")
    print("3. View Percentage Completed for a Date")
    print("4. Delete Task")
    print("5. Exit")

    choice = input("Enter your choice: ")

    if choice == "1":
        task_name = input("Enter task name: ")
        date = input("Enter date (YYYY-MM-DD): ")
        task_manager.add_task(task_name, date)
        print("Task added!")

    elif choice == "2":
        task_name = input("Enter task name: ")
        date = input("Enter date (YYYY-MM-DD): ")
        completed = input("Is the task completed? (yes/no): ").lower()
        completed = True if completed == "yes" else False
        if task_manager.update_task(task_name, date, completed):
            print("Task updated!")
        else:
            print("Task not found!")

    elif choice == "3":
        date = input("Enter date (YYYY-MM-DD): ")
        percentage = task_manager.view_percentage_completed(date)
        print(f"Percentage of tasks completed on {date}: {percentage}%")

    elif choice == "4":
        task_name = input("Enter task name: ")
        date = input("Enter date (YYYY-MM-DD): ")
        task_manager.delete_task(task_name, date)
        print("Task deleted!")

    elif choice == "5":
        break

