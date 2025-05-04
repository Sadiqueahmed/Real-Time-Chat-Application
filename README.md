<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Real-Time Chat App - README</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet">
    <style>
        body {
            padding-top: 40px;
            padding-bottom: 40px;
            background-color: #f8f9fa;
        }
        h1, h2, h3 {
            color: #0d6efd;
        }
        pre {
            background: #f1f1f1;
            padding: 10px;
            border-radius: 5px;
            overflow-x: auto;
        }
    </style>
</head>
<body>
<div class="container">
    <h1 class="mb-4">💬 Real-Time Chat Application</h1>

    <p>This is a web-based real-time chat application built with <strong>Spring Boot</strong>, <strong>WebSockets</strong>, <strong>STOMP</strong>, <strong>SockJS</strong>, <strong>Thymeleaf</strong>, and <strong>Bootstrap 5</strong>.</p>

    <h2>🚀 Features</h2>
    <ul>
        <li>Real-time chat using WebSocket protocol</li>
        <li>STOMP messaging support</li>
        <li>Simple and responsive UI</li>
        <li>User join notifications</li>
        <li>Auto-scrolling chat box</li>
    </ul>

    <h2>🖥️ Technologies Used</h2>
    <ul>
        <li>Java + Spring Boot</li>
        <li>Thymeleaf</li>
        <li>WebSocket, STOMP, SockJS</li>
        <li>Bootstrap 5</li>
        <li>HTML, CSS, JavaScript</li>
    </ul>

    <h2>📸 Screenshot</h2>
    <p>You can add a screenshot by replacing the path below:</p>
    <img src="path/to/screenshot.png" alt="Chat App Screenshot" class="img-fluid rounded shadow">

    <h2>🛠️ How to Run</h2>
    <ol>
        <li><strong>Clone the repository</strong>:
            <pre><code>git clone https://github.com/yourusername/your-chat-app.git
cd your-chat-app</code></pre>
        </li>
        <li><strong>Run the Spring Boot application</strong>:
            <pre><code>./mvnw spring-boot:run</code></pre>
        </li>
        <li><strong>Open your browser</strong> and go to:
            <pre><code>http://localhost:8080</code></pre>
        </li>
    </ol>

    <h2>📂 Project Structure</h2>
    <pre><code>src
├── main
│   ├── java
│   │   └── com.example.chat
│   │       ├── controller
│   │       ├── model
│   │       ├── config
│   │       └── ChatApplication.java
│   └── resources
│       ├── static
│       ├── templates
│       └── application.properties</code></pre>

    <h2>🙌 Contribution</h2>
    <p>Feel free to fork the project, open issues, or submit pull requests.</p>

    <h2>📄 License</h2>
    <p>This project is licensed under the MIT License.</p>
</div>
</body>
</html>
