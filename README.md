<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <title>Real-Time Chat App</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet">
    <style>
        #chat-box {
            height: 400px;
            overflow-y: scroll;
            border: 1px solid #ccc;
            padding: 10px;
            background: #f9f9f9;
        }
        .message {
            margin-bottom: 10px;
        }
        .message .user {
            font-weight: bold;
        }
    </style>
</head>
<body class="bg-light">

<div class="container py-5">
    <div class="card shadow-lg">
        <div class="card-header text-center bg-primary text-white">
            <h3>💬 Real-Time Chat Application</h3>
        </div>
        <div class="card-body">
            <div id="username-section" class="mb-4">
                <label for="username" class="form-label">Enter your name to join the chat:</label>
                <input type="text" id="username" class="form-control mb-2" placeholder="Your name">
                <button class="btn btn-success w-100" onclick="connect()">Join Chat</button>
            </div>

            <div id="chat-section" style="display: none;">
                <div id="chat-box" class="mb-3"></div>
                <div class="input-group">
                    <input type="text" id="message" class="form-control" placeholder="Type your message here..." onkeyup="checkEnter(event)">
                    <button class="btn btn-primary" onclick="sendMessage()">Send</button>
                </div>
            </div>
        </div>
    </div>
</div>

<!-- STOMP & SockJS -->
<script src="https://cdn.jsdelivr.net/npm/sockjs-client@1.6.1/dist/sockjs.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/stompjs@2.3.3/lib/stomp.min.js"></script>

<script>
    let stompClient = null;
    let username = null;

    function connect() {
        username = document.getElementById("username").value.trim();
        if (!username) {
            alert("Please enter a valid name.");
            return;
        }

        let socket = new SockJS('/ws');
        stompClient = Stomp.over(socket);

        stompClient.connect({}, function () {
            document.getElementById("username-section").style.display = "none";
            document.getElementById("chat-section").style.display = "block";

            stompClient.subscribe('/topic/public', function (messageOutput) {
                let message = JSON.parse(messageOutput.body);
                showMessage(message);
            });

            stompClient.send("/app/chat.sendMessage", {}, JSON.stringify({
                sender: username,
                content: username + " joined the chat",
                type: 'JOIN'
            }));
        });
    }

    function sendMessage() {
        let messageInput = document.getElementById("message");
        let messageContent = messageInput.value.trim();
        if (messageContent && stompClient) {
            let chatMessage = {
                sender: username,
                content: messageContent,
                type: 'CHAT'
            };
            stompClient.send("/app/chat.sendMessage", {}, JSON.stringify(chatMessage));
            messageInput.value = '';
        }
    }

    function checkEnter(event) {
        if (event.key === "Enter") {
            sendMessage();
        }
    }

    function showMessage(message) {
        let chatBox = document.getElementById("chat-box");
        let msgElement = document.createElement("div");
        msgElement.classList.add("message");

        if (message.type === 'JOIN') {
            msgElement.innerHTML = `<em>${message.content}</em>`;
        } else {
            msgElement.innerHTML = `<span class="user">${message.sender}:</span> ${message.content}`;
        }

        chatBox.appendChild(msgElement);
        chatBox.scrollTop = chatBox.scrollHeight;
    }
</script>

</body>
</html>
