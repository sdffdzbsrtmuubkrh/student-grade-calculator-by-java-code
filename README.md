import java.util.ArrayList;
import java.util.Scanner;

class Student {
    private String name;
    private ArrayList<Double> grades;

    public Student(String name) {
        this.name = name;
        this.grades = new ArrayList<>();
    }

    public void addGrade(double grade) {
        grades.add(grade);
    }

    public String getName() {
        return name;
    }

    public ArrayList<Double> getGrades() {
        return grades;
    }

    public double calculateAverage() {
        double sum = 0;
        for (double grade : grades) {
            sum += grade;
        }
        return grades.size() > 0 ? sum / grades.size() : 0;
    }
}

public class StudentGradeManager {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        ArrayList<Student> students = new ArrayList<>();

        while (true) {
            System.out.print("Enter student name (or 'exit' to finish): ");
            String name = scanner.nextLine();
            if (name.equalsIgnoreCase("exit")) {
                break;
            }

            Student student = new Student(name);

            while (true) {
                System.out.print("Enter grade for " + name + " (or -1 to finish): ");
                double grade = scanner.nextDouble();
                scanner.nextLine();  // Consume newline

                if (grade == -1) {
                    break;
                }

                if (grade < 0 || grade > 100) {
                    System.out.println("Grade must be between 0 and 100.");
                } else {
                    student.addGrade(grade);
                }
            }

            students.add(student);
        }

        System.out.println("\nStudent Grades:");
        for (Student student : students) {
            System.out.printf("Name: %s, Average Grade: %.2f%n", student.getName(), student.calculateAverage());
        }

        scanner.close();
    }
}
