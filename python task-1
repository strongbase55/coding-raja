import tkinter as tk
from tkinter import messagebox
from datetime import datetime
import json
import os  # Import the os module

# Define the file path to store tasks
TASKS_FILE = "tasks.json"

# Initialize an empty task list
tasks = []


# Function to add a task
def add_task():
    description = task_entry.get()
    priority = priority_var.get()
    due_date = due_date_entry.get()

    try:
        due_date = datetime.strptime(due_date, "%Y-%m-%d").date()
        task = {
            "description": description,
            "priority": priority,
            "due_date": due_date.strftime("%Y-%m-%d"),
            "completed": False,
        }
        tasks.append(task)
        save_tasks()
        task_listbox.insert(tk.END, f"{description} - Priority: {priority} - Due Date: {due_date.strftime('%Y-%m-%d')}")
        task_entry.delete(0, tk.END)
        due_date_entry.delete(0, tk.END)
    except ValueError:
        messagebox.showwarning("Warning", "Invalid date format. Please use YYYY-MM-DD.")

# Function to remove a task
def remove_task():
    try:
        selected_index = task_listbox.curselection()[0]
        task_listbox.delete(selected_index)
        del tasks[selected_index]
        save_tasks()
    except IndexError:
        messagebox.showwarning("Warning", "Please select a task to remove.")

# Function to mark a task as completed
def mark_task_completed():
    try:
        selected_index = task_listbox.curselection()[0]
        tasks[selected_index]["completed"] = True
        task_listbox.itemconfig(selected_index, {"fg": "gray"})
        save_tasks()
    except IndexError:
        messagebox.showwarning("Warning", "Please select a task to mark as completed.")

# Function to list tasks
def list_tasks():
    task_listbox.delete(0, tk.END)
    for task in tasks:
        status = "Completed" if task["completed"] else "Not Completed"
        task_listbox.insert(tk.END, f"{task['description']} - Priority: {task['priority']} - Due Date: {task['due_date']} - Status: {status}")

# Function to save tasks to the file
def save_tasks():
    with open(TASKS_FILE, "w") as file:
        json.dump(tasks, file, indent=4)

# Create the main window
root = tk.Tk()
root.title("To-Do List Application")
root.geometry("600x400")  # Set the window size

# Set the background color
root.configure(bg="lightblue")

# Create task entry widget
task_entry = tk.Entry(root, width=40)
task_entry.pack(pady=10)

# Create priority dropdown
priority_var = tk.StringVar()
priority_var.set("medium")  # Default priority
priority_dropdown = tk.OptionMenu(root, priority_var, "high", "medium", "low")
priority_dropdown.pack()

# Create due date entry widget
due_date_label = tk.Label(root, text="Due Date (YYYY-MM-DD):", bg="lightblue")
due_date_label.pack()
due_date_entry = tk.Entry(root, width=20)
due_date_entry.pack()

# Create add button with a blue background
add_button = tk.Button(root, text="Add Task", command=add_task, bg="blue", fg="white")
add_button.pack()

# Create task listbox
task_listbox = tk.Listbox(root, width=60)
task_listbox.pack()

# Create remove button with a red background
remove_button = tk.Button(root, text="Remove Task", command=remove_task, bg="red", fg="white")
remove_button.pack()

# Create mark as completed button with a green background
mark_completed_button = tk.Button(root, text="Mark as Completed", command=mark_task_completed, bg="green", fg="white")
mark_completed_button.pack()

# Create list tasks button
list_tasks_button = tk.Button(root, text="List Tasks", command=list_tasks, bg="purple", fg="white")
list_tasks_button.pack()

# Load tasks from the file (if it exists)
if os.path.exists(TASKS_FILE):
    with open(TASKS_FILE, "r") as file:
        tasks = json.load(file)
        list_tasks()

# Start the main loop
root.mainloop()
