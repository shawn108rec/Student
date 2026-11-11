import java.io.*;
import java.text.SimpleDateFormat;
import java.util.Date;
import java.util.Random;

public class StudentList {

    private static final String FILE_NAME = "students.txt";

    public static void main(String[] args) {

        // Step 2 and Step 9: Validate arguments
        if (args.length != 1 || args[0].isEmpty()) {
            System.out.println("Invalid arguments!");
            return;
        }

        String command = args[0];

        System.out.println("Loading data ...");

        try {

            if (command.equals("a")) {
                loadAllStudents();
            }

            else if (command.equals("r")) {
                loadRandomStudent();
            }

            else if (command.startsWith("+")) {
                appendStudent(command.substring(1));
            }

            else if (command.startsWith("?")) {
                searchStudent(command.substring(1));
            }

            else if (command.equals("c")) {
                countWords();
            }

            else {
                System.out.println("Invalid arguments!");
            }

        } catch (Exception e) {
            System.out.println("Error: " + e.getMessage());
        }

        System.out.println("Data Loaded.");
    }

    // Step 4: Read all students
    private static String readData() throws IOException {

        BufferedReader reader = new BufferedReader(
                new FileReader(FILE_NAME));

        String data = reader.readLine();
        reader.close();

        return data;
    }

    // Display all students
    private static void loadAllStudents() throws IOException {

        String data = readData();
        String[] students = data.split(",");

        for (String student : students) {
            System.out.println(student.trim());
        }
    }

    // Display a random student
    private static void loadRandomStudent() throws IOException {

        String data = readData();

        System.out.println(data);

        String[] students = data.split(",");

        Random random = new Random();
        int index = random.nextInt(students.length);

        System.out.println(students[index].trim());
    }

    // Append a new student
    private static void appendStudent(String name) throws IOException {

        BufferedWriter writer = new BufferedWriter(
                new FileWriter(FILE_NAME, true));

        Date date = new Date();

        SimpleDateFormat formatter =
                new SimpleDateFormat("yyyy-MM-dd h:mm:ss a");

        String formattedDate = formatter.format(date);

        writer.write(", " + name
                + "\nList last updated on " + formattedDate);

        writer.close();
    }

    // Search for a student
    private static void searchStudent(String name) throws IOException {

        String data = readData();

        String[] students = data.split(",");

        for (String student : students) {

            if (student.trim().equals(name)) {
                System.out.println("We found it!");
                break;
            }
        }
    }

    // Count words using the original assignment's counting logic
    private static void countWords() throws IOException {

        String data = readData();

        int count = 0;
        boolean inWord = false;

        for (char ch : data.toCharArray()) {

            if (ch == ' ') {

                if (!inWord) {
                    count++;
                    inWord = true;
                } else {
                    inWord = false;
                }
            }
        }

        System.out.println(count + " word(s) found");
    }
}
