class StudentDatabase:
    student_list = []

    @classmethod
    def add_student(self, student):
       self.student_list.append(student)

    @classmethod
    def get_student_id(self, student_id):
        for student in self.student_list:
            if student.student_id == student_id:
                return student
        return None

    @classmethod
    def view_all_students(self):
        if not self.student_list:
            print("No students in the database.")
        for student in self.student_list:
            student.view_student_info()

class Student:
    def __init__(self, student_id, name, department, is_enrolled=False):
        self.student_id = student_id
        self.name = name
        self.department = department
        self.is_enrolled = is_enrolled
        StudentDatabase.add_student(self)


    def enroll_student(self):
        if self.is_enrolled:
            print(f"Student {self.student_id} is already enrolled.")
        else:
            self.is_enrolled = True
            print(f"Student {self.student_id} has been enrolled.")


    def drop_student(self):
        if not self.is_enrolled:
            print(f"Student {self.student_id} is not currently enrolled.")
        else:
            self.is_enrolled = False
            print(f"Student {self.student_id} has been dropped.")
           

    def view_student_info(self):
        enrolled="true" if self.is_enrolled else "false"
        print(f"ID: {self.student_id}, Name: {self.name}, "
              f"Department: {self.department}, Enrolled: {enrolled}")


Student("S101", "Alice Smith", "Computer Science", True)
Student("S102", "Bob Johnson", "Mathematics")
Student("S103", "Charlie Lee", "Physics", True)


def menu():
    while True:
        print("\n--- Student Management Menu---")
        print("1. View All Students")
        print("2. Enroll Student")
        print("3. Drop Student")
        print("4. Exit")

        choice = input("Enter your choice (1-4): ")

        if choice == '1':
            StudentDatabase.view_all_students()

        elif choice == '2':
            student_id = input("Enter student ID to enroll: ")
            student = StudentDatabase.get_student_id(student_id)
            if student:
                student.enroll_student()
            else:
                print("Invalid student ID.")

        elif choice == '3':
            student_id = input("Enter student ID to drop: ")
            student = StudentDatabase.get_student_id(student_id)
            if student:
                student.drop_student()
            else:
                print("Invalid student ID.")

        elif choice == '4':
            print("Exiting the system.")
            break
        else:
            print("Invalid choice. Please enter a number between 1 and 4.")

menu()
