1. Project Overview
This project is a desktop Notepad Application built using JavaFX for the graphical user interface (GUI) and MySQL for data persistence. The application allows users to perform full CRUD (Create, Read, Update, Delete) operations on personal text notes through an intuitive, interactive layout.

2. System Architecture
The application is designed using a self-contained, single-file architecture (NotepadApp.java) for straightforward deployment and evaluation. It features three primary layers:

Data Layer (Note Class): A static nested class that serves as the data model, capturing the ID, title, and body text of each note.

Presentation Layer (JavaFX GUI): A split-pane layout using an HBox. The left pane contains navigation controls (action buttons and a ListView), while the right pane contains text editing areas (TextField and TextArea).

Persistence Layer (JDBC): Handles direct communication with a local MySQL database instance (notepaddb) to automatically initialize the storage table, save new records, update edits, or remove entries.

3. Key Technical Features
A. Dynamic UI Syncing
The application binds the UI ListView to a reactive ObservableList<Note>. When a note is added, updated, or deleted, the interface automatically refreshes in real time without requiring a manual page reload or view reset.

B. Safe Resource Management
All database methods implement Java’s modern Try-with-Resources syntax. This ensures that database connections, statements, and result sets are automatically closed after execution, completely preventing memory leaks and dangling socket connections.

C. SQL Injection Prevention
Database queries use parameterized PreparedStatement boundaries instead of raw string concatenation. This protects the application from common malicious SQL Injection vulnerabilities by treating user input strictly as data rather than executable code.

4. Conclusion
The NotepadApp successfully delivers a robust, secure, and user-friendly solution for managing notes. By combining the reactive properties of JavaFX with the data reliability of MySQL, the program handles data safely and updates smoothly, meeting all standard criteria for an object-oriented desktop application submission.
