
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Social Media App</title>
    <script src="https://www.gstatic.com/firebasejs/9.6.1/firebase-app.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.6.1/firebase-auth.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.6.1/firebase-firestore.js"></script>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            margin: 0;
            padding: 0;
            background-color: #f0f0f0;
            color: #333;
        }

        header {
            background-color: #4A90E2;
            padding: 20px;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.2);
            color: white;
        }

        nav ul {
            list-style-type: none;
            padding: 0;
        }

        nav ul li {
            display: inline;
            margin-right: 20px;
        }

        nav a {
            text-decoration: none;
            color: white;
            font-weight: bold;
            transition: color 0.3s;
        }

        nav a:hover {
            color: #FFD700; /* Gold color on hover */
        }

        main {
            padding: 20px;
            max-width: 800px;
            margin: auto;
        }

        section {
            background-color: white;
            border-radius: 8px;
            padding: 20px;
            margin-bottom: 20px;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
        }

        h2 {
            color: #4A90E2;
        }

        #chat-window {
            border: 1px solid #ccc;
            border-radius: 8px;
            padding: 10px;
            background-color: #f9f9f9;
            max-width: 400px;
            margin: auto;
        }

        #messages {
            height: 200px;
            overflow-y: scroll;
            border: 1px solid #ccc;
            border-radius: 8px;
            margin-bottom: 10px;
            padding: 5px;
            background-color: white;
        }

        #message-input {
            width: 75%;
            padding: 10px;
            border: 1px solid #ccc;
            border-radius: 4px;
            margin-right: 5px;
        }

        #send-button {
            padding: 10px;
            background-color: #4A90E2;
            color: white;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            transition: background-color 0.3s;
        }

        #send-button:hover {
            background-color: #357ABD; /* Darker blue on hover */
        }

        footer {
            text-align: center;
            padding: 10px;
            background-color: #4A90E2;
            color: white;
            position: relative;
            bottom: 0;
            width: 100%;
        }
    </style>
</head>
<body>
    <header>
        <h1>My Social Media App</h1>
        <nav>
            <ul>
                <li><a href="#home">Home</a></li>
                <li><a href="#chat">Chat</a></li>
                <li><a href="#profile">Profile</a></li>
            </ul>
        </nav>
    </header>
    
    <main>
        <section id="home">
            <h2>Welcome to My Social Media App</h2>
            <p>Share your moments with friends!</p>
        </section>
        
        <section id="chat">
            <h2>Chat</h2>
            <div id="chat-window">
                <div id="messages"></div>
                <input type="text" id="message-input" placeholder="Type a message...">
                <button id="send-button">Send</button>
            </div>
        </section>
        
        <section id="profile">
            <h2>Your Profile</h2>
            <p>Manage your account settings here.</p>
        </section>
    </main>

    <footer>
        <p>&copy; 2023 My Social Media App</p>
    </footer>

    <script>
        // Initialize Firebase
        const firebaseConfig = {
            apiKey: "AIzaSyBhDzhvIYm_ayEhSy9YtRvkeiXrajZH5q8",
            authDomain: "heoster-class-2024.firebaseapp.com",
            projectId: "heoster-class-2024",
            storageBucket: "heoster-class-2024.firebasestorage.app",
            messagingSenderId: "832744733078",
            appId: "1:832744733078:web:6f1ea8bdaf7acbce5e45b7",
            measurementId: "G-FSX9SZWZP3"
        };

        const app = firebase.initializeApp(firebaseConfig);
        const db = firebase.firestore();

        const messagesDiv = document.getElementById('messages');
        const messageInput = document.getElementById('message-input');
        const sendButton = document.getElementById('send-button');

        // Send message
        sendButton.addEventListener('click', () => {
            const message = messageInput.value;
            if (message) {
                db.collection('messages').add({
                    text: message,
                    timestamp: firebase.firestore.FieldValue.serverTimestamp()
                });
                messageInput.value = '';
            }
        });

        // Listen for messages
        db.collection('messages').orderBy('timestamp')
            .onSnapshot((snapshot) => {
                messagesDiv.innerHTML = '';
                snapshot.forEach(doc => {
                    const message = doc.data().text;
                    const messageElement = document.createElement('div');
                    messageElement.textContent = message;
                    messagesDiv.appendChild(messageElement);
                });
            });
    </script>
</body>
</html>