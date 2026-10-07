# CN-UDP-Socket

## CCD Lab Assignment

This project demonstrates **UDP Socket Programming in Python** using client-server communication.

The UDP server receives strings from student clients and processes them based on the number of students connected:

- **First 50% of students:** Converts the received string to **lowercase**
- **Remaining 50% of students:** **Reverses** the received string

The processed result is then sent back to the respective client.

---

## Files

```text
CN-UDP-Socket/
│
├── server.py
├── client.py
└── README.md
```

---

## Technologies Used

- Python
- UDP Socket Programming
- Client-Server Architecture
- UDP/IP

---

## How It Works

The server listens for UDP messages on:

```text
IP Address: 127.0.0.1
Port: 5005
```

The server is configured for a batch of **10 students** by default.

```python
TOTAL_STUDENTS = 10
```

The server divides the students into two groups:

| Students | Operation |
|---|---|
| First 50% (1–5) | Convert string to lowercase |
| Remaining 50% (6–10) | Reverse the string |

---

# How to Run

## Step 1: Open the Project Folder

Open a terminal and navigate to the project folder:

```bash
cd CN-UDP-Socket
```

Make sure both files are present:

```text
server.py
client.py
```

---

## Step 2: Start the Server

Open **Terminal 1** and run:

```bash
python server.py
```

You should see:

```text
UDP Server listening on 127.0.0.1:5005...
Expecting 10 students total.
```

The server is now waiting for student clients.

---

## Step 3: Start the Client

Open **Terminal 2** and run:

```bash
python client.py
```

Enter a string when prompted:

```text
Enter the string to process: HELLO WORLD
```

The client sends the string to the UDP server and waits for the response.

---

# Example 1 — First 50% of Students

For the first five students, the server converts the input to lowercase.

### Client

```text
Enter the string to process: HELLO WORLD
Sending data to server: HELLO WORLD
Received from server: hello world
```

### Server

```text
[Student 1] Received from ('127.0.0.1', 54321): 'HELLO WORLD'
Processing: First 50% (Lower Case) -> hello world
```

---

# Example 2 — Remaining 50% of Students

For students 6–10, the server reverses the input string.

### Client

```text
Enter the string to process: HELLO
Sending data to server: HELLO
Received from server: OLLEH
```

### Server

```text
[Student 6] Received from ('127.0.0.1', 54322): 'HELLO'
Processing: Remaining 50% (Reverse) -> OLLEH
```

---

# Server Configuration

You can change the total number of students in `server.py`:

```python
TOTAL_STUDENTS = 10
```

For example, for a batch of 20 students:

```python
TOTAL_STUDENTS = 20
```

The server automatically calculates half of the batch:

```python
HALF_MARK = TOTAL_STUDENTS // 2
```

Therefore:

- Students 1–10 → lowercase
- Students 11–20 → reverse

---

# Multiple Clients

The server processes clients one by one.

For example, with:

```python
TOTAL_STUDENTS = 10
```

you can run the client **10 times**.

Each client sends one string to the server.

The server keeps track of the student count:

```text
Student 1
Student 2
Student 3
...
Student 10
```

After processing all 10 students, the server shuts down automatically.

```text
All students processed. Server shutting down.
```

---

# Important Notes

- Start the **server before running the client**.
- The server uses **UDP**, so there is no TCP-style connection establishment.
- Both server and client use the same IP address and port:
  - IP: `127.0.0.1`
  - Port: `5005`
- The server must remain running while clients send messages.
- The server shuts down after processing `TOTAL_STUDENTS` messages.
- If the client does not receive a response within **5 seconds**, it displays a timeout error.

---

# UDP Communication Flow

```text
       CLIENT
          |
          |  String
          |  UDP
          ↓
       SERVER
          |
          |-- Students 1–5
          |      ↓
          |   Lowercase
          |
          |-- Students 6–10
          |      ↓
          |    Reverse
          |
          ↓
       CLIENT
          |
          |  Processed Result
          ↓
```

---

# Example

### Input

```text
HELLO COMPUTER
```

### If student is in first 50%

```text
hello computer
```

### If student is in remaining 50%

```text
retupmoc olleh
```

---

## Objective

To understand and implement **UDP socket communication** between a client and server, and to perform different string processing operations based on the number of students handled by the server.
