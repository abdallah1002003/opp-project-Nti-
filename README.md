# opp-project-Nti-
opp project withe python 
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age


class Student(Person):
    def __init__(self, name, age):
        super().__init__(name, age)
        self.scores = {}


class Teacher(Person):
    def __init__(self, name, age, salary=0):
        super().__init__(name, age)
        self.salary = salary


class TeacherManager:
    def __init__(self):
        self.students = []
        self.teachers = []

    def add_student(self):
        name = input("Student name: ")
        age = int(input("Age: "))
        subjects = input("Subjects (comma separated): ").split(",")
        student = Student(name, age)
        for subject in subjects:
            student.scores[subject.strip()] = []
        self.students.append(student)
        print("Student added!")

    def add_teacher(self):
        name = input("Teacher name: ")
        age = int(input("Age: "))
        salary = float(input("Salary: ") or 0)
        teacher = Teacher(name, age, salary)
        self.teachers.append(teacher)
        print("Teacher added!")

    def record_score(self):
        name = input("Student name: ")
        student = self.find_student(name)
        if not student:
            print("Student not found.")
            return
        subject = input("Subject: ")
        if subject not in student.scores:
            print("Subject not found for this student.")
            return
        scores = input("Enter scores (comma separated): ").split(",")
        student.scores[subject].extend(float(s.strip()) for s in scores)
        print("Scores recorded!")

    def show_student_report(self):
        name = input("Student name: ")
        student = self.find_student(name)
        if not student:
            print("Student not found.")
            return
        for subject, scores in student.scores.items():
            if scores:
                avg = sum(scores) / len(scores)
                status = "Passed" if avg >= 50 else "Failed"
                print(f"{subject}: {scores} | Avg: {avg:.2f} | {status}")
            else:
                print(f"{subject}: No scores yet.")

    def list_all_students(self):
        for s in self.students:
            print(f"{s.name}, Age: {s.age}, Subjects: {list(s.scores.keys())}")

    def list_all_teachers(self):
        for t in self.teachers:
            print(f"{t.name}, Age: {t.age}, Salary: {t.salary}")

    def find_student(self, name):
        for s in self.students:
            if s.name.lower() == name.lower():
                return s
        return None

    def run(self):
        while True:
            print("\n1. Add Student\n2. Add Teacher\n3. Record Score\n4. Show Student Report\n5. List Students\n6. List Teachers\n7. Exit")
            choice = input("Choose: ")
            if choice == "1":
                self.add_student()
            elif choice == "2":
                self.add_teacher()
            elif choice == "3":
                self.record_score()
            elif choice == "4":
                self.show_student_report()
            elif choice == "5":
                self.list_all_students()
            elif choice == "6":
                self.list_all_teachers()
            elif choice == "7":
                print("Goodbye!")
                break
            else:
                print("Invalid choice, try again.")


if __name__ == "__main__":
    manager = TeacherManager()
    manager.run()
