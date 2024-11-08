# Student Management System in C++

This project is a simple Student Management System implemented in C++. It allows you to perform basic operations on a list of students, including adding, deleting, searching, updating, sorting, and displaying student records.

## Features
- **Insert Student**: Add a new student with ID, name, age, and GPA.
- **Delete Student**: Remove a student by their ID.
- **Search Student**: Find a student by their ID and display their details.
- **Update Student**: Modify the details of an existing student by their ID.
- **Sort Students**: Sort the list of students by ID.
- **Display All Students**: View all student records in the system.

## Code

```cpp
#include <iostream>
#include <string>
using namespace std;

const int MAX_STUDENTS = 100;

struct Student {
    int id;
    string name;
    int age;
    float gpa;
};

int currentStudentCount = 0;
Student students[MAX_STUDENTS];

// Function to add a student
void insertStudent(int id, string name, int age, float gpa) {
    if (currentStudentCount >= MAX_STUDENTS) {
        cout << "Student list is full.\n";
        return;
    }
    students[currentStudentCount] = {id, name, age, gpa};
    currentStudentCount++;
    cout << "Student added successfully.\n";
}

// Function to delete a student by ID
void deleteStudent(int id) {
    bool found = false;
    for (int i = 0; i < currentStudentCount; i++) {
        if (students[i].id == id) {
            found = true;
            for (int j = i; j < currentStudentCount - 1; j++) {
                students[j] = students[j + 1];
            }
            currentStudentCount--;
            cout << "Student deleted successfully.\n";
            break;
        }
    }
    if (!found) {
        cout << "Student not found.\n";
    }
}

// Function to search a student by ID
void searchStudent(int id) {
    for (int i = 0; i < currentStudentCount; i++) {
        if (students[i].id == id) {
            cout << "Student found: " << students[i].name << ", Age: " << students[i].age << ", GPA: " << students[i].gpa << endl;
            return;
        }
    }
    cout << "Student not found.\n";
}

// Function to update a student's details by ID
void updateStudent(int id, string name, int age, float gpa) {
    for (int i = 0; i < currentStudentCount; i++) {
        if (students[i].id == id) {
            students[i].name = name;
            students[i].age = age;
            students[i].gpa = gpa;
            cout << "Student updated successfully.\n";
            return;
        }
    }
    cout << "Student not found.\n";
}

// Function to sort students by ID
void sortStudents() {
    for (int i = 0; i < currentStudentCount - 1; i++) {
        for (int j = i + 1; j < currentStudentCount; j++) {
            if (students[i].id > students[j].id) {
                swap(students[i], students[j]);
            }
        }
    }
    cout << "Students sorted by ID.\n";
}

// Function to display all students
void displayStudents() {
    if (currentStudentCount == 0) {
        cout << "No students to display.\n";
        return;
    }
    for (int i = 0; i < currentStudentCount; i++) {
        cout << "ID: " << students[i].id << ", Name: " << students[i].name << ", Age: " << students[i].age << ", GPA: " << students[i].gpa << endl;
    }
}

int main() {
    int choice, id, age;
    float gpa;
    string name;

    while (true) {
        cout << "\nStudent Management System\n";
        cout << "1. Insert Student\n2. Delete Student\n3. Search Student\n4. Update Student\n5. Sort Students\n6. Display All Students\n7. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice;

        switch (choice) {
            case 1:
                cout << "Enter ID, Name, Age, GPA: ";
                cin >> id >> ws;
                getline(cin, name);
                cin >> age >> gpa;
                insertStudent(id, name, age, gpa);
                break;
            case 2:
                cout << "Enter ID to delete: ";
                cin >> id;
                deleteStudent(id);
                break;
            case 3:
                cout << "Enter ID to search: ";
                cin >> id;
                searchStudent(id);
                break;
            case 4:
                cout << "Enter ID to update: ";
                cin >> id >> ws;
                cout << "Enter new Name, Age, GPA: ";
                getline(cin, name);
                cin >> age >> gpa;
                updateStudent(id, name, age, gpa);
                break;
            case 5:
                sortStudents();
                break;
            case 6:
                displayStudents();
                break;
            case 7:
                return 0;
            default:
                cout << "Invalid choice.\n";
        }
    }
}
