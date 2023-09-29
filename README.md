# University Timetable Repository
#This repository helps university students organize and manage their class timetables. It includes sample timetables, a template for creating your own, and guidelines for usage.

import os
timetables = {}

def display_menu():
    print("\nTimetable Management System")
    print("1. View Timetable")
    print("2. Add Timetable")
    print("3. Delete Timetable")
    print("4. Exit")

def view_timetable():
    print("\nView Timetable")
    for student, timetable in timetables.items():
        print(f"Student: {student}")
        print("Timetable:")
        for day, schedule in timetable.items():
            print(f"  {day}: {schedule}")
        print()

def add_timetable():
    student_name = input("Enter student name: ")
    if student_name in timetables:
        print(f"{student_name}'s timetable already exists.")
        return

    timetable = {}
    days = ["Monday", "Tuesday", "Wednesday", "Thursday", "Friday"]
    for day in days:
        schedule = input(f"Enter {day}'s schedule: ")
        timetable[day] = schedule

    timetables[student_name] = timetable
    print(f"{student_name}'s timetable added successfully.")

def delete_timetable():
    student_name = input("Enter student name to delete timetable: ")
    if student_name in timetables:
        del timetables[student_name]
        print(f"{student_name}'s timetable deleted.")
    else:
        print(f"{student_name}'s timetable not found.")

# Main loop
while True:
    display_menu()
    choice = input("Enter your choice: ")

    if choice == "1":
        view_timetable()
    elif choice == "2":
        add_timetable()
    elif choice == "3":
        delete_timetable()
    elif choice == "4":
        print("Exiting the Timetable Management System.")
        break
    else:
        print("Invalid choice. Please try again.")

# Save the data .
with open("timetable_data.txt", "w") as file:
    for student, timetable in timetables.items():
        file.write(student + "\n")
        for day, schedule in timetable.items():
            file.write(day + ":" + schedule + "\n")
        file.write("\n")

print("Data saved.")
