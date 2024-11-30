# Global Data
users = {"admin": "password123"}  # Default admin credentials
students = {}  # Stores student records


def main():
    print("\n=== Welcome to the Student Management System ===")
    while True:
        print("\n1. Login as Admin")
        print("2. Exit")
        choice = input("Enter your choice: ")

        if choice == "1":
            if admin_login():
                admin_panel()
        elif choice == "2":
            print("Goodbye!")
            break
        else:
            print("Invalid choice. Please try again.")


# Admin Login
def admin_login():
    username = input("Enter admin username: ")
    password = input("Enter admin password: ")
    if username in users and users[username] == password:
        print("\nLogin successful!")
        return True
    else:
        print("\nInvalid credentials.")
        return False


# Admin Panel
def admin_panel():
    while True:
        print("\n--- Admin Panel ---")
        print("1. Manage Student Records")
        print("2. Manage Attendance")
        print("3. Manage Grades")
        print("4. View Reports")
        print("5. Logout")

        choice = input("Enter your choice: ")

        if choice == "1":
            manage_students()
        elif choice == "2":
            manage_attendance()
        elif choice == "3":
            manage_grades()
        elif choice == "4":
            view_reports()
        elif choice == "5":
            print("Logging out...")
            break
        else:
            print("Invalid choice. Please try again.")


# Manage Students
def manage_students():
    while True:
        print("\n--- Manage Students ---")
        print("1. Add Student")
        print("2. View Students")
        print("3. Update Student")
        print("4. Delete Student")
        print("5. Back")

        choice = input("Enter your choice: ")

        if choice == "1":
            add_student()
        elif choice == "2":
            view_students()
        elif choice == "3":
            update_student()
        elif choice == "4":
            delete_student()
        elif choice == "5":
            break
        else:
            print("Invalid choice. Please try again.")


def add_student():
    student_id = input("Enter student ID: ")
    if student_id in students:
        print("Student already exists!")
        return

    name = input("Enter student name: ")
    grade = input("Enter grade: ")
    students[student_id] = {"name": name, "grade": grade, "attendance": [], "marks": {}}
    print("Student added successfully!")


def view_students():
    if not students:
        print("No students available.")
        return

    for student_id, details in students.items():
        print(f"ID: {student_id}, Name: {details['name']}, Grade: {details['grade']}")


def update_student():
    student_id = input("Enter student ID to update: ")
    if student_id not in students:
        print("Student not found!")
        return

    name = input("Enter new name: ")
    grade = input("Enter new grade: ")
    students[student_id]["name"] = name
    students[student_id]["grade"] = grade
    print("Student updated successfully!")


def delete_student():
    student_id = input("Enter student ID to delete: ")
    if student_id not in students:
        print("Student not found!")
        return

    del students[student_id]
    print("Student deleted successfully!")


# Manage Attendance
def manage_attendance():
    student_id = input("Enter student ID: ")
    if student_id not in students:
        print("Student not found!")
        return

    date = input("Enter date (YYYY-MM-DD): ")
    status = input("Enter attendance (P/A): ").upper()
    students[student_id]["attendance"].append({"date": date, "status": status})
    print("Attendance recorded!")


# Manage Grades
def manage_grades():
    student_id = input("Enter student ID: ")
    if student_id not in students:
        print("Student not found!")
        return

    subject = input("Enter subject: ")
    marks = input("Enter marks: ")
    students[student_id]["marks"][subject] = marks
    print("Grade recorded!")


# View Reports
def view_reports():
    print("\n--- Reports ---")
    print("1. Attendance Report")
    print("2. Grade Report")
    choice = input("Enter your choice: ")

    if choice == "1":
        attendance_report()
    elif choice == "2":
        grade_report()
    else:
        print("Invalid choice. Please try again.")


def attendance_report():
    for student_id, details in students.items():
        print(f"\nAttendance for {details['name']} (ID: {student_id}):")
        if not details["attendance"]:
            print("  No attendance records.")
        else:
            for record in details["attendance"]:
                print(f"  Date: {record['date']}, Status: {record['status']}")


def grade_report():
    for student_id, details in students.items():
        print(f"\nGrades for {details['name']} (ID: {student_id}):")
        if not details["marks"]:
            print("  No grades recorded.")
        else:
            for subject, marks in details["marks"].items():
                print(f"  Subject: {subject}, Marks: {marks}")


# Run the Program
if __name__ == "__main__":
    main()

