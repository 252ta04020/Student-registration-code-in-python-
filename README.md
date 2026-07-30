class Student:
    def __init__(self, student_id, name, age, course):
        self.student_id = student_id
        self.name = name
        self.age = age
        self.course = course

    def display_details(self):
        print(f"| {self.student_id:<10} | {self.name:<20} | {self.age:<5} | {self.course:<15} |")


class RegistrationSystem:
    def __init__(self):
        self.students = {}

    def register_student(self):
        print("\n--- Register New Student ---")
        
        # Validate Student ID
        while True:
            student_id = input("Enter 4-Digit Student ID (e.g., 1001): ").strip()
            if not student_id.isdigit() or len(student_id) != 4:
                print("❌ Error: ID must be exactly a 4-digit number. Try again.")
                continue
            if student_id in self.students:
                print("❌ Error: This Student ID already exists. Try another.")
                continue
            break

        # Validate Name
        while True:
            name = input("Enter Student Full Name: ").strip()
            if not name.replace(" ", "").isalpha() or len(name) < 2:
                print("❌ Error: Name must contain letters only (min 2 characters).")
                continue
            break

        # Validate Age
        while True:
            try:
                age = int(input("Enter Age (15 - 100): "))
                if age < 15 or age > 100:
                    print("❌ Error: Age must be between 15 and 100.")
                    continue
                break
            except ValueError:
                print("❌ Error: Invalid input! Please enter a valid number for age.")

        # Validate Course
        while True:
            course = input("Enter Course Name (e.g., Computer Science): ").strip()
            if len(course) < 2:
                print("❌ Error: Course field cannot be empty.")
                continue
            break

        # Add validated data to the database dictionary
        new_student = Student(student_id, name, age, course)
        self.students[student_id] = new_student
        print(f"\n✅ Success: {name} has been registered successfully!")

    def display_all_students(self):
        print("\n--- Registered Students List ---")
        if not self.students:
            print("No students registered yet.")
            return

        print("-" * 63)
        print(f"| {'ID':<10} | {'Name':<20} | {'Age':<5} | {'Course':<15} |")
        print("-" * 63)
        for student in self.students.values():
            student.display_details()
        print("-" * 63)


def main():
    system = RegistrationSystem()
    
    while True:
        print("\n===== STUDENT REGISTRATION SYSTEM =====")
        print("1. Register a Student")
        print("2. Display All Registered Students")
        print("3. Exit System")
        
        choice = input("Select an option (1-3): ").strip()
        
        if choice == '1':
            system.register_student()
        elif choice == '2':
            system.display_all_students()
        elif choice == '3':
            print("\nExiting system. Goodbye!")
            break
        else:
            print("❌ Invalid Option! Please choose 1, 2, or 3.")

if __name__ == "__main__":
    main()
    
