import tkinter as tk
from tkinter import messagebox, ttk

root = tk.Tk()
root.title("Student Management System")
root.geometry("600x400")

student_data = []
name_var = tk.StringVar()
age_var = tk.StringVar()
grade_var = tk.StringVar()

def add_student():
    name = name_var.get()
    age = age_var.get()
    grade = grade_var.get()
    
    if name and age and grade:
        student_data.append({"Name": name, "Age": age, "Grade": grade})
        refresh_table()
        clear_inputs()
        messagebox.showinfo("Success", "Student added successfully!")
    else:
        messagebox.showerror("Error", "Please fill out all fields.")

def delete_student():
    selected_item = student_table.selection()
    if selected_item:
        index = student_table.index(selected_item)
        student_data.pop(index)
        refresh_table()
        messagebox.showinfo("Success", "Student deleted successfully!")
    else:
        messagebox.showerror("Error", "Please select a student to delete.")

def refresh_table():
    for row in student_table.get_children():
        student_table.delete(row)
    for student in student_data:
        student_table.insert("", "end", values=(student["Name"], student["Age"], student["Grade"]))

def clear_inputs():
    name_var.set("")
    age_var.set("")
    grade_var.set("")

title_label = tk.Label(root, text="Student Management System", font=("Arial", 18), bg="dark turquoise")
title_label.pack(pady=10, fill="x")

form_frame = tk.Frame(root)
form_frame.pack(pady=10)

tk.Label(form_frame, text="Name: ").grid(row=0, column=0)
tk.Entry(form_frame, textvariable=name_var).grid(row=0, column=1)

tk.Label(form_frame, text="Age: ").grid(row=1, column=0)
tk.Entry(form_frame, textvariable=age_var).grid(row=1, column=1)

tk.Label(form_frame, text="Grade: ").grid(row=2, column=0)
tk.Entry(form_frame, textvariable=grade_var).grid(row=2, column=1)

button_frame = tk.Frame(root)
button_frame.pack(pady=10)

tk.Button(button_frame, text="Add Student", command=add_student, bg="forest green", fg="black").pack(side="left", padx=5)
tk.Button(button_frame, text="Delete Student", command=delete_student, bg="red2", fg="black").pack(side="left", padx=5)

table_frame = tk.Frame(root)
table_frame.pack(pady=10)

student_table = ttk.Treeview(table_frame, columns=("Name", "Age", "Grade"), show="headings")
student_table.heading("Name", text="Name")
student_table.heading("Age", text="Age")
student_table.heading("Grade", text="Grade")
student_table.pack()

root.mainloop()
