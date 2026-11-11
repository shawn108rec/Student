# Student
Student information

import java.io.*;
import java.text.*;
import java.util.*;

public class StudentList {

    public static void main(String[] args) {

        // Check arguments
        if (args.length == 0) {
            System.out.println("Please provide an argument.");
            return;
        }

        String command = args[0];

        if (command.equals("a")) {

            System.out.println("Loading data ...");

            try {
                BufferedReader s = new BufferedReader(
                    new FileReader("students.txt"));

                String r = s.readLine();
                s.close();

                if (r != null) {
                    String i[] = r.split(",");

                    for (String j : i) {
                        System.out.println(j.trim());
                    }
                }

            } catch (Exception e) {
                System.out.println(e.getMessage());
            }

            System.out.println("Data Loaded.");
        }

        else if (command.equals("r")) {

            System.out.println("Loading data ...");

            try {
                BufferedReader s = new BufferedReader(
                    new FileReader("students.txt"));

                String r = s.readLine();
                s.close();

                String i[] = r.split(",");

                Random x = new Random();
                int y = x.nextInt(i.length);

                System.out.println("Random Student: " + i[y].trim());

            } catch (Exception e) {
                System.out.println(e.getMessage());
            }

            System.out.println("Data Loaded.");
        }

        else if (command.startsWith("+")) {

            System.out.println("Loading data ...");

            try {
                String name = command.substring(1);

                BufferedReader br = new BufferedReader(
                    new FileReader("students.txt"));

                String r = br.readLine();
                br.close();

                if (r == null) r = "";

                if (!r.isEmpty()) {
                    r += ", ";
                }

                r += name;

                Date d = new Date();

                String df = "dd/MM/yyyy-hh:mm:ss a";
                DateFormat dateFormat = new SimpleDateFormat(df);

                String fd = dateFormat.format(d);

                BufferedWriter s = new BufferedWriter(
                    new FileWriter("students.txt"));

                s.write(r);
                s.newLine();
                s.write("List last updated on " + fd);

                s.close();

            } catch (Exception e) {
                System.out.println(e.getMessage());
            }

            System.out.println("Data Loaded.");
        }

        else if (command.startsWith("?")) {

            System.out.println("Loading data ...");

            try {
                BufferedReader s = new BufferedReader(
                    new FileReader("students.txt"));

                String r = s.readLine();
                s.close();

                String i[] = r.split(",");
                String t = command.substring(1).trim();

                boolean done = false;

                for (int idx = 0; idx < i.length; idx++) {

                    if (i[idx].trim().equals(t)) {
                        System.out.println("We found it!");
                        done = true;
                        break;
                    }
                }

                if (!done) {
                    System.out.println("Student not found!");
                }

            } catch (Exception e) {
                System.out.println(e.getMessage());
            }

            System.out.println("Data Loaded.");
        }

        else if (command.equals("c")) {

            System.out.println("Loading data ...");

            try {
                BufferedReader s = new BufferedReader(
                    new FileReader("students.txt"));

                String D = s.readLine();
                s.close();

                if (D != null && !D.trim().isEmpty()) {

                    String words[] = D.trim().split("\\s+");

                    System.out.println(
                        words.length + " word(s) found "
                        + D.length());
                }

            } catch (Exception e) {
                System.out.println(e.getMessage());
            }

            System.out.println("Data Loaded.");
        }

        else {
            System.out.println("Invalid command!");
        }
    }
}

