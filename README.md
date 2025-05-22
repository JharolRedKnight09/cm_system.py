# cm_system.py
import sys

class CMSystem:
    def __init__(self):
        self.students = {}
        self.payments = {}
        self.grades = {}
        self.teachers = {}
        self.courses = {}

    def register_student(self):
        student_id = input("ID del alumno: ").strip()
        name = input("Nombre completo: ").strip()
        if student_id in self.students:
            print("Alumno ya registrado.")
            return
        self.students[student_id] = name
        print(f"Alumno {name} registrado correctamente.")

    def record_payment(self):
        student_id = input("ID del alumno: ").strip()
        if student_id not in self.students:
            print("Alumno no encontrado.")
            return
        amount = input("Monto a pagar: ").strip()
        try:
            amount = float(amount)
        except ValueError:
            print("Monto inválido.")
            return
        self.payments.setdefault(student_id, 0)
        self.payments[student_id] += amount
        print(f"Pago registrado: {amount} para {self.students[student_id]}.")

    def record_grade(self):
        student_id = input("ID del alumno: ").strip()
        if student_id not in self.students:
            print("Alumno no encontrado.")
            return
        course = input("Curso: ").strip()
        try:
            grade = float(input("Calificación (0-100): ").strip())
            if grade < 0 or grade > 100:
                print("Calificación fuera de rango.")
                return
        except ValueError:
            print("Calificación inválida.")
            return
        self.grades.setdefault(student_id, {})
        self.grades[student_id][course] = grade
        print(f"Calificación registrada para {self.students[student_id]} en {course}.")

    def register_teacher(self):
        teacher_id = input("ID del docente: ").strip()
        name = input("Nombre completo: ").strip()
        if teacher_id in self.teachers:
            print("Docente ya registrado.")
            return
        self.teachers[teacher_id] = name
        print(f"Docente {name} registrado correctamente.")

    def assign_course(self):
        course = input("Nombre del curso: ").strip()
        teacher_id = input("ID del docente: ").strip()
        if teacher_id not in self.teachers:
            print("Docente no encontrado.")
            return
        self.courses[course] = teacher_id
        print(f"Curso {course} asignado a {self.teachers[teacher_id]}.")

    def show_menu(self):
        print("\n=== CM System Menu ===")
        print("1. Registrar alumno")
        print("2. Registrar pago")
        print("3. Registrar calificación")
        print("4. Registrar docente")
        print("5. Asignar curso a docente")
        print("6. Salir")

    def run(self):
        while True:
            self.show_menu()
            option = input("Seleccione una opción: ").strip()
            if option == "1":
                self.register_student()
            elif option == "2":
                self.record_payment()
            elif option == "3":
                self.record_grade()
            elif option == "4":
                self.register_teacher()
            elif option == "5":
                self.assign_course()
            elif option == "6":
                print("Saliendo del sistema...")
                sys.exit()
            else:
                print("Opción inválida. Intente de nuevo.")

if __name__ == "__main__":
    system = CMSystem()
    system.run()
