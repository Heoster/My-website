<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>SocialConnect</title>
    <script src="https://www.gstatic.com/firebasejs/9.6.1/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.6.1/firebase-auth-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.6.1/firebase-firestore-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.6.1/firebase-storage-compat.js"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
    <style>
  
        :root {
            --primary-color: #4A90E2;
            --secondary-color: #FFD700;
            --dark-color: #333;
            --light-color: #f0f0f0;
            --danger-color: #e74c3c;
            --success-color: #2ecc71;
            --white: #ffffff;
            --gray: #95a5a6;
            --dark-gray: #7f8c8d;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: var(--light-color);
            color: var(--dark-color);
            line-height: 1.6;
        }

        header {
            background-color: var(--primary-color);
            padding: 1rem 2rem;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.2);
            color: var(--white);
            position: sticky;
            top: 0;
            z-index: 100;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .logo {
            font-size: 1.5rem;
            font-weight: bold;
            display: flex;
            align-items: center;
        }

        .logo i {
            margin-right: 0.5rem;
            color: var(--secondary-color);
        }

        nav ul {
            list-style-type: none;
            display: flex;
            align-items: center;
        }

        nav ul li {
            margin-left: 1.5rem;
        }

        nav a {
            text-decoration: none;
            color: var(--white);
            font-weight: 600;
            transition: color 0.3s;
            display: flex;
            align-items: center;
        }

        nav a i {
            margin-right: 0.3rem;
        }

        nav a:hover {
            color: var(--secondary-color);
        }

        .auth-buttons button {
            padding: 0.5rem 1rem;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            font-weight: 600;
            transition: all 0.3s;
            margin-left: 1rem;
        }

        .login-btn {
            background-color: transparent;
            color: var(--white);
            border: 1px solid var(--white);
        }

        .login-btn:hover {
            background-color: rgba(255, 255, 255, 0.1);
        }

        .signup-btn {
            background-color: var(--secondary-color);
            color: var(--dark-color);
        }

        .signup-btn:hover {
            background-color: #e6c200;
        }

        .user-profile {
            display: flex;
            align-items: center;
            cursor: pointer;
            position: relative;
        }

        .user-avatar {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            object-fit: cover;
            margin-right: 0.5rem;
            border: 2px solid var(--white);
        }

        .dropdown-menu {
            position: absolute;
            top: 100%;
            right: 0;
            background-color: var(--white);
            border-radius: 4px;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
            padding: 0.5rem 0;
            min-width: 150px;
            display: none;
        }

        .dropdown-menu.show {
            display: block;
        }

        .dropdown-menu a {
            color: var(--dark-color);
            padding: 0.5rem 1rem;
            display: block;
        }

        .dropdown-menu a:hover {
            background-color: var(--light-color);
            color: var(--primary-color);
        }

        main {
            padding: 2rem;
            max-width: 1200px;
            margin: 0 auto;
            display: grid;
            grid-template-columns: 1fr 2fr 1fr;
            gap: 2rem;
        }

        .sidebar {
            position: sticky;
            top: 80px;
            height: fit-content;
        }

        .feed {
            display: flex;
            flex-direction: column;
            gap: 1.5rem;
        }

        section {
            background-color: var(--white);
            border-radius: 8px;
            padding: 1.5rem;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
        }

        h2 {
            color: var(--primary-color);
            margin-bottom: 1rem;
            font-size: 1.5rem;
        }

        .post-form {
            display: flex;
            flex-direction: column;
            gap: 1rem;
        }

        .post-input {
            width: 100%;
            padding: 1rem;
            border: 1px solid #ccc;
            border-radius: 4px;
            resize: none;
            font-family: inherit;
            font-size: 1rem;
        }

        .post-actions {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .media-upload {
            display: flex;
            gap: 1rem;
        }

        .media-upload label {
            cursor: pointer;
            color: var(--primary-color);
            font-size: 1.2rem;
        }

        .media-upload input {
            display: none;
        }

        .post-button {
            padding: 0.5rem 1.5rem;
            background-color: var(--primary-color);
            color: var(--white);
            border: none;
            border-radius: 4px;
            font-weight: 600;
            cursor: pointer;
            transition: background-color 0.3s;
        }

        .post-button:hover {
            background-color: #357ABD;
        }

        .post {
            display: flex;
            flex-direction: column;
            gap: 1rem;
            padding-bottom: 1rem;
            border-bottom: 1px solid #eee;
            margin-bottom: 1rem;
        }

        .post:last-child {
            border-bottom: none;
            margin-bottom: 0;
        }

        .post-header {
            display: flex;
            align-items: center;
            gap: 1rem;
        }

        .post-user-avatar {
            width: 50px;
            height: 50px;
            border-radius: 50%;
            object-fit: cover;
        }

        .post-user-info {
            flex: 1;
        }

        .post-username {
            font-weight: 600;
            color: var(--dark-color);
            text-decoration: none;
            display: block;
        }

        .post-time {
            font-size: 0.8rem;
            color: var(--gray);
        }

        .post-content {
            margin-left: 60px;
        }

        .post-text {
            margin-bottom: 0.5rem;
        }

        .post-image {
            max-width: 100%;
            max-height: 400px;
            border-radius: 8px;
            object-fit: cover;
        }

        .post-actions {
            display: flex;
            gap: 1rem;
            margin-left: 60px;
        }

        .post-action {
            display: flex;
            align-items: center;
            gap: 0.3rem;
            color: var(--dark-gray);
            cursor: pointer;
            transition: color 0.3s;
        }

        .post-action:hover {
            color: var(--primary-color);
        }

        .post-action.liked {
            color: var(--danger-color);
        }

        #chat-window {
            border: 1px solid #ccc;
            border-radius: 8px;
            padding: 1rem;
            background-color: #f9f9f9;
            height: 500px;
            display: flex;
            flex-direction: column;
        }

        #messages {
            flex: 1;
            overflow-y: auto;
            border: 1px solid #ccc;
            border-radius: 8px;
            margin-bottom: 1rem;
            padding: 0.5rem;
            background-color: var(--white);
            display: flex;
            flex-direction: column;
            gap: 0.5rem;
        }

        .message {
            max-width: 70%;
            padding: 0.5rem 1rem;
            border-radius: 18px;
            word-wrap: break-word;
        }

        .message.sent {
            align-self: flex-end;
            background-color: var(--primary-color);
            color: var(--white);
            border-bottom-right-radius: 4px;
        }

        .message.received {
            align-self: flex-start;
            background-color: #e5e5ea;
            color: var(--dark-color);
            border-bottom-left-radius: 4px;
        }

        .message-sender {
            font-size: 0.8rem;
            font-weight: bold;
            margin-bottom: 0.2rem;
        }

        .chat-input-container {
            display: flex;
            gap: 0.5rem;
        }

        #message-input {
            flex: 1;
            padding: 0.75rem;
            border: 1px solid #ccc;
            border-radius: 4px;
            font-size: 1rem;
        }

        #send-button {
            padding: 0.75rem 1.5rem;
            background-color: var(--primary-color);
            color: var(--white);
            border: none;
            border-radius: 4px;
            cursor: pointer;
            transition: background-color 0.3s;
        }

        #send-button:hover {
            background-color: #357ABD;
        }

        .profile-header {
            display: flex;
            align-items: center;
            gap: 2rem;
            margin-bottom: 2rem;
        }

        .profile-avatar {
            width: 120px;
            height: 120px;
            border-radius: 50%;
            object-fit: cover;
            border: 5px solid var(--white);
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
        }

        .profile-info h1 {
            font-size: 1.8rem;
            margin-bottom: 0.5rem;
            color: var(--dark-color);
        }

        .profile-stats {
            display: flex;
            gap: 1.5rem;
            margin-bottom: 1rem;
        }

        .stat {
            text-align: center;
        }

        .stat-value {
            font-weight: bold;
            font-size: 1.2rem;
        }

        .stat-label {
            font-size: 0.9rem;
            color: var(--gray);
        }

        .profile-bio {
            margin-bottom: 1rem;
        }

        .edit-profile-btn {
            padding: 0.5rem 1rem;
            background-color: var(--primary-color);
            color: var(--white);
            border: none;
            border-radius: 4px;
            font-weight: 600;
            cursor: pointer;
            transition: background-color 0.3s;
        }

        .edit-profile-btn:hover {
            background-color: #357ABD;
        }

        .auth-modal {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.5);
            display: flex;
            justify-content: center;
            align-items: center;
            z-index: 1000;
            opacity: 0;
            visibility: hidden;
            transition: all 0.3s;
        }

        .auth-modal.show {
            opacity: 1;
            visibility: visible;
        }

        .auth-container {
            background-color: var(--white);
            border-radius: 8px;
            width: 100%;
            max-width: 400px;
            padding: 2rem;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
            position: relative;
        }

        .close-modal {
            position: absolute;
            top: 1rem;
            right: 1rem;
            font-size: 1.5rem;
            cursor: pointer;
            color: var(--gray);
        }

        .auth-tabs {
            display: flex;
            margin-bottom: 1.5rem;
            border-bottom: 1px solid #eee;
        }

        .auth-tab {
            padding: 0.5rem 1rem;
            cursor: pointer;
            font-weight: 600;
            color: var(--gray);
            border-bottom: 2px solid transparent;
        }

        .auth-tab.active {
            color: var(--primary-color);
            border-bottom: 2px solid var(--primary-color);
        }

        .auth-form {
            display: flex;
            flex-direction: column;
            gap: 1rem;
        }

        .form-group {
            display: flex;
            flex-direction: column;
            gap: 0.5rem;
        }

        .form-group label {
            font-weight: 600;
            color: var(--dark-gray);
        }

        .form-control {
            padding: 0.75rem;
            border: 1px solid #ccc;
            border-radius: 4px;
            font-size: 1rem;
        }

        .auth-submit {
            padding: 0.75rem;
            background-color: var(--primary-color);
            color: var(--white);
            border: none;
            border-radius: 4px;
            font-weight: 600;
            cursor: pointer;
            transition: background-color 0.3s;
            margin-top: 0.5rem;
        }

        .auth-submit:hover {
            background-color: #357ABD;
        }

        .auth-footer {
            text-align: center;
            margin-top: 1rem;
            color: var(--gray);
        }

        .auth-footer a {
            color: var(--primary-color);
            text-decoration: none;
            font-weight: 600;
        }

        .error-message {
            color: var(--danger-color);
            font-size: 0.9rem;
            margin-top: -0.5rem;
        }

        .success-message {
            color: var(--success-color);
            font-size: 0.9rem;
            margin-top: -0.5rem;
        }

        footer {
            text-align: center;
            padding: 1.5rem;
            background-color: var(--primary-color);
            color: var(--white);
            margin-top: 2rem;
        }

        .hidden {
            display: none !important;
        }

        @media (max-width: 992px) {
            main {
                grid-template-columns: 1fr;
            }
            
            .sidebar {
                position: static;
            }
        }

        @media (max-width: 768px) {
            header {
                flex-direction: column;
                gap: 1rem;
                padding: 1rem;
            }
            
            nav ul {
                flex-wrap: wrap;
                justify-content: center;
            }
            
            nav ul li {
                margin: 0 0.5rem;
            }
            
            .auth-buttons {
                margin-top: 1rem;
            }
        }
    </style>
</head>
<body>
    <header>
        <div class="logo">
            <i class="fas fa-users"></i>
            <span>SocialConnect</span>
        </div>
        <nav>
            <ul>
                <li><a href="#home"><i class="fas fa-home"></i> Home</a></li>
                <li><a href="#chat"><i class="fas fa-comments"></i> Chat</a></li>
                <li><a href="#profile"><i class="fas fa-user"></i> Profile</a></li>
            </ul>
        </nav>
        <div class="auth-buttons" id="authButtons">
            <button class="login-btn" id="loginBtn">Log In</button>
            <button class="signup-btn" id="signupBtn">Sign Up</button>
        </div>
        <div class="user-profile hidden" id="userProfile">
            <img src="https://2024wallepals.simdif.images/public/sd_6745ebe0b2b4f.jpg?no_cache=1732639253" alt="User Avatar" class="user-avatar" id="userAvatar">
            <span id="usernameDisplay">User</span>
            <div class="dropdown-menu" id="dropdownMenu">
                <a href="#profile"><i class="fas fa-user"></i> Profile</a>
                <a href="#" id="logoutBtn"><i class="fas fa-sign-out-alt"></i> Logout</a>
            </div>
        </div>
    </header>
    
    <main>
        <aside class="sidebar">
            <section id="friends">
                <h2><i class="fas fa-user-friends"></i> Friends</h2>
                <div id="friendsList">
                    <div class="friend">
                        <img src="https://via.placeholder.com/40" alt="Friend" class="user-avatar">
                        <span>Friend 1</span>
                    </div>
                    <div class="friend">
                        <img src="https://via.placeholder.com/40" alt="Friend" class="user-avatar">
                        <span>Friend 2</span>
                    </div>
                </div>
            </section>
            
            <section id="trending">
                <h2><i class="fas fa-fire"></i> Trending</h2>
                <div id="trendingList">
                    <div class="trending-item">#SocialMedia</div>
                    <div class="trending-item">#NewApp</div>
                </div>
            </section>
        </aside>
        
        <div class="feed">
            <section id="home" class="active-section">
                <h2><i class="fas fa-home"></i> Home Feed</h2>
                <div class="post-form" id="postForm">
                    <textarea class="post-input" id="postInput" placeholder="What's on your mind?"></textarea>
                    <div class="post-actions">
                        <div class="media-upload">
                            <label for="imageUpload"><i class="fas fa-image"></i></label>
                            <input type="file" id="imageUpload" accept="image/*">
                            <label for="videoUpload"><i class="fas fa-video"></i></label>
                            <input type="file" id="videoUpload" accept="video/*">
                        </div>
                        <button class="post-button" id="postButton">Post</button>
                    </div>
                    <div id="mediaPreview" class="hidden"></div>
                </div>
                
                <div id="postsContainer">
                    <!-- Posts will be loaded here -->
                </div>
            </section>
            
            <section id="chat" class="hidden-section">
                <h2><i class="fas fa-comments"></i> Chat</h2>
                <div id="chat-window">
                    <div id="messages"></div>
                    <div class="chat-input-container">
                        <input type="text" id="message-input" placeholder="Type a message...">
                        <button id="send-button">Send</button>
                    </div>
                </div>
            </section>
            
            <section id="profile" class="hidden-section">
                <div class="profile-header">
                    <img src="https://via.placeholder.com/120" alt="Profile" class="profile-avatar" id="profileAvatar">
                    <div class="profile-info">
                        <h1 id="profileName">User Name</h1>
                        <div class="profile-stats">
                            <div class="stat">
                                <div class="stat-value" id="postCount">0</div>
                                <div class="stat-label">Posts</div>
                            </div>
                            <div class="stat">
                                <div class="stat-value" id="friendCount">0</div>
                                <div class="stat-label">Friends</div>
                            </div>
                            <div class="stat">
                                <div class="stat-value" id="likeCount">0</div>
                                <div class="stat-label">Likes</div>
                            </div>
                        </div>
                        <div class="profile-bio" id="profileBio">This is a sample bio. Click edit to update your profile.</div>
                        <button class="edit-profile-btn" id="editProfileBtn">Edit Profile</button>
                    </div>
                </div>
                
                <h2><i class="fas fa-user-edit"></i> Your Posts</h2>
                <div id="userPosts">
                    <!-- User posts will be loaded here -->
                </div>
            </section>
        </div>
    </main>

    <!-- Auth Modals -->
    <div class="auth-modal" id="authModal">
        <div class="auth-container">
            <span class="close-modal" id="closeModal">&times;</span>
            <div class="auth-tabs">
                <div class="auth-tab active" id="loginTab">Login</div>
                <div class="auth-tab" id="signupTab">Sign Up</div>
            </div>
            
            <form class="auth-form" id="loginForm">
                <div class="form-group">
                    <label for="loginEmail">Email</label>
                    <input type="email" id="loginEmail" class="form-control" required>
                </div>
                <div class="form-group">
                    <label for="loginPassword">Password</label>
                    <input type="password" id="loginPassword" class="form-control" required>
                </div>
                <p class="error-message" id="loginError"></p>
                <button type="submit" class="auth-submit">Log In</button>
                <p class="auth-footer">Don't have an account? <a href="#" id="switchToSignup">Sign up</a></p>
            </form>
            
            <form class="auth-form hidden" id="signupForm">
                <div class="form-group">
                    <label for="signupName">Name</label>
                    <input type="text" id="signupName" class="form-control" required>
                </div>
                <div class="form-group">
                    <label for="signupEmail">Email</label>
                    <input type="email" id="signupEmail" class="form-control" required>
                </div>
                <div class="form-group">
                    <label for="signupPassword">Password</label>
                    <input type="password" id="signupPassword" class="form-control" required>
                </div>
                <div class="form-group">
                    <label for="signupConfirmPassword">Confirm Password</label>
                    <input type="password" id="signupConfirmPassword" class="form-control" required>
                </div>
                <p class="error-message" id="signupError"></p>
                <button type="submit" class="auth-submit">Sign Up</button>
                <p class="auth-footer">Already have an account? <a href="#" id="switchToLogin">Log in</a></p>
            </form>
        </div>
    </div>

    <!-- Edit Profile Modal -->
    <div class="auth-modal" id="editProfileModal">
        <div class="auth-container">
            <span class="close-modal" id="closeEditModal">&times;</span>
            <h2>Edit Profile</h2>
            <form class="auth-form" id="editProfileForm">
                <div class="form-group">
                    <label for="editName">Name</label>
                    <input type="text" id="editName" class="form-control" required>
                </div>
                <div class="form-group">
                    <label for="editBio">Bio</label>
                    <textarea id="editBio" class="form-control" rows="3"></textarea>
                </div>
                <div class="form-group">
                    <label for="editAvatar">Profile Picture</label>
                    <input type="file" id="editAvatar" class="form-control" accept="image/*">
                </div>
                <p class="error-message" id="editProfileError"></p>
                <p class="success-message" id="editProfileSuccess"></p>
                <button type="submit" class="auth-submit">Save Changes</button>
            </form>
        </div>
    </div>

    <footer>
        <p>&copy; 2023 SocialConnect. All rights reserved.</p>
    </footer>

    <script>
        // Initialize Firebase
        const firebaseConfig = {
            apiKey: "AIzaSyBhDzhvIYm_ayEhSy9YtRvkeiXrajZH5q8",
            authDomain: "heoster-class-2024.firebaseapp.com",
            projectId: "heoster-class-2024",
            storageBucket: "heoster-class-2024.appspot.com",
            messagingSenderId: "832744733078",
            appId: "1:832744733078:web:6f1ea8bdaf7acbce5e45b7",
            measurementId: "G-FSX9SZWZP3"
        };

        // Initialize Firebase
    
        const app = firebase.initializeApp(firebaseConfig);
        const auth = firebase.auth();
        const db = firebase.firestore();
        const storage = firebase.storage();

        // DOM Elements
        const authButtons = document.getElementById('authButtons');
        const userProfile = document.getElementById('userProfile');
        const userAvatar = document.getElementById('userAvatar');
        const usernameDisplay = document.getElementById('usernameDisplay');
        const dropdownMenu = document.getElementById('dropdownMenu');
        const logoutBtn = document.getElementById('logoutBtn');
        
        const authModal = document.getElementById('authModal');
        const closeModal = document.getElementById('closeModal');
        const loginBtn = document.getElementById('loginBtn');
        const signupBtn = document.getElementById('signupBtn');
        const loginTab = document.getElementById('loginTab');
        const signupTab = document.getElementById('signupTab');
        const loginForm = document.getElementById('loginForm');
        const signupForm = document.getElementById('signupForm');
        const switchToSignup = document.getElementById('switchToSignup');
        const switchToLogin = document.getElementById('switchToLogin');
        const loginError = document.getElementById('loginError');
        const signupError = document.getElementById('signupError');
        
        const editProfileModal = document.getElementById('editProfileModal');
        const closeEditModal = document.getElementById('closeEditModal');
        const editProfileBtn = document.getElementById('editProfileBtn');
        const editProfileForm = document.getElementById('editProfileForm');
        const editProfileError = document.getElementById('editProfileError');
        const editProfileSuccess = document.getElementById('editProfileSuccess');
        
        const postForm = document.getElementById('postForm');
        const postInput = document.getElementById('postInput');
        const postButton = document.getElementById('postButton');
        const imageUpload = document.getElementById('imageUpload');
        const videoUpload = document.getElementById('videoUpload');
        const mediaPreview = document.getElementById('mediaPreview');
        const postsContainer = document.getElementById('postsContainer');
        
        const chatWindow = document.getElementById('chat-window');
        const messagesDiv = document.getElementById('messages');
        const messageInput = document.getElementById('message-input');
        const sendButton = document.getElementById('send-button');
        
        const profileName = document.getElementById('profileName');
        const profileAvatar = document.getElementById('profileAvatar');
        const profileBio = document.getElementById('profileBio');
        const postCount = document.getElementById('postCount');
        const friendCount = document.getElementById('friendCount');
        const likeCount = document.getElementById('likeCount');
        const userPosts = document.getElementById('userPosts');
        
        const sections = document.querySelectorAll('section');
        const navLinks = document.querySelectorAll('nav a');

        // Global variables
        let currentUser = null;
        let selectedFile = null;

        // Event Listeners
        function initApp() {
            // Event listeners for authentication
            loginBtn.addEventListener('click', showAuthModal);
            signupBtn.addEventListener('click', showAuthModal);
            closeModal.addEventListener('click', hideAuthModal);
            closeEditModal.addEventListener('click', hideEditProfileModal);

            // Tab switching
            loginTab.addEventListener('click', showLoginForm);
            signupTab.addEventListener('click', showSignupForm);
            switchToSignup.addEventListener('click', (e) => {
                e.preventDefault();
                showSignupForm();
            });
            switchToLogin.addEventListener('click', (e) => {
                e.preventDefault();
                showLoginForm();
            });
        

        signupBtn.addEventListener('click', () => {
            showAuthModal();
            showSignupForm();
        });

        closeModal.addEventListener('click', hideAuthModal);
        closeEditModal.addEventListener('click', hideEditProfileModal);

        loginTab.addEventListener('click', showLoginForm);
        signupTab.addEventListener('click', showSignupForm);
        switchToSignup.addEventListener('click', (e) => {
            e.preventDefault();
            showSignupForm();
        });
        switchToLogin.addEventListener('click', (e) => {
            e.preventDefault();
            showLoginForm();
        });

        loginForm.addEventListener('submit', handleLogin);
        signupForm.addEventListener('submit', handleSignup);
        logoutBtn.addEventListener('click', handleLogout);
        

        editProfileBtn.addEventListener('click', showEditProfileModal);
        editProfileForm.addEventListener('submit', handleEditProfile);

        postButton.addEventListener('click', createPost);
        imageUpload.addEventListener('change', handleMediaUpload);
        videoUpload.addEventListener('change', handleMediaUpload);

        sendButton.addEventListener('click', sendMessage);
        messageInput.addEventListener('keypress', (e) => {
            if (e.key === 'Enter') {
                sendMessage();
            }
        });

        userProfile.addEventListener('click', toggleDropdown);

        // Navigation
        navLinks.forEach(link => {
            link.addEventListener('click', (e) => {
                e.preventDefault();
                const sectionId = link.getAttribute('href').substring(1);
                showSection(sectionId);
                
                // Update active nav link
                navLinks.forEach(navLink => navLink.classList.remove('active'));
                link.classList.add('active');
            });
        });

        // Functions
        function showAuthModal() {
            authModal.classList.add('show');
        }

        function hideAuthModal() {
            authModal.classList.remove('show');
            loginError.textContent = '';
            signupError.textContent = '';
        }

        function showLoginForm() {
            loginForm.classList.remove('hidden');
            signupForm.classList.add('hidden');
            loginTab.classList.add('active');
            signupTab.classList.remove('active');
        }

        function showSignupForm() {
            signupForm.classList.remove('hidden');
            loginForm.classList.add('hidden');
            signupTab.classList.add('active');
            loginTab.classList.remove('active');
        }

        function showEditProfileModal() {
            if (!currentUser) return;
            
            // Fill form with current user data
            db.collection('users').doc(currentUser.uid).get()
                .then(doc => {
                    if (doc.exists) {
                        const userData = doc.data();
                        document.getElementById('editName').value = userData.name || '';
                        document.getElementById('editBio').value = userData.bio || '';
                    }
                });
            
            editProfileModal.classList.add('show');
        }

        function hideEditProfileModal() {
            editProfileModal.classList.remove('show');
            editProfileError.textContent = '';
            editProfileSuccess.textContent = '';
        }

        function toggleDropdown(e) {
            e.stopPropagation();
            dropdownMenu.classList.toggle('show');
        }

        function showSection(sectionId) {
            sections.forEach(section => {
                if (section.id === sectionId) {
                    section.classList.remove('hidden-section');
                    section.classList.add('active-section');
                } else {
                    section.classList.add('hidden-section');
                    section.classList.remove('active-section');
                }
            });
            
            // Load content for the section
            if (sectionId === 'home') {
                loadPosts();
            } else if (sectionId === 'profile') {
                loadProfile();
            }
        }

        // Auth Functions
        function handleLogin(e) {
            e.preventDefault();
            const email = document.getElementById('loginEmail').value;
            const password = document.getElementById('loginPassword').value;
            
            auth.signInWithEmailAndPassword(email, password)
                .then((userCredential) => {
                    currentUser = userCredential.user;
                    hideAuthModal();
                    updateUI();
                    loadPosts();
                })
                .catch((error) => {
                    loginError.textContent = error.message;
                });
        }

        function handleSignup(e) {
            e.preventDefault();
            const name = document.getElementById('signupName').value;
            const email = document.getElementById('signupEmail').value;
            const password = document.getElementById('signupPassword').value;
            const confirmPassword = document.getElementById('signupConfirmPassword').value;
            
            if (password !== confirmPassword) {
                signupError.textContent = 'Passwords do not match';
                return;
            }
            
            auth.createUserWithEmailAndPassword(email, password)
                .then((userCredential) => {
                    currentUser = userCredential.user;
                    
                    // Save additional user data to Firestore
                    return db.collection('users').doc(currentUser.uid).set({
                        name: name,
                        email: email,
                        bio: '',
                        createdAt: firebase.firestore.FieldValue.serverTimestamp()
                    });
                })
                .then(() => {
                    hideAuthModal();
                    updateUI();
                    loadPosts();
                })
                .catch((error) => {
                    signupError.textContent = error.message;
                });
        }

        function handleLogout() {
            auth.signOut().then(() => {
                currentUser = null;
                updateUI();
                showSection('home');
            });
        }

        function updateUI() {
            if (currentUser) {
                authButtons.classList.add('hidden');
                userProfile.classList.remove('hidden');
                
                // Load user data
                db.collection('users').doc(currentUser.uid).get()
                    .then(doc => {
                        if (doc.exists) {
                            const userData = doc.data();
                            usernameDisplay.textContent = userData.name;
                            
                            // Set avatar if exists
                            if (userData.avatar) {
                                userAvatar.src = userData.avatar;
                            }
                        }
                    });
            } else {
                authButtons.classList.remove('hidden');
                userProfile.classList.add('hidden');
                postsContainer.innerHTML = '';
                userPosts.innerHTML = '';
            }
        }

        // Post Functions
        function createPost() {
            if (!currentUser) {
                alert('Please log in to create a post');
                return;
            }
            
            const postText = postInput.value.trim();
            if (!postText && !selectedFile) return;
            
            const postData = {
                text: postText,
                userId: currentUser.uid,
                createdAt: firebase.firestore.FieldValue.serverTimestamp(),
                likes: 0,
                likedBy: []
            };
            
            let uploadPromise = Promise.resolve(null);
            
            if (selectedFile) {
                const fileType = selectedFile.type.split('/')[0]; // 'image' or 'video'
                const storageRef = storage.ref(`posts/${currentUser.uid}/${Date.now()}_${selectedFile.name}`);
                uploadPromise = storageRef.put(selectedFile)
                    .then(snapshot => snapshot.ref.getDownloadURL())
                    .then(url => {
                        postData.mediaUrl = url;
                        postData.mediaType = fileType;
                        return url;
                    });
            }
            
            uploadPromise.then(() => {
                return db.collection('posts').add(postData);
            })
            .then(() => {
                postInput.value = '';
                mediaPreview.innerHTML = '';
                mediaPreview.classList.add('hidden');
                selectedFile = null;
                loadPosts();
            })
            .catch(error => {
                console.error('Error creating post:', error);
            });
        }

        function handleMediaUpload(e) {
            const file = e.target.files[0];
            if (!file) return;
            
            selectedFile = file;
            mediaPreview.innerHTML = '';
            mediaPreview.classList.remove('hidden');
            
            const fileType = file.type.split('/')[0]; // 'image' or 'video'
            const reader = new FileReader();
            
            reader.onload = function(event) {
                if (fileType === 'image') {
                    const img = document.createElement('img');
                    img.src = event.target.result;
                    img.style.maxWidth = '100%';
                    img.style.maxHeight = '200px';
                    mediaPreview.appendChild(img);
                } else if (fileType === 'video') {
                    const video = document.createElement('video');
                    video.src = event.target.result;
                    video.controls = true;
                    video.style.maxWidth = '100%';
                    video.style.maxHeight = '200px';
                    mediaPreview.appendChild(video);
                }
            };
            
            reader.readAsDataURL(file);
        }

        function loadPosts() {
            if (!currentUser) return;
            
            postsContainer.innerHTML = '';
            
            db.collection('posts').orderBy('createdAt', 'desc').limit(20)
                .onSnapshot(snapshot => {
                    snapshot.docChanges().forEach(change => {
                        if (change.type === 'added') {
                            displayPost(change.doc, postsContainer);
                        }
                    });
                });
        }

        function displayPost(doc, container) {
            const post = doc.data();
            const postId = doc.id;
            
            // Get user data
            db.collection('users').doc(post.userId).get()
                .then(userDoc => {
                    const userData = userDoc.data();
                    
                    const postElement = document.createElement('div');
                    postElement.className = 'post';
                    postElement.dataset.id = postId;
                    
                    let mediaHtml = '';
                    if (post.mediaUrl) {
                        if (post.mediaType === 'image') {
                            mediaHtml = `<img src="${post.mediaUrl}" class="post-image" alt="Post image">`;
                        } else if (post.mediaType === 'video') {
                            mediaHtml = `<video src="${post.mediaUrl}" class="post-image" controls></video>`;
                        }
                    }
                    
                    const isLiked = post.likedBy && post.likedBy.includes(currentUser.uid);
                    
                    postElement.innerHTML = `
                        <div class="post-header">
                            <img src="${userData.avatar || 'https://via.placeholder.com/50'}" class="post-user-avatar" alt="${userData.name}">
                            <div class="post-user-info">
                                <a href="#" class="post-username">${userData.name}</a>
                                <div class="post-time">${formatDate(post.createdAt)}</div>
                            </div>
                        </div>
                        <div class="post-content">
                            <p class="post-text">${post.text}</p>
                            ${mediaHtml}
                            <div class="post-actions">
                                <div class="post-action ${isLiked ? 'liked' : ''}" data-action="like">
                                    <i class="fas fa-heart"></i>
                                    <span>${post.likes || 0}</span>
                                </div>
                                <div class="post-action" data-action="comment">
                                    <i class="fas fa-comment"></i>
                                    <span>0</span>
                                </div>
                                <div class="post-action" data-action="share">
                                    <i class="fas fa-share"></i>
                                </div>
                            </div>
                        </div>
                    `;
                    
                    container.appendChild(postElement);
                    
                    // Add event listeners for actions
                    const likeButton = postElement.querySelector('[data-action="like"]');
                    if (likeButton) {
                        likeButton.addEventListener('click', () => toggleLike(postId, post, likeButton));
                    }
                });
        }

        function toggleLike(postId, post, likeButton) {
            if (!currentUser) return;
            
            const isLiked = post.likedBy && post.likedBy.includes(currentUser.uid);
            const newLikedBy = isLiked 
                ? post.likedBy.filter(id => id !== currentUser.uid) 
                : [...(post.likedBy || []), currentUser.uid];
            
            const newLikes = isLiked ? (post.likes - 1) : (post.likes + 1);
            
            db.collection('posts').doc(postId).update({
                likes: newLikes,
                likedBy: newLikedBy
            })
            .then(() => {
                likeButton.classList.toggle('liked');
                likeButton.querySelector('span').textContent = newLikes;
            })
            .catch(error => {
                console.error('Error updating like:', error);
            });
        }

        // Chat Functions
        function sendMessage() {
            const message = messageInput.value.trim();
            if (!message || !currentUser) return;
            
            db.collection('messages').add({
                text: message,
                userId: currentUser.uid,
                timestamp: firebase.firestore.FieldValue.serverTimestamp()
            })
            .then(() => {
                messageInput.value = '';
            })
            .catch(error => {
                console.error('Error sending message:', error);
            });
        }

        function loadMessages() {
            messagesDiv.innerHTML = '';
            
            db.collection('messages').orderBy('timestamp').limit(50)
                .onSnapshot(snapshot => {
                    snapshot.docChanges().forEach(change => {
                        if (change.type === 'added') {
                            displayMessage(change.doc);
                        }
                    });
                    
                    // Scroll to bottom
                    messagesDiv.scrollTop = messagesDiv.scrollHeight;
                });
        }

        function displayMessage(doc) {
            const message = doc.data();
            
            // Get user data
            db.collection('users').doc(message.userId).get()
                .then(userDoc => {
                    const userData = userDoc.data();
                    const isCurrentUser = message.userId === currentUser.uid;
                    
                    const messageElement = document.createElement('div');
                    messageElement.className = `message ${isCurrentUser ? 'sent' : 'received'}`;
                    
                    messageElement.innerHTML = `
                        ${!isCurrentUser ? `<div class="message-sender">${userData.name}</div>` : ''}
                        <div>${message.text}</div>
                    `;
                    
                    messagesDiv.appendChild(messageElement);
                });
        }

        // Profile Functions
        function loadProfile() {
            if (!currentUser) return;
            
            userPosts.innerHTML = '';
            
            // Load user data
            db.collection('users').doc(currentUser.uid).get()
                .then(doc => {
                    if (doc.exists) {
                        const userData = doc.data();
                        profileName.textContent = userData.name;
                        profileBio.textContent = userData.bio || 'No bio yet.';
                        
                        if (userData.avatar) {
                            profileAvatar.src = userData.avatar;
                        }
                    }
                });
            
            // Load user stats
            db.collection('posts').where('userId', '==', currentUser.uid).get()
                .then(snapshot => {
                    postCount.textContent = snapshot.size;
                });
            
            // Load user posts
            db.collection('posts').where('userId', '==', currentUser.uid).orderBy('createdAt', 'desc')
                .onSnapshot(snapshot => {
                    snapshot.docChanges().forEach(change => {
                        if (change.type === 'added') {
                            displayPost(change.doc, userPosts);
                        }
                    });
                });
        }

        function handleEditProfile(e) {
            e.preventDefault();
            const name = document.getElementById('editName').value;
            const bio = document.getElementById('editBio').value;
            const avatarFile = document.getElementById('editAvatar').files[0];
            
            const updates = {
                name: name,
                bio: bio
            };
            
            let uploadPromise = Promise.resolve(null);
            
            if (avatarFile) {
                const storageRef = storage.ref(`avatars/${currentUser.uid}`);
                uploadPromise = storageRef.put(avatarFile)
                    .then(snapshot => snapshot.ref.getDownloadURL())
                    .then(url => {
                        updates.avatar = url;
                        return url;
                    });
            }
            
            uploadPromise.then(() => {
                return db.collection('users').doc(currentUser.uid).update(updates);
            })
            .then(() => {
                editProfileSuccess.textContent = 'Profile updated successfully!';
                setTimeout(hideEditProfileModal, 1500);
                updateUI();
                loadProfile();
            })
            .catch(error => {
                editProfileError.textContent = error.message;
            });
        }

        // Helper Functions
        function formatDate(timestamp) {
            if (!timestamp) return 'Just now';
            
            const date = timestamp.toDate();
            const now = new Date();
            const diff = now - date;
            
            const seconds = Math.floor(diff / 1000);
            const minutes = Math.floor(seconds / 60);
            const hours = Math.floor(minutes / 60);
            const days = Math.floor(hours / 24);
            
            if (days > 0) return `${days}d ago`;
            if (hours > 0) return `${hours}h ago`;
            if (minutes > 0) return `${minutes}m ago`;
            return 'Just now';
        }

        // Close dropdown when clicking outside
        document.addEventListener('click', () => {
            dropdownMenu.classList.remove('show');
        });

        // Auth State Listener
        auth.onAuthStateChanged(user => {
            currentUser = user;
            updateUI();
            
            if (user) {
                loadPosts();
                loadMessages();
            }
        });

        // Initialize
        showSection('home');
        navLinks[0].classList.add('active');
    </script>
</body>
</html>
