Student Record Management System

A simple console-based mini project in Python for managing student records — built to demonstrate core programming concepts: data types, conditionals, loops, functions, exception handling, file I/O, data structures, and a menu-driven design.

Submitted By
Shubham Eknath Sukhadare
Soham Choudhari — Roll No. 52

Course: Master of Computer Applications (MCA) Subject: Python Programming — Mini Project

Features
Add a new student record (with duplicate ID check)
View all student records
Search for a student by ID
Update an existing student's details
Delete a student record
Data is saved permanently to a JSON file, so records persist across runs
Requirements
Python 3.x (no external libraries needed — only built-in json and os modules)
How to Run
Make sure student_records.py is in a folder you can write to (the program creates a students.json file next to it).
Open a terminal in that folder and run:
bash
   python student_records.py
Follow the on-screen menu:
   ===== Student Record Management System =====
   1. Add Student Record
   2. View All Records
   3. Search Record
   4. Update Record
   5. Delete Record
   6. Exit
Enter the number of the action you want, then follow the prompts.
Data Storage

All records are stored in students.json, created automatically in the same folder the first time you add a record. Example:

json
{
    "101": {
        "name": "Aarav Sharma",
        "course": "MCA",
        "marks": 88.5
    }
}
The outer key is the Student ID.
Each value is a dictionary holding name, course, and marks.
The file is safely reloaded on every run — if it doesn't exist yet, the program just starts with an empty record set instead of crashing.
Project Structure
student_records.py   → main program (all logic)
students.json         → auto-created data file (holds saved records)
Code Overview
Function	Purpose
load_data()	Reads records from students.json into a dictionary; returns an empty dictionary if the file doesn't exist or is corrupted
save_data()	Writes the current records dictionary back to students.json
add_record()	Adds a new student, after checking the ID isn't already used and the marks are a valid number
view_records()	Displays all records in a formatted table
search_record()	Looks up and displays one student by ID
update_record()	Edits an existing student's name, course, and/or marks
delete_record()	Removes a student record, with a y/n confirmation
show_menu()	Prints the menu options
main()	Runs the menu loop and dispatches to the right function based on user choice
Error Handling
Entering non-numeric text for Marks is caught and reported without crashing the program.
An empty or corrupted students.json file is handled gracefully — the program starts fresh instead of failing.
Attempting to add a duplicate Student ID is blocked with a clear error message.
Attempting to search, update, or delete a Student ID that doesn't exist is reported instead of causing an error.
