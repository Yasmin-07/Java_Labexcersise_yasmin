1. Project Overview
This project consists of a distributed, multi-client Real-Time Chat Application composed of two main programs: a Chat Server and a Chat Client.

The system utilizes a central server architecture where a network backend (ChatServer) coordinates communication among multiple graphical interfaces (ChatClient) built using JavaFX. The application also incorporates data persistence via a MySQL database to store and retrieve chat history.

2. System Architecture
The application runs on a classic Client-Server Architecture linked together via standard TCP/IP network sockets:

The Server (ChatServer.java): A multithreaded console application running continuously on port 5000. It manages active network sockets, controls client lifecycles, writes active messages to a MySQL database table, and broadcasts inbound payloads to all active clients simultaneously.

The Client (ChatClient.java): A graphical desktop interface that enables users to input a username, connect to the server, read chat logs, and exchange real-time text streams.

3. Key Technical Features
A. Multithreading & Concurrency
To ensure smooth operational scaling, the application separates its network tasks from its presentation logic:

Server-Side Handlers: The server delegates every incoming connection to a separate ClientHandler thread. This enables the server to handle multiple clients concurrently without getting blocked by a single user's slow connection.

Client-Side Sockets: The client runs its network listener loop inside a separate background thread. This separates network I/O from the UI thread, ensuring the window remains responsive while waiting for data.

Thread-Safe UI Modifying: When updating the interface from the background network thread, the client uses Platform.runLater(). This ensures all additions to the JavaFX window are executed safely on the primary UI thread.

B. Synchronization & Thread Safety
The server shares a central list of output streams (clients) among all active connection threads. To prevent data corruption from concurrent modifications (e.g., when multiple users join or leave at the exact same time), the code utilizes explicit synchronized code blocks to maintain thread safety.

C. Persistent Chat History
Rather than losing conversation context when a server restarts, the application integrates persistent SQL database controls:

Idempotent Initialization: The server verifies or auto-provisions the required database schema (chatapp) and message storage tables at startup.

History Injection: Upon establishing a new connection, the server queries the database for the 50 limit history logs and streams them to the newly connected client before opening the live broadcast channel.

4. Conclusion
This real-time chat program demonstrates a strong grasp of core networking and database concepts. By combining multithreaded socket operations with automated MySQL storage routines and a clean JavaFX frontend, the application provides a robust blueprint for an asynchronous, multi-client messaging platform.
