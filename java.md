## 1. Write a Java program to check if two strings are anagrams (contain the same characters in different orders).
- **Definition** : An anagram is a word or phrase formed by rearranging the letters of another word or phrase, typically using all the original letters exactly once.
```java
import java.util.Arrays;
import java.util.Scanner;

class AnagramCheck {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.print("Enter the first string: ");
        String str1 = sc.nextLine();

        System.out.print("Enter the second string: ");
        String str2 = sc.nextLine();

        // Check if lengths are equal
        if (str1.length() != str2.length()) {
            System.out.println("The strings are NOT anagrams.");
        } else {
            // Convert strings to character arrays
            char[] arr1 = str1.toCharArray();
            char[] arr2 = str2.toCharArray();

            // Sort both arrays
            Arrays.sort(arr1);
            Arrays.sort(arr2);

            // Compare sorted arrays
            if (Arrays.equals(arr1, arr2)) {
                System.out.println("The strings ARE anagrams.");
            } else {
                System.out.println("The strings are NOT anagrams.");
            }
        }

        sc.close();
    }
}
```
## 2. Program to authenticate Case-insensitive login details using equals method.
```java
import java.util.Scanner;

class LoginAuth {
    public static void main(String[] args) {
        String validUsername = "admin";
        String validPassword = "Password123";

        Scanner sc = new Scanner(System.in);

        System.out.print("Enter username: ");
        String inputUsername = sc.nextLine();

        System.out.print("Enter password: ");
        String inputPassword = sc.nextLine();

        if (inputUsername.equalsIgnoreCase(validUsername) &&
                inputPassword.equals(validPassword)) {
            System.out.println("Login successful!");
        } else {
            System.out.println("Invalid username or password.");
        }

        sc.close();
    }
}
```
## 3. . Implement a java program to demonstrate creation of ArrayList, adding elements, removing elements, sorting elements of ArrayList. 
```
import java.util.ArrayList;
import java.util.Collections;

class ArrayListDemo {
    public static void main(String[] args) {
        ArrayList<String> fruits = new ArrayList<>();

        fruits.add("Banana");
        fruits.add("Apple");
        fruits.add("Mango");
        fruits.add("Orange");

        // Print the original list
        System.out.println("Original List: " + fruits);

        // Remove an element
        fruits.remove("Mango");

        // Print the list after removal
        System.out.println("After removing 'Mango': " + fruits);

        // Sort the ArrayList
        Collections.sort(fruits);

        // Print the sorted list
        System.out.println("Sorted List: " + fruits);
    }
}
```
## 4. Remove duplicate entries (Emails in mailing list) using Hashset
```java
import java.util.*;

class RemoveDuplicateEmails {
    public static void main(String[] args) {
        List<String> emailList = Arrays.asList(
                "user1@example.com",
                "user2@example.com",
                "user1@example.com", // duplicate
                "user3@example.com",
                "user2@example.com"  // duplicate
        );

        Set<String> uniqueEmails = new HashSet<>(emailList);

        System.out.println("Unique Email List:");
        for (String email : uniqueEmails) {
            System.out.println(email);
        }
    }
}
```
## 5. Store student details in a HashMap (Student ID - Name).
Implement methods to:
− Add a student.
− Retrieve a student's name.
− Remove a student.
− Display all students.
```java
import java.util.HashMap;
import java.util.Scanner;

class StudentDatabase {
    public static void main(String[] args) {
        HashMap<Integer, String> studentMap = new HashMap<>();
        Scanner scanner = new Scanner(System.in);
        int choice;

        do {
            System.out.println("\n--- Student Database Menu ---");
            System.out.println("1. Add Student");
            System.out.println("2. Retrieve Student Name");
            System.out.println("3. Remove Student");
            System.out.println("4. Display All Students");
            System.out.println("5. Exit");
            System.out.print("Enter your choice: ");
            choice = scanner.nextInt();

            switch (choice) {
                case 1:
                    // Add student
                    System.out.print("Enter Student ID: ");
                    int idToAdd = scanner.nextInt();
                    scanner.nextLine(); // consume newline
                    System.out.print("Enter Student Name: ");
                    String nameToAdd = scanner.nextLine();
                    studentMap.put(idToAdd, nameToAdd);
                    System.out.println("Student added successfully.");
                    break;

                case 2:
                    // Retrieve student
                    System.out.print("Enter Student ID to retrieve: ");
                    int idToRetrieve = scanner.nextInt();
                    String retrievedName = studentMap.get(idToRetrieve);
                    if (retrievedName != null) {
                        System.out.println("Student Name: " + retrievedName);
                    } else {
                        System.out.println("Student not found.");
                    }
                    break;

                case 3:
                    // Remove student
                    System.out.print("Enter Student ID to remove: ");
                    int idToRemove = scanner.nextInt();
                    if (studentMap.remove(idToRemove) != null) {
                        System.out.println("Student removed successfully.");
                    } else {
                        System.out.println("Student not found.");
                    }
                    break;

                case 4:
                    // Display all students
                    System.out.println("Student List:");
                    for (Integer id : studentMap.keySet()) {
                        System.out.println("ID: " + id + ", Name: " + studentMap.get(id));
                    }
                    break;

                case 5:
                    System.out.println("Exiting program...");
                    break;

                default:
                    System.out.println("Invalid choice! Please try again.");
            }
        } while (choice != 5);

        scanner.close();
    }
}
```
## 6. Create an AWT Frame with: Labels for Character, Key Code, Modifier Key, Action Key TextFields for displaying the corresponding values (Read-only).
- Implement KeyListener to handle key events.
- Display key details dynamically when a key is pressed:
- Character in the TextField.
- Key Code in the TextField.
- Modifier Key (Yes/No) in the TextField.
- Action Key (Yes/No) in the TextField.
- Change text colour based on specific keys:
  - A → Red
  - S → Green
  - D → Blue
  - W → Orange
- Any other key → Black
The expected outcome is:
  - Press A → Character: A, Key Code should be displayed, Modifier Key: No, Action Key: No
(Text should turn Red).
- Press Shift + A → Modifier Key: Yes, Key Code updates, Action Key: No.
- Press Arrow Keys → Action Key: Yes, Modifier Key updates accordingly.
- TextFields should dynamically update for each key press.

---
### **In Simple Words**
- We need to make a simple Java AWT program that creates a frame with labels and read-only text fields. It uses a KeyListener to display key event details and dynamically change the text color based on the key pressed.

✅ Features:
- Shows: Character, Key Code, Modifier Key (Yes/No), Action Key (Yes/No)

- Changes text color for A/S/D/W keys

- Handles Shift and Arrow keys
```java
import java.awt.*;
import java.awt.event.*;

class KeyEventDemoAWT extends Frame implements KeyListener {
    TextField charField, codeField, modifierField, actionField;

    public KeyEventDemoAWT() {
        setTitle("Key Event Demo");
        setSize(400, 300);
        setLayout(new GridLayout(4, 2, 10, 10));

        // Labels
        add(new Label("Character:"));
        charField = new TextField();
        charField.setEditable(false);
        add(charField);

        add(new Label("Key Code:"));
        codeField = new TextField();
        codeField.setEditable(false);
        add(codeField);

        add(new Label("Modifier Key:"));
        modifierField = new TextField();
        modifierField.setEditable(false);
        add(modifierField);

        add(new Label("Action Key:"));
        actionField = new TextField();
        actionField.setEditable(false);
        add(actionField);

        addKeyListener(this); // Attach key listener to the frame

        setVisible(true);

        // Ensure focus is on the Frame to capture key events
        this.requestFocus();
        addWindowListener(new WindowAdapter() {
            @Override
            public void windowClosing(WindowEvent e) {
                System.exit(0);
            }
        });
    }

    public void keyPressed(KeyEvent e) {
        char ch = e.getKeyChar();
        int code = e.getKeyCode();
        boolean isModifier = e.isShiftDown() || e.isControlDown() || e.isAltDown();
        boolean isAction = e.isActionKey();

        // Update fields
        charField.setText(String.valueOf(ch));
        codeField.setText(String.valueOf(code));
        modifierField.setText(isModifier ? "Yes" : "No");
        actionField.setText(isAction ? "Yes" : "No");

        // Set color based on key
        Color color;
        switch (Character.toUpperCase(ch)) {
            case 'A': color = Color.RED; break;
            case 'S': color = Color.GREEN; break;
            case 'D': color = Color.BLUE; break;
            case 'W': color = Color.ORANGE; break;
            default: color = Color.BLACK; break;
        }

        charField.setForeground(color);
        codeField.setForeground(color);
        modifierField.setForeground(color);
        actionField.setForeground(color);
    }

    public void keyReleased(KeyEvent e) {}
    public void keyTyped(KeyEvent e) {}

    public static void main(String[] args) {
        new KeyEventDemoAWT();
    }
}
```


