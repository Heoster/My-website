<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Happy Birthday Heoster!</title>
  <style>
    @keyframes fadeIn {
      0% { opacity: 0; transform: translateY(-20px); }
      100% { opacity: 1; transform: translateY(0); }
    }
    @keyframes glow {
      0% { box-shadow: 0 0 5px #ff6ec4; }
      50% { box-shadow: 0 0 20px #ff6ec4; }
      100% { box-shadow: 0 0 5px #ff6ec4; }
    }
    @keyframes float {
      0% { transform: translateY(0px); }
      50% { transform: translateY(-15px); }
      100% { transform: translateY(0px); }
    }
    
    body {
      margin: 0;
      padding: 0;
      font-family: 'Segoe UI', sans-serif;
      /* Party background image from Unsplash */
      background: url('https://images.unsplash.com/photo-1492684223066-81342ee5ff30?auto=format&fit=crop&w=1950&q=80') no-repeat center center fixed;
      background-size: cover;
      color: #fff;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      height: 100vh;
      text-align: center;
      overflow: hidden;
      animation: fadeIn 1.5s ease-in-out;
      position: relative;
    }
    
    /* Semi-transparent overlay for readability */
    body::before {
      content: '';
      position: absolute;
      top: 0; left: 0;
      width: 100%;
      height: 100%;
      background: rgba(0, 0, 0, 0.5);
      z-index: 0;
    }
    
    /* Updated container style using glassmorphism */
    .party-container {
      position: relative;
      z-index: 1;
      background: rgba(255, 255, 255, 0.1);
      backdrop-filter: blur(10px);
      border: 1px solid rgba(255, 255, 255, 0.2);
      border-radius: 15px;
      box-shadow: 0 4px 30px rgba(0, 0, 0, 0.5);
      padding: 2em;
      width: 90%;
      max-width: 500px;
      margin: 20px;
      animation: fadeIn 2s ease-in-out;
    }
    
    h1 {
      font-size: 2.5em;
      margin-bottom: 0.3em;
      text-shadow: 0 0 10px #ff6ec4, 0 0 20px #ff6ec4;
      animation: glow 2s infinite, float 3s ease-in-out infinite;
    }
    
    p {
      font-size: 1.2em;
      margin-bottom: 1em;
      text-shadow: 0 0 5px #00bcd4;
    }
    
    .input-group {
      margin-bottom: 1em;
    }
    
    input[type="text"] {
      padding: 10px;
      width: 70%;
      border: none;
      border-radius: 5px;
      margin-right: 5px;
      font-size: 1em;
    }
    
    button {
      padding: 10px 15px;
      font-size: 1em;
      border: none;
      border-radius: 5px;
      background-color: #ff6ec4;
      color: #000;
      cursor: pointer;
      transition: background-color 0.3s, transform 0.3s;
      box-shadow: 0 0 10px #ff6ec4;
    }
    
    button:hover {
      background-color: #e055a4;
      transform: scale(1.05);
    }
    
    #visitor-message {
      margin-top: 0.5em;
      font-style: italic;
      font-size: 1.1em;
    }
    
    #user-list {
      margin-top: 1.5em;
      padding: 1em;
      background: rgba(255, 255, 255, 0.1);
      border-radius: 5px;
      max-height: 150px;
      overflow-y: auto;
      text-align: left;
      font-size: 1em;
      line-height: 1.4em;
      box-shadow: inset 0 0 10px #00bcd4;
    }
    
    /* Scrollbar styling */
    #user-list::-webkit-scrollbar {
      width: 6px;
    }
    
    #user-list::-webkit-scrollbar-thumb {
      background: #00bcd4;
      border-radius: 3px;
    }
    
    /* Animated party elements */
    .balloon {
      position: absolute;
      bottom: -100px;
      width: 50px;
      height: 70px;
      background: radial-gradient(circle, #ff6ec4, #e055a4);
      border-radius: 50%;
      animation: floatUp 8s linear infinite;
      opacity: 0.9;
      z-index: 0;
    }
    
    @keyframes floatUp {
      0% { transform: translateX(0) translateY(0); opacity: 0.9; }
      50% { opacity: 1; }
      100% { transform: translateX(100px) translateY(-120vh); opacity: 0; }
    }
  </style>
</head>
<body>
  <div class="party-container">
    <h1>Happy Birthday Heoster!</h1>
    <p>Welcome to the ultimate birthday party!</p>
    
    <div class="input-group">
      <input type="text" id="nameInput" placeholder="Enter your name...">
      <button id="saveBtn">Join</button>
    </div>
    
    <div id="visitor-message"></div>
    <div id="user-list"></div>
  </div>
  
  <!-- Animated Balloons -->
  <div class="balloon" style="left: 10%; animation-delay: 0s;"></div>
  <div class="balloon" style="left: 40%; animation-delay: 2s;"></div>
  <div class="balloon" style="left: 70%; animation-delay: 4s;"></div>
  
  <script>
    // Update guest list from localStorage
    const saveBtn = document.getElementById('saveBtn');
    const visitorMsg = document.getElementById('visitor-message');
    const userListDiv = document.getElementById('user-list');
    
    function updateUserList() {
      const userList = JSON.parse(localStorage.getItem('userList') || '[]');
      userListDiv.innerHTML = '<strong>Guests Joined:</strong><br>' + 
        userList.map(user => `- ${user}`).join('<br>');
    }
    
    saveBtn.addEventListener('click', () => {
      const nameInput = document.getElementById('nameInput');
      const name = nameInput.value.trim();
      
      if (name !== '') {
        localStorage.setItem('visitorName', name);
        visitorMsg.textContent = `Welcome to the party, ${name}!`;
        
        const userList = JSON.parse(localStorage.getItem('userList') || '[]');
        if (!userList.includes(name)) {
          userList.push(name);
          localStorage.setItem('userList', JSON.stringify(userList));
        }
        updateUserList();
        nameInput.value = '';
      } else {
        visitorMsg.textContent = 'Please enter a name to join the party!';
      }
    });
    
    window.onload = () => {
      const savedName = localStorage.getItem('visitorName');
      if (savedName) {
        document.getElementById('visitor-message').textContent = `Welcome back, ${savedName}!`;
      }
      updateUserList();
    };
  </script>
</body>
</html>
