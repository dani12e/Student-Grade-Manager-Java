import java.io.*;
import java.util.*;
import javax.swing.*;
import java.awt.*;
import java.awt.event.*;

public class Project2 {

    static class GradeManager {
        HashMap<String, Integer> subjects = new HashMap<>();
        HashMap<String, String> subjectGrades = new HashMap<>();
        Map<String, Double> gradePoints = Map.of(
                "A", 5.0, "B", 4.0, "C", 3.0, "D", 2.0, "E", 1.0, "F", 0.0);

        void scoreAllocator(String subject, int score) {
            subjects.put(subject, score);
            subjectGrades.put(subject, getGrade(score));
            System.out.println(subject + ": " + getGrade(score));
        }

        String getGrade(int score) {
            if (score >= 70)
                return "A";
            else if (score >= 60)
                return "B";
            else if (score >= 50)
                return "C";
            else if (score >= 40)
                return "D";
            else if (score >= 30)
                return "E";
            else
                return "F";
        }

        void seeStudentGrades() {
            if (subjects.isEmpty()) {
                System.out.println("No subjects added.");
            } else {
                for (Map.Entry<String, Integer> entry : subjects.entrySet()) {
                    System.out.println(
                            entry.getKey() + ": " + entry.getValue() + " (" + subjectGrades.get(entry.getKey()) + ")");
                }
            }
        }

        void calculateGPA() {
            if (subjectGrades.isEmpty()) {
                System.out.println("No grades to calculate GPA.");
                return;
            }

            double total = 0;
            for (String grade : subjectGrades.values()) {
                total += gradePoints.get(grade);
            }

            double gpa = total / subjectGrades.size();
            System.out.printf("GPA: %.2f%n", gpa);
        }

        void saveToFile() {
            try (BufferedWriter writer = new BufferedWriter(new FileWriter("grades.txt"))) {
                for (Map.Entry<String, Integer> entry : subjects.entrySet()) {
                    writer.write(entry.getKey() + "," + entry.getValue() + "," + subjectGrades.get(entry.getKey()));
                    writer.newLine();
                }
                System.out.println("Grades saved to grades.txt");
            } catch (IOException e) {
                System.out.println("Error saving to file.");
            }
        }

        void loadFromFile() {
            try (BufferedReader reader = new BufferedReader(new FileReader("grades.txt"))) {
                String line;
                subjects.clear();
                subjectGrades.clear();
                while ((line = reader.readLine()) != null) {
                    String[] parts = line.split(",");
                    subjects.put(parts[0], Integer.parseInt(parts[1]));
                    subjectGrades.put(parts[0], parts[2]);
                }
                System.out.println("Grades loaded from grades.txt");
            } catch (IOException e) {
                System.out.println("Error loading file.");
            }
        }
    }

    // 🖼️ GUI Section
    static class GradeManagerGUI {
        GradeManager manager = new GradeManager();

        void display() {
            JFrame frame = new JFrame("Student Grade Manager");
            frame.setSize(400, 300);
            frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
            frame.setLayout(new FlowLayout());

            JTextField subjectField = new JTextField(10);
            JTextField scoreField = new JTextField(5);
            JButton addButton = new JButton("Add Subject");
            JButton gpaButton = new JButton("Calculate GPA");
            JButton saveButton = new JButton("Save");
            JButton loadButton = new JButton("Load");
            JTextArea output = new JTextArea(10, 30);
            output.setEditable(false);

            frame.add(new JLabel("Subject:"));
            frame.add(subjectField);
            frame.add(new JLabel("Score:"));
            frame.add(scoreField);
            frame.add(addButton);
            frame.add(gpaButton);
            frame.add(saveButton);
            frame.add(loadButton);
            frame.add(new JScrollPane(output));

            addButton.addActionListener(e -> {
                String subject = subjectField.getText();
                int score;
                try {
                    score = Integer.parseInt(scoreField.getText());
                    manager.scoreAllocator(subject, score);
                    output.append(subject + " added with score " + score + "\n");
                } catch (NumberFormatException ex) {
                    output.append("Invalid score input.\n");
                }
            });

            gpaButton.addActionListener(e -> {
                manager.calculateGPA();
                output.append("GPA calculated.\n");
            });

            saveButton.addActionListener(e -> {
                manager.saveToFile();
                output.append("Saved to file.\n");
            });

            loadButton.addActionListener(e -> {
                manager.loadFromFile();
                output.append("Loaded from file.\n");
            });

            frame.setVisible(true);
        }
    }

    public static void main(String[] args) {
        java.util.Scanner scanner = new java.util.Scanner(System.in);
        GradeManager manager = new GradeManager();
        System.out.println("1. Console Mode\n2. GUI Mode\nChoose option:");
        int option = scanner.nextInt();
        scanner.nextLine();

        if (option == 1) {
            while (true) {
                System.out.println("\n1. Add Subject\n2. View Grades\n3. Calculate GPA\n4. Save\n5. Load\n6. Exit");
                int choice = scanner.nextInt();
                scanner.nextLine();

                switch (choice) {
                    case 1:
                        System.out.print("Enter subject name: ");
                        String subject = scanner.nextLine();
                        System.out.print("Enter score: ");
                        int score = scanner.nextInt();
                        manager.scoreAllocator(subject, score);
                        break;
                    case 2:
                        manager.seeStudentGrades();
                        break;
                    case 3:
                        manager.calculateGPA();
                        break;
                    case 4:
                        manager.saveToFile();
                        break;
                    case 5:
                        manager.loadFromFile();
                        break;
                    case 6:
                        System.out.println("Exiting...");
                        return;
                }
            }
        } else {
            new GradeManagerGUI().display();
        }
    }
}
