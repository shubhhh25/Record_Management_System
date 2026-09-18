Readme · MD
🎓 Student Record Management System

A menu-driven console application built in Python that lets you Add, View, Search, Update, Delete, and Export student records — with all data saved permanently to disk between runs.

This project was built as an MCA mini project to demonstrate core Python concepts (data types, conditionals, loops, functions, exception handling, and file I/O) inside one cohesive, working application.

Author: Shubham Eknath Sukhadare 
Roll No:53
Course: MCA — Mini Project (Console Record-Management Application) Language: Python 3

Table of Contents
Overview
Features
Requirements
Installation
How to Run
Menu Options
Project Structure
Data Model
How It Works (Architecture)
Function Reference
Validation Rules
Exception Handling
Sample Usage
Testing Checklist
Known Limitations
Possible Future Improvements
Concepts Demonstrated
Overview

Think of this application as a digital notebook for a college's student records. Instead of writing entries on paper, the program stores structured records (one per student) and lets you manage them through a simple numbered menu — no GUI, no database, no internet connection required.

Every change you make (adding, updating, or deleting a record) is immediately saved to a file called students.json, so your data is still there the next time you run the program.

Features
➕ Add Record — add a new student, with duplicate-ID and empty-field checks
📋 View Records — display every stored student record as a readable card
🔍 Search Record — look up a single student by Student ID
✏️ Update Record — edit an existing student's details; leave a field blank to keep its current value
🗑️ Delete Record — remove a record, with a yes/no confirmation prompt before deleting
📊 Export Records to Excel — save all records into a nicely formatted students_report.xlsx file
💾 Persistent storage — records survive closing and reopening the program (stored in students.json)
🛡️ Input validation & exception handling — invalid ages, invalid menu choices, empty fields, missing/corrupted files, and non-existent IDs are all handled gracefully instead of crashing
🎨 Colorized console output — success, warning, and error messages are color-coded for readability
Requirements
Python 3.7+
openpyxl — only required for the "Export to Excel" feature

Everything else (json, os) is part of Python's standard library — no other installation needed.

Installation
Download/copy student_record_manager.py into its own folder.
Install the one external dependency:
bash
   pip install openpyxl

If you skip this step, every feature still works — only the Excel export option will show a friendly message asking you to install openpyxl.

How to Run

Open a terminal in the folder containing student_record_manager.py and run:

bash
python student_record_manager.py

(Use python3 instead of python if your system requires it.)

To run it again later — even after restarting your computer — just repeat the same command from the same folder. The program automatically reloads all previously saved records from students.json on startup.

Menu Options
╔══════════════════════════════════════════════════╗
║        STUDENT RECORD MANAGEMENT SYSTEM           ║
╚══════════════════════════════════════════════════╝

  1. Add Record
  2. View Records
  3. Search Record
  4. Update Record
  5. Delete Record
  6. Export Records to Excel
  7. Exit
#	Option	What it does
1	Add Record	Prompts for ID, Name, Age, Course, Email, Phone; rejects empty fields and duplicate IDs
2	View Records	Lists every saved student, one card per record
3	Search Record	Finds and displays one student by their ID
4	Update Record	Lets you edit any field of an existing student; blank input = keep old value
5	Delete Record	Removes a student after you confirm with y
6	Export Records to Excel	Writes all records into students_report.xlsx
7	Exit	Closes the program
Project Structure
project-folder/
│
├── student_record_manager.py   # Main program (all source code)
├── students.json                # Auto-created — permanent record storage
└── students_report.xlsx         # Auto-created — only after using "Export to Excel"
Data Model

Each student record is a Python dictionary:

Field	Type	Notes
id	str	Unique Student ID — duplicates are rejected
name	str	Student's full name
age	int	Whole number between 1 and 100
course	str	Course name (e.g. "MCA")
email	str	Email address
phone	str	Stored as text, not a number — no arithmetic is ever done on it

All student dictionaries together are stored in a list, which is the exact structure written to and read from students.json:

json
[
    {
        "id": "101",
        "name": "Riya Sharma",
        "age": 22,
        "course": "MCA",
        "email": "riya@example.com",
        "phone": "9876543210"
    },
    {
        "id": "102",
        "name": "Aman Verma",
        "age": 23,
        "course": "MCA",
        "email": "aman@example.com",
        "phone": "9123456780"
    }
]

Why a list of dictionaries? A dictionary lets every field be accessed by name (student["name"]) instead of a fragile numeric position (student[1]), and this structure maps directly onto JSON — meaning the whole list can be saved and loaded with almost no conversion code.

How It Works (Architecture)
Program starts
      │
      ▼
Load students.json into memory
(if missing/corrupted → start with an empty list, no crash)
      │
      ▼
┌───────────────────────────┐
│   Show main menu (loop)    │◄────────────────┐
└─────────────┬──────────────┘                  │
              ▼                                  │
      User enters a choice (1-7)                 │
              ▼                                  │
   Call the matching function                    │
   (add_record / view_records / ... )            │
              ▼                                  │
   Function updates the in-memory list            │
   and saves it back to students.json             │
              │                                  │
              └──────────────────────────────────┘
                     (loop repeats until Exit)
Function Reference
Function	Purpose
load_records()	Reads students.json into a list at startup; handles a missing or corrupted file
save_records(students)	Writes the current list of records back to students.json
get_non_empty_input(prompt)	Re-asks until the user enters non-blank text
get_valid_age()	Re-asks until the user enters a valid whole number (1–100) for age
find_student_by_id(students, id)	Searches the list and returns the matching record, or None
print_student_card(student)	Displays one student's details in a readable, bordered format
add_record(students)	Collects new student details and appends them to the list
view_records(students)	Displays every record currently stored
search_record(students)	Finds and displays one student by ID
update_record(students)	Edits an existing student's fields (blank = unchanged)
delete_record(students)	Removes a student after confirmation
export_to_excel(students)	Writes all records into a formatted .xlsx file using openpyxl
show_menu()	Prints the numbered menu
main()	Runs the overall program loop, tying everything together
Validation Rules
Student ID, Name, Course, Email, and Phone cannot be left empty
Age must be a whole number between 1 and 100
Duplicate Student IDs are not allowed when adding a new record
Update and Delete only work if the entered Student ID already exists
Exception Handling
Situation	How it's handled
Non-numeric age entered	try/except ValueError — re-asks until valid
Invalid menu choice (letters or out-of-range number)	try/except ValueError + if/elif/else range check
students.json doesn't exist	Checked with os.path.exists() — starts with an empty list
students.json is corrupted/invalid	except json.JSONDecodeError — warns and starts fresh
File can't be read or written	except IOError around file operations
Searching/updating/deleting a non-existent ID	find_student_by_id() returns None, handled with a clear message
Duplicate Student ID on Add	Checked before insertion; the add is rejected with an error message
openpyxl not installed	Checked before export; shows an install instruction instead of crashing

No broad, unqualified except: blocks are used anywhere — every except targets a specific, expected error type.

Sample Usage
Enter your choice (1-7): 1

ADD NEW STUDENT
Enter Student ID: 101
Enter Name: Riya Sharma
Enter Age: 22
Enter Course: MCA
Enter Email: riya@example.com
Enter Phone Number: 9876543210
✔ Student 'Riya Sharma' added successfully!
Enter your choice (1-7): 3

SEARCH STUDENT
Enter Student ID to search: 101
✔ Student found!
────────────────────────────────────────────
 ID     : 101
 Name   : Riya Sharma
 Age    : 22
 Course : MCA
 Email  : riya@example.com
 Phone  : 9876543210
────────────────────────────────────────────
Testing Checklist
Test Case	Input	Expected Result
Add valid record	Valid details	Record added
Duplicate ID	Existing ID	Error message shown
Invalid age	"abc"	Program asks again
Search existing ID	Existing ID	Record displayed
Search invalid ID	Non-existing ID	"Not found" message
Update record	Existing ID	Record updated
Delete record	Existing ID + y	Record deleted
Missing students.json	No file present	Program starts with 0 records, no crash
Corrupted students.json	Invalid JSON content	Program warns and starts fresh
Export to Excel	Choice 6	students_report.xlsx created
Exit	Choice 7	Program closes cleanly
Known Limitations
Single-user, local file storage only — not designed for multiple people editing at the same time
No authentication/login — anyone running the program can see and edit all records
Age is limited to 1–100; no support for other age formats (e.g. months for infants)
Email and phone number formats are not validated beyond "not empty" (e.g. it won't reject "abc" as an email)
Possible Future Improvements
Add regex-based validation for email format and phone number length
Add a "Sort Records" option (by name, age, or ID)
Add CSV import/export in addition to Excel
Add a search that matches partial names, not just exact ID
Concepts Demonstrated
Python Concept	Where it appears
Data types & variables	int for age, str for ID/name/course/email/phone
Conditional statements	if/elif/else for menu routing and validation
Loops	while True for the menu; for loops to search/display records
Functions	One dedicated function per feature
Exception handling	try/except around user input and all file operations
File I/O	json.load() / json.dump() for students.json
Data structures	List of dictionaries for all records
Menu-driven design	Numbered menu inside a while loop

This README documents student_record_manager.py — see the file itself for the full source code and inline comments.
