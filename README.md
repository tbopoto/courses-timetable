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
# Added functions to save and load timetable data to/from a text file.

def save_timetables(filename):
    with open(filename, "w") as file:
        for student, timetable in timetables.items():
            file.write(student + "\n")
            for day, schedule in timetable.items():
                file.write(day + ":" + schedule + "\n")
            file.write("\n")

def load_timetables(filename):
    global timetables
    timetables = {}
    try:
        with open(filename, "r") as file:
            lines = file.readlines()
            student = None
            timetable = {}
            for line in lines:
                line = line.strip()
                if not line:
                    if student:
                        timetables[student] = timetable
                    student = None
                    timetable = {}
                else:
                    if ":" in line:
                        day, schedule = line.split(":", 1)
                        timetable[day] = schedule
                    else:
                        student = line
    except FileNotFoundError:
        pass

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
        
# Updated the main program to load existing data at startup and save data on program exit.
if __name__ == "__main__":
    load_timetables("timetable_data.txt")  # Load existing data at startup
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
            save_timetables("timetable_data.txt")  # Save data on program exit
            print("Exiting the Timetable Management System.")
            break
        else:
            print("Invalid choice. Please try again.")

# Save the data.
with open("timetable_data.txt", "w") as file:
    for student, timetable in timetables.items():
        file.write(student + "\n")
        for day, schedule in timetable.items():
            file.write(day + ":" + schedule + "\n")
        file.write("\n")

print("Data saved.")
