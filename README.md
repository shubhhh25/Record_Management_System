# Record_Management_System

Mini Project Report
Console Record-Management Application
Student Record Management System (Python)
Submitted by: Shubham Eknath Sukhadare
Roll No --52
Submitted as part of MCA coursework
Language: Python 3 
1. Introduction & Objective
This project is a console-based Student Record Management System built in Python. It allows a user to Add, View, Search, Update, Delete, and Export student records through a simple, menu-driven text interface. All records are saved permanently to a JSON file, so data is not lost when the program is closed and reopened.
The objective of this mini project is to demonstrate the practical use of core Python programming concepts within a single, working application: data types and variables, conditional statements, loops, functions, exception handling, file I/O, and menu-driven program design.
2. How the Project Meets the Assignment Requirements
Requirement	How it is Implemented
Data types & variables	int for age, str for ID/name/course/email/phone; dict for one record
Conditional statements	if / elif / else used for menu routing and field validation
Loops	while True drives the main menu; for loops search and display records
Functions	One dedicated function per feature (add_record, view_records, search_record, etc.)
Exception handling	try/except around age input, menu choice input, and all file read/write operations
File I/O	json.load() / json.dump() read and write students.json
Menu-driven design	Numbered menu inside a while loop routes to the correct function each time
3. Project Theme & Data Structure
Theme: Student Record Management System — a realistic and simple theme suitable for an MCA-level assignment.
Each student record contains:
•	Student ID (text) — unique identifier for each student
•	Name (text)
•	Age (whole number)
•	Course (text)
•	Email (text)
•	Phone Number (text — not a number, since no arithmetic is ever done on it)
Data structure used: a list of dictionaries
Each individual student record is stored as a Python dictionary (key–value pairs), which makes each field self-describing, e.g. student["name"]. All student dictionaries are kept inside one Python list. This structure maps directly onto JSON, so the entire list can be saved to and loaded from students.json with very little code.
4. Tools & Technologies Used
Tool / Library	Purpose
Python 3	Core programming language
json (standard library)	Save and load records permanently in students.json
os (standard library)	Check whether students.json already exists
openpyxl (external library)	Export records into a real, formatted Excel (.xlsx) report
5. Program Architecture / Flow
•	Program starts → tries to load existing records from students.json (if the file is missing or corrupted, it safely starts with an empty list)
•	Main menu is displayed in a while loop
•	User enters a choice (1–7)
•	The matching function runs (Add / View / Search / Update / Delete / Export)
•	Any change to the data is immediately saved back to students.json
•	The loop repeats until the user selects Exit (7)
6. Menu Options
#	Option	Description
1	Add Record	Add a new student, with duplicate-ID and empty-field checks
2	View Records	Display every stored student record
3	Search Record	Look up one student by Student ID
4	Update Record	Edit an existing student's details (blank = keep old value)
5	Delete Record	Remove a student record, with a yes/no confirmation
6	Export Records to Excel	Save all records into a formatted students_report.xlsx file
7	Exit	Close the program
7. Step-by-Step Working (with Console Screenshots)
The following screenshots were captured from an actual run of the program, showing each of the 7 menu options in action.
Step 1 — Main Menu
When the program starts, it loads existing records (if any) and displays the main menu. The user picks an option by typing its number.
 
Figure 1: Program startup and main menu
Step 2 — Add Record
The user is prompted field-by-field for the new student's details. Empty fields and duplicate Student IDs are rejected automatically.
 
Figure 2: Adding a new student record
Step 3 — View Records
All stored records are displayed as neatly formatted cards, one per student.
 
Figure 3: Viewing all student records
Step 4 — Search Record
The user enters a Student ID, and the matching record (if found) is displayed.
 
Figure 4: Searching for a student by ID
Step 5 — Update Record
The user selects a Student ID to edit. Leaving a field blank keeps its existing value, so only the fields that need changing are retyped.
 
Figure 5: Updating a student's age
Step 6 — Delete Record
The matching record is shown first, then the user must confirm with 'y' before it is permanently removed.
 
Figure 6: Deleting a student record with confirmation
Step 7 — Export Records to Excel
All current records are written into a real, formatted Excel file (students_report.xlsx) using the openpyxl library.
 
Figure 7: Exporting records to an Excel file
8. Exception Handling Summary
Situation	How it's Handled
Non-numeric age entered	try/except ValueError re-asks until a valid number is given
Invalid menu choice (text or out-of-range)	try/except ValueError plus if/elif/else range check
students.json missing	os.path.exists() check — program starts with an empty list, no crash
students.json corrupted / invalid JSON	except json.JSONDecodeError — warns and starts fresh
File cannot be read/written	except IOError around file operations
Searching/updating/deleting a non-existent ID	find_student_by_id() returns None, handled with a clear message
Duplicate Student ID on Add	Checked before insertion; add is rejected with an error message
9. Sample Test Cases
Test Case	Input	Expected Result
Add valid record	Valid details	Record added
Duplicate ID	Existing ID	Error message shown
Invalid age	"abc"	Program asks again
Search existing ID	Existing ID	Record displayed
Search invalid ID	Non-existing ID	"Not found" message
Update record	Existing ID	Record updated
Delete record	Existing ID + "y"	Record deleted
Missing students.json	No file present	Program starts with 0 records, no crash
Export to Excel	Choice 6	students_report.xlsx created
Exit	Choice 7	Program closes cleanly
10. Conclusion
This mini project successfully implements a menu-driven Student Record Management System that satisfies every requirement of the assignment. It demonstrates practical use of Python data types, conditionals, loops, functions, exception handling, and file I/O within one cohesive, beginner-friendly application. Records persist across program runs using JSON storage, and an additional Excel export feature makes the data easy to share and present.
