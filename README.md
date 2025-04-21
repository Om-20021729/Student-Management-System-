# Student-Management-System-
The Student Management System is a simple Python application that helps manage student records using basic file handling and Object-Oriented Programming (OOP). It allows users to add, view, update, and delete student information such as roll number, name, age, and course. The system stores the records in a text file (students.txt) for persistence.

import os

# Class representing a student
class Student:
    def __init__(self, roll_no, name, age, course):
        self.roll_no = roll_no
        self.name = name
        self.age = age
        self.course = course

    def __str__(self):
        # Return student information as a string
        return f"{self.roll_no}, {self.name}, {self.age}, {self.course}"

# Class to manage the student system
class StudentManagementSystem:
    def __init__(self, filename):
        self.filename = filename

    # Create: Add new student to the file
    def create(self, student):
        with open(self.filename, 'a') as file:
            file.write(f"{student.roll_no},{student.name},{student.age},{student.course}\n")
        print("Student record added successfully.")

    # Read: Display all student records
    def read(self):
        if os.path.exists(self.filename):
            with open(self.filename, 'r') as file:
                records = file.readlines()
                if records:
                    for record in records:
                        print(record.strip())
                else:
                    print("No records found.")
        else:
            print("No records found.")

    # Update: Modify a student's record
    def update(self, roll_no, updated_student):
        if os.path.exists(self.filename):
            with open(self.filename, 'r') as file:
                lines = file.readlines()

            found = False
            with open(self.filename, 'w') as file:
                for line in lines:
                    if line.startswith(str(roll_no)):
                        file.write(f"{updated_student.roll_no},{updated_student.name},{updated_student.age},{updated_student.course}\n")
                        found = True
                    else:
                        file.write(line)

            if found:
                print("Student record updated successfully.")
            else:
                print("Student with given roll number not found.")
        else:
            print("No records found.")

    # Delete: Remove a student record
    def delete(self, roll_no):
        if os.path.exists(self.filename):
            with open(self.filename, 'r') as file:
                lines = file.readlines()

            found = False
            with open(self.filename, 'w') as file:
                for line in lines:
                    if not line.startswith(str(roll_no)):
                        file.write(line)
                    else:
                        found = True

            if found:
                print("Student record deleted successfully.")
            else:
                print("Student with given roll number not found.")
        else:
            print("No records found.")

# Main function to interact with the user
def main():
    filename = 'students.txt'
    system = StudentManagementSystem(filename)

    while True:
        print("\nStudent Management System")
        print("1. Add Student")
        print("2. View Students")
        print("3. Update Student")
        print("4. Delete Student")
        print("5. Exit")
        choice = input("Enter your choice: ")

        if choice == '1':
            # Add a student
            roll_no = input("Enter roll number: ")
            name = input("Enter name: ")
            age = input("Enter age: ")
            course = input("Enter course: ")
            student = Student(roll_no, name, age, course)
            system.create(student)

        elif choice == '2':
            # View all students
            print("\nStudent Records:")
            system.read()

        elif choice == '3':
            # Update student record
            roll_no = input("Enter roll number of student to update: ")
            name = input("Enter new name: ")
            age = input("Enter new age: ")
            course = input("Enter new course: ")
            updated_student = Student(roll_no, name, age, course)
            system.update(roll_no, updated_student)

        elif choice == '4':
            # Delete student record
            roll_no = input("Enter roll number of student to delete: ")
            system.delete(roll_no)

        elif choice == '5':
            print("Exiting system.")
            break

        else:
            print("Invalid choice. Please try again.")

# Run the program
if __name__ == '__main__':
    main()
