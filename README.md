# -Serialization-and-Deserialization-of-a-Student-Object
To implement Java serialization to save a Student object to a file and later retrieve it through deserialization
import java.io.*;

class Student implements Serializable {
    private static final long serialVersionUID = 1L;
    String studentID;
    String name;
    double grade;

    Student(String studentID, String name, double grade) {
        this.studentID = studentID;
        this.name = name;
        this.grade = grade;
    }
}

public class StudentSerialization {
    public static void main(String[] args) throws IOException, ClassNotFoundException {
        Student student = new Student("S101", "Vishesh", 9.5);

        FileOutputStream fileOut = new FileOutputStream("student.ser");
        ObjectOutputStream out = new ObjectOutputStream(fileOut);
        out.writeObject(student);
        out.close();
        fileOut.close();

        FileInputStream fileIn = new FileInputStream("student.ser");
        ObjectInputStream in = new ObjectInputStream(fileIn);
        Student deserializedStudent = (Student) in.readObject();
        in.close();
        fileIn.close();

        System.out.println("Student ID: " + deserializedStudent.studentID);
        System.out.println("Name: " + deserializedStudent.name);
        System.out.println("Grade: " + deserializedStudent.grade);
    }
}
