Student Record Management System

A menu-driven console application built in Python for managing student records — Add, View, Search, Update, Delete, and Export, with data saved permanently between runs.

Author: Shubham Eknath Sukhadare
Roll No : 53
Course: MCA — Mini Project (Console Record-Management Application)

Features
Add Record — add a new student with duplicate-ID and empty-field checks
View Records — display every stored student record
Search Record — look up a single student by Student ID
Update Record — edit an existing student's details (leave a field blank to keep its current value)
Delete Record — remove a record, with a yes/n confirmation prompt
Export Records to Excel — save all records into a formatted students_report.xlsx file
Persistent storage — records are saved to students.json and automatically reloaded the next time the program runs
Input validation & exception handling — invalid ages, invalid menu choices, missing/corrupted files, and non-existent IDs are all handled gracefully
Requirements
Python 3.7 or later
openpyxl (only needed for the Excel export feature)

Install the one external dependency with:

bash
pip install openpyxl

(Everything else — json, os — comes built into Python.)

How to Run
Make sure student_record_manager.py is in a folder by itself (or alongside students.json if you already have one).
Open a terminal in that folder.
Run:
bash
   python student_record_manager.py

(Use python3 instead of python if that's what your system requires.)

Use the on-screen menu to manage records:
   1. Add Record
   2. View Records
   3. Search Record
   4. Update Record
   5. Delete Record
   6. Export Records to Excel
   7. Exit

To run it again later, just repeat step 3 — your previously saved records will load automatically from students.json.

Data Storage

Each student record is stored as a dictionary with these fields:

Field	Type	Notes
id	str	Unique Student ID
name	str	Student's full name
age	int	Whole number, 1–100
course	str	Course name
email	str	Email address
phone	str	Stored as text (not used in math)

All records together are stored as a list of dictionaries, saved to students.json in this format:

json
[
    {
        "id": "101",
        "name": "Riya Sharma",
        "age": 22,
        "course": "MCA",
        "email": "riya@example.com",
        "phone": "9876543210"
    }
]
Files
File	Purpose
student_record_manager.py	Main program
students.json	Auto-created — permanent storage for all records
students_report.xlsx	Auto-created — generated when you use the Excel export option
Notes
If students.json doesn't exist yet, the program starts with zero records instead of crashing.
If students.json is corrupted or contains invalid data, the program warns you and starts fresh rather than failing.
The Excel export (option 6) requires openpyxl. If it isn't installed, the program shows a clear message instead of crashing.
