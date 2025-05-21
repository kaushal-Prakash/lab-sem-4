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

class KeyEventDemoAWTNoExtend {

    public static void main(String[] args) {
        // Create Frame
        Frame frame = new Frame("Key Event Demo");
        frame.setSize(400, 300);
        frame.setLayout(new GridLayout(4, 2, 10, 10));

        // Create components
        Label lblChar = new Label("Character:");
        TextField charField = new TextField();
        charField.setEditable(false);

        Label lblCode = new Label("Key Code:");
        TextField codeField = new TextField();
        codeField.setEditable(false);

        Label lblModifier = new Label("Modifier Key:");
        TextField modifierField = new TextField();
        modifierField.setEditable(false);

        Label lblAction = new Label("Action Key:");
        TextField actionField = new TextField();
        actionField.setEditable(false);

        // Add components to frame
        frame.add(lblChar);
        frame.add(charField);
        frame.add(lblCode);
        frame.add(codeField);
        frame.add(lblModifier);
        frame.add(modifierField);
        frame.add(lblAction);
        frame.add(actionField);

        // Add KeyListener to frame
        frame.addKeyListener(new KeyListener() {
            @Override
            public void keyPressed(KeyEvent e) {
                char ch = e.getKeyChar();
                int code = e.getKeyCode();
                boolean isModifier = e.isShiftDown() || e.isControlDown() || e.isAltDown();
                boolean isAction = e.isActionKey();

                // Update text fields
                charField.setText(String.valueOf(ch));
                codeField.setText(String.valueOf(code));
                modifierField.setText(isModifier ? "Yes" : "No");
                actionField.setText(isAction ? "Yes" : "No");

                // Set color based on key pressed
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

            @Override
            public void keyReleased(KeyEvent e) {}

            @Override
            public void keyTyped(KeyEvent e) {}
        });

        // Window close handler
        frame.addWindowListener(new WindowAdapter() {
            public void windowClosing(WindowEvent e) {
                frame.dispose();
                System.exit(0);
            }
        });

        frame.setVisible(true);
        // Important: set focus to frame to receive key events
        frame.requestFocus();
    }
}
```
## 7. Implement a java program to illustrate the use of different types of String constructors.
```java
class StringConstructorsDemo {
    public static void main(String[] args) {
        // 1. Empty String
        String str1 = new String();
        System.out.println("1. Empty String: \"" + str1 + "\"");

        // 2. String from another String
        String str2 = new String("Hello World");
        System.out.println("2. String from another string: \"" + str2 + "\"");

        // 3. String from character array
        char[] charArray = { 'J', 'a', 'v', 'a' };
        String str3 = new String(charArray);
        System.out.println("3. String from char array: \"" + str3 + "\"");

        // 4. String from byte array
        byte[] byteArray = { 72, 101, 108, 108, 111 }; // ASCII values of 'Hello'
        String str4 = new String(byteArray);
        System.out.println("4. String from byte array: \"" + str4 + "\"");

        // 5. String from part of a char array
        String str5 = new String(charArray, 1, 2); // "av"
        System.out.println("5. String from part of char array: \"" + str5 + "\"");

        // 6. String from part of a byte array
        String str6 = new String(byteArray, 1, 3); // "ell"
        System.out.println("6. String from part of byte array: \"" + str6 + "\"");
    }
}
```
## 8. Sort the list of strings using Bubble sort using compareTo()
```java
class SortString {
    public static void main(String args[]) {
        String arr[] = {
                "Java", "is", "an", "object", "oriented",
                "programming", "language", "that", "allows",
                "code", "reusability", "and", "modularity"
        };
        int n = arr.length;
        // Bubble Sort using compareTo
        for (int i = 0; i < n - 1; i++) {
            for (int j = 0; j < n - 1 - i; j++) {
                if (arr[j].compareTo(arr[j + 1]) > 0) {
                    // Swap arr[j] and arr[j + 1]
                    String temp = arr[j];
                    arr[j] = arr[j + 1];
                    arr[j + 1] = temp;
                }
            }
        }
        // Print sorted strings
        System.out.println("Sorted Strings:");
        for (String str : arr) {
            System.out.print(str + " ");
        }
    }
}
```
## 9.  simple Java program that demonstrates the use of various StringBuffer methods
```java
class StringBufferMethodsDemo {
    public static void main(String[] args) {
        // 1. Creating a StringBuffer
        StringBuffer sb = new StringBuffer("Hello");
        System.out.println("Original: " + sb);

        // 2. append()
        sb.append(" World");
        System.out.println("After append: " + sb);

        // 3. insert()
        sb.insert(5, " Java");
        System.out.println("After insert: " + sb);

        // 4. replace()
        sb.replace(6, 10, "Cool");
        System.out.println("After replace: " + sb);

        // 5. delete()
        sb.delete(5, 10);
        System.out.println("After delete: " + sb);

        // 6. reverse()
        sb.reverse();
        System.out.println("After reverse: " + sb);

        // 7. length()
        System.out.println("Length: " + sb.length());

        // 8. capacity()
        System.out.println("Capacity: " + sb.capacity());

        // 9. ensureCapacity()
        sb.ensureCapacity(50);
        System.out.println("Capacity after ensureCapacity(50): " + sb.capacity());

        // 10. setCharAt()
        sb.setCharAt(0, 'Z');
        System.out.println("After setCharAt(0, 'Z'): " + sb);

        // 11. charAt()
        System.out.println("Character at index 1: " + sb.charAt(1));
    }
}
```
## 10. simple java programe to show the use of different type of character extraction string comparision ,string search, and string modification methods
```java
class StringMethodsDemo {
    public static void main(String[] args) {
        String str = "Java Programming";

        // ===== 1. Character Extraction =====
        char ch = str.charAt(5);  // Get character at index 5
        System.out.println("Character at index 5: " + ch);

        // ===== 2. String Comparison =====
        String str2 = "java programming";
        System.out.println("Equals: " + str.equals(str2));                   // false
        System.out.println("Equals Ignore Case: " + str.equalsIgnoreCase(str2)); // true
        System.out.println("Compare To: " + str.compareTo(str2));           // based on Unicode diff

        // ===== 3. String Search =====
        System.out.println("Index of 'Pro': " + str.indexOf("Pro"));        // 5
        System.out.println("Contains 'gram': " + str.contains("gram"));     // true
        System.out.println("Starts with 'Java': " + str.startsWith("Java")); // true
        System.out.println("Ends with 'ing': " + str.endsWith("ing"));      // true

        // ===== 4. String Modification =====
        System.out.println("To Uppercase: " + str.toUpperCase());           // JAVA PROGRAMMING
        System.out.println("To Lowercase: " + str.toLowerCase());           // java programming
        System.out.println("Replace 'a' with '@': " + str.replace('a', '@'));
        System.out.println("Substring (5 to 16): " + str.substring(5, 16)); // Programming
        System.out.println("Trim (with spaces): '" + "  Hello  ".trim() + "'"); // "Hello"
    }
}
```
## 11. . Drawing on AWT Canvas
- Create a class extending Canvas and override the paint(Graphics g) method.
- In the paint method, draw:
A filled rectangle, oval, and a line.
- Display mouse coordinates as the user moves the mouse (MouseMotionListener).
- Create a Frame and add the Canvas to it.
− Add a Button to change the color of shapes dynamically using an ActionListener.
```java
import java.awt.*;
import java.awt.event.*;

class AWTCanvasExample {
    public static void main(String[] args) {
        // Create Frame
        Frame frame = new Frame("Canvas Drawing Example");

        // Create Canvas
        Canvas canvas = new Canvas() {
            private int mouseX = 0, mouseY = 0;
            private Color shapeColor = Color.RED;

            {
                // Add mouse motion listener inside instance initializer
                addMouseMotionListener(new MouseMotionAdapter() {
                    public void mouseMoved(MouseEvent e) {
                        mouseX = e.getX();
                        mouseY = e.getY();
                        repaint();
                    }
                });
            }

            // Add method to change color
            public void setShapeColor(Color newColor) {
                shapeColor = newColor;
                repaint();
            }

            public void paint(Graphics g) {
                g.setColor(shapeColor);
                g.fillRect(50, 50, 100, 60);      // Rectangle
                g.fillOval(180, 50, 100, 60);     // Oval
                g.drawLine(50, 150, 250, 150);    // Line

                g.setColor(Color.BLACK);
                g.drawString("Mouse: (" + mouseX + ", " + mouseY + ")", 50, 220);
            }
        };

        canvas.setSize(350, 250);
        canvas.setBackground(Color.WHITE);

        // Create button to change color
        Button btn = new Button("Change Color");

        // Add ActionListener to button
        btn.addActionListener(new ActionListener() {
            private boolean toggle = true;

            public void actionPerformed(ActionEvent e) {
                Color newColor = toggle ? Color.BLUE : Color.RED;
                // Call setShapeColor through casting since it's anonymous subclass
                ((Canvas) canvas).setForeground(newColor); // Optional: set text color
                try {
                    canvas.getClass().getMethod("setShapeColor", Color.class)
                            .invoke(canvas, newColor);
                } catch (Exception ex) {
                    ex.printStackTrace();
                }
                toggle = !toggle;
            }
        });

        // Layout and add components
        frame.setLayout(new BorderLayout());
        frame.add(canvas, BorderLayout.CENTER);
        frame.add(btn, BorderLayout.SOUTH);

        frame.setSize(400, 350);
        frame.setVisible(true);

        // Handle window close
        frame.addWindowListener(new WindowAdapter() {
            public void windowClosing(WindowEvent e) {
                frame.dispose();
            }
        });
    }
}
```
## 12. simple calculator implemented in both AWT and Swing for addition, subtraction, multiplication, and division.

### **Using AWT**
```java
import java.awt.*;
import java.awt.event.*;

class SimpleCalcAWT {
    public static void main(String[] args) {
        Frame frame = new Frame("AWT Calculator");
        frame.setSize(300, 200);
        frame.setLayout(new GridLayout(3, 2, 10, 10));

        TextField num1 = new TextField();
        TextField num2 = new TextField();
        TextField result = new TextField();
        result.setEditable(false);

        Panel buttonPanel = new Panel();
        buttonPanel.setLayout(new GridLayout(1, 4, 5, 5));

        Button addBtn = new Button("+");
        Button subBtn = new Button("-");
        Button mulBtn = new Button("*");
        Button divBtn = new Button("/");

        buttonPanel.add(addBtn);
        buttonPanel.add(subBtn);
        buttonPanel.add(mulBtn);
        buttonPanel.add(divBtn);

        frame.add(new Label("Number 1:"));
        frame.add(num1);
        frame.add(new Label("Number 2:"));
        frame.add(num2);
        frame.add(buttonPanel);
        frame.add(result);

        // Action listeners for buttons
        addBtn.addActionListener(e -> {
            double r = parseDouble(num1.getText()) + parseDouble(num2.getText());
            result.setText(String.valueOf(r));
        });
        subBtn.addActionListener(e -> {
            double r = parseDouble(num1.getText()) - parseDouble(num2.getText());
            result.setText(String.valueOf(r));
        });
        mulBtn.addActionListener(e -> {
            double r = parseDouble(num1.getText()) * parseDouble(num2.getText());
            result.setText(String.valueOf(r));
        });
        divBtn.addActionListener(e -> {
            double d2 = parseDouble(num2.getText());
            if (d2 != 0) {
                double r = parseDouble(num1.getText()) / d2;
                result.setText(String.valueOf(r));
            } else {
                result.setText("Cannot divide by zero");
            }
        });

        frame.addWindowListener(new WindowAdapter() {
            public void windowClosing(WindowEvent e) {
                frame.dispose();
                System.exit(0);
            }
        });

        frame.setVisible(true);
    }

    private static double parseDouble(String s) {
        try {
            return Double.parseDouble(s);
        } catch (NumberFormatException e) {
            return 0;
        }
    }
}
```
### **Uing Swing**
```java
import javax.swing.*;
import java.awt.*;
import java.awt.event.*;

class SimpleCalcSwing {
    public static void main(String[] args) {
        JFrame frame = new JFrame("Swing Calculator");
        frame.setSize(300, 200);
        frame.setLayout(new GridLayout(3, 2, 10, 10));

        JTextField num1 = new JTextField();
        JTextField num2 = new JTextField();
        JTextField result = new JTextField();
        result.setEditable(false);

        JPanel buttonPanel = new JPanel(new GridLayout(1, 4, 5, 5));

        JButton addBtn = new JButton("+");
        JButton subBtn = new JButton("-");
        JButton mulBtn = new JButton("*");
        JButton divBtn = new JButton("/");

        buttonPanel.add(addBtn);
        buttonPanel.add(subBtn);
        buttonPanel.add(mulBtn);
        buttonPanel.add(divBtn);

        frame.add(new JLabel("Number 1:"));
        frame.add(num1);
        frame.add(new JLabel("Number 2:"));
        frame.add(num2);
        frame.add(buttonPanel);
        frame.add(result);

        // Action listeners for buttons
        addBtn.addActionListener(e -> {
            double r = parseDouble(num1.getText()) + parseDouble(num2.getText());
            result.setText(String.valueOf(r));
        });
        subBtn.addActionListener(e -> {
            double r = parseDouble(num1.getText()) - parseDouble(num2.getText());
            result.setText(String.valueOf(r));
        });
        mulBtn.addActionListener(e -> {
            double r = parseDouble(num1.getText()) * parseDouble(num2.getText());
            result.setText(String.valueOf(r));
        });
        divBtn.addActionListener(e -> {
            double d2 = parseDouble(num2.getText());
            if (d2 != 0) {
                double r = parseDouble(num1.getText()) / d2;
                result.setText(String.valueOf(r));
            } else {
                result.setText("Cannot divide by zero");
            }
        });

        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.setVisible(true);
    }

    private static double parseDouble(String s) {
        try {
            return Double.parseDouble(s);
        } catch (NumberFormatException e) {
            return 0;
        }
    }
}
```
### Comparison:
- AWT	
  - Aesthetics	Looks more basic uses native OS widgets	
  - Behavior	Less flexible
  - Limited styling options	Supports
- Swing
  - More modern, consistent look across OS
  - can behave differently on OS	More consistent look & feel
  - pluggable look and feel, rich components
	 
## 13. Act as a business analyst to reverse engineer a given screenshot of a java Swing application
```java
import javax.swing.*;
import java.awt.*;
import java.util.ArrayList;

class Student {
    String name, usn, branch;

    Student(String name, String usn, String branch) {
        this.name = name;
        this.usn = usn;
        this.branch = branch;
    }

    @Override
    public String toString() {
        return "Name: " + name + ", USN: " + usn + ", Branch: " + branch;
    }
}

class StudentForm {
    JTextField nameField, usnField, branchField;
    JTextArea displayArea;
    ArrayList<Student> studentList;
    JFrame frame;

    public StudentForm() {
        studentList = new ArrayList<>();

        frame = new JFrame("Student Information Form");
        frame.setSize(400, 350);
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.setLayout(new BorderLayout(10, 10)); // BorderLayout with some gaps

        // Panel for Labels and Text Fields (3 rows, 2 columns)
        JPanel inputPanel = new JPanel(new GridLayout(3, 2, 5, 5));
        inputPanel.setBorder(BorderFactory.createTitledBorder("Enter Student Details"));

        inputPanel.add(new JLabel("Name:"));
        nameField = new JTextField(20);
        inputPanel.add(nameField);

        inputPanel.add(new JLabel("USN:"));
        usnField = new JTextField(20);
        inputPanel.add(usnField);

        inputPanel.add(new JLabel("Branch:"));
        branchField = new JTextField(20);
        inputPanel.add(branchField);

        frame.add(inputPanel, BorderLayout.NORTH);

        // Panel for buttons
        JPanel buttonPanel = new JPanel(new FlowLayout());
        JButton addButton = new JButton("Add");
        JButton clearButton = new JButton("Clear");
        JButton viewButton = new JButton("View All");
        buttonPanel.add(addButton);
        buttonPanel.add(clearButton);
        buttonPanel.add(viewButton);
        frame.add(buttonPanel, BorderLayout.CENTER);

        // Display area with scroll pane
        displayArea = new JTextArea(8, 30);
        displayArea.setEditable(false);
        JScrollPane scrollPane = new JScrollPane(displayArea);
        scrollPane.setBorder(BorderFactory.createTitledBorder("Student List"));
        frame.add(scrollPane, BorderLayout.SOUTH);

        // Button actions
        addButton.addActionListener(e -> addStudent());
        clearButton.addActionListener(e -> clearFields());
        viewButton.addActionListener(e -> viewAllStudents());

        frame.setLocationRelativeTo(null); // Center the frame on screen
        frame.setVisible(true);
    }

    void addStudent() {
        String name = nameField.getText().trim();
        String usn = usnField.getText().trim();
        String branch = branchField.getText().trim();

        if (name.isEmpty() || usn.isEmpty() || branch.isEmpty()) {
            JOptionPane.showMessageDialog(frame, "All fields must be filled!", "Error", JOptionPane.ERROR_MESSAGE);
            return;
        }
        studentList.add(new Student(name, usn, branch));
        JOptionPane.showMessageDialog(frame, "Student added successfully!", "Message", JOptionPane.INFORMATION_MESSAGE);
        clearFields();
    }

    void clearFields() {
        nameField.setText("");
        usnField.setText("");
        branchField.setText("");
    }

    void viewAllStudents() {
        displayArea.setText("");
        for (Student s : studentList) {
            displayArea.append(s.toString() + "\n");
        }
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(StudentForm::new);
    }
}
```
## 14. Swing application that creates two buttons — Alpha and Beta — and displays a message dialog when either is pressed
```java
import javax.swing.*;
import java.awt.*;
import java.awt.event.*;

class ButtonDemo {
    public static void main(String[] args) {
        // Run on Event Dispatch Thread for thread safety
        SwingUtilities.invokeLater(() -> {
            JFrame frame = new JFrame("Button Demo");
            frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
            frame.setSize(300, 150);
            frame.setLayout(new FlowLayout());

            JButton alphaButton = new JButton("Alpha");
            JButton betaButton = new JButton("Beta");

            // Add action listeners
            alphaButton.addActionListener(e ->
                    JOptionPane.showMessageDialog(frame, "Alpha pressed"));

            betaButton.addActionListener(e ->
                    JOptionPane.showMessageDialog(frame, "Beta pressed"));

            // Add buttons to frame
            frame.add(alphaButton);
            frame.add(betaButton);

            frame.setLocationRelativeTo(null); // center frame
            frame.setVisible(true);
        });
    }
}
```