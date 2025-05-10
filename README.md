
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Muslim Face</title>
  <style>
    * { box-sizing: border-box; }
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      background: #f0f2f5;
    }
    header {
      background: #1877f2;
      color: white;
      padding: 10px 20px;
      display: flex;
      flex-wrap: wrap;
      justify-content: space-between;
      align-items: center;
    }
    .logo { font-size: 24px; font-weight: bold; }
    .container {
      width: 95%;
      max-width: 600px;
      margin: 20px auto;
      background: white;
      padding: 20px;
      border-radius: 8px;
      box-shadow: 0 0 10px rgba(0,0,0,0.1);
    }
    .post { border-bottom: 1px solid #ddd; padding: 10px 0; }
    .post:last-child { border-bottom: none; }
    .post-user {
      font-weight: bold;
      color: #1877f2;
      cursor: pointer;
    }
    .post-text { margin-top: 5px; }
    .new-post { margin-bottom: 20px; }
    textarea, input[type="text"], input[type="file"] {
      width: 100%; padding: 10px; margin: 10px 0;
      border: 1px solid #ccc; border-radius: 5px;
    }
    button {
      background: #1877f2; color: white; border: none;
      padding: 10px 15px; border-radius: 5px; margin-top: 10px;
      cursor: pointer;
    }
    .login-box {
      width: 90%; max-width: 300px;
      margin: 50px auto;
      background: white; padding: 20px;
      border-radius: 8px;
      box-shadow: 0 0 10px rgba(0,0,0,0.1);
      text-align: center;
    }
    .comments { margin-top: 10px; padding-left: 20px; }
    .comment {
      border-left: 2px solid #ddd;
      padding-left: 10px; margin-bottom: 5px;
      font-size: 14px;
    }
    .comment-form {
      display: flex; flex-wrap: wrap; gap: 10px; margin-top: 5px;
    }
    .comment-form input {
      flex: 1; padding: 5px;
      border: 1px solid #ccc; border-radius: 5px;
    }
    .like-button {
      color: #1877f2; cursor: pointer; margin-top: 5px; font-size: 14px;
    }
    .post-image {
      margin-top: 10px; max-width: 100%; border-radius: 5px;
    }
    #profilePage {
      display: none;
      width: 95%; max-width: 600px; margin: 20px auto;
      background: white; padding: 20px;
      border-radius: 8px; box-shadow: 0 0 10px rgba(0,0,0,0.1);
    }
    #chatBox {
      position: fixed;
      bottom: 20px;
      right: 20px;
      width: 300px;
      height: 400px;
      background: white;
      box-shadow: 0 0 15px rgba(0, 0, 0, 0.2);
      border-radius: 8px;
      padding: 10px;
      display: none;
    }
    .chat-header {
      font-weight: bold;
      margin-bottom: 10px;
    }
    .chat-messages {
      height: 300px;
      overflow-y: auto;
      margin-bottom: 10px;
    }
    .chat-messages div {
      margin-bottom: 5px;
    }
    .chat-input {
      display: flex;
      gap: 10px;
    }
    .chat-input input {
      flex: 1;
      padding: 8px;
      border: 1px solid #ccc;
      border-radius: 5px;
    }
    #chatButton {
      position: fixed;
      bottom: 20px;
      left: 20px;
      background: #1877f2;
      color: white;
      padding: 10px 20px;
      border-radius: 5px;
      cursor: pointer;
    }
    @media (max-width: 480px) {
      .logo { font-size: 20px; }
      .comment-form { flex-direction: column; }
      button { width: 100%; }
    }
  </style>
</head><script type="module">
  // Import the functions you need from the SDKs you need
  import { initializeApp } from "https://www.gstatic.com/firebasejs/11.7.1/firebase-app.js";
  import { getAnalytics } from "https://www.gstatic.com/firebasejs/11.7.1/firebase-analytics.js";
  // TODO: Add SDKs for Firebase products that you want to use
  // https://firebase.google.com/docs/web/setup#available-libraries

  // Your web app's Firebase configuration
  // For Firebase JS SDK v7.20.0 and later, measurementId is optional
  const firebaseConfig = {
    apiKey: "AIzaSyC5ZVULOoUIuDIVOr3jTJUBDaTgr9-VIaI",
    authDomain: "muslimfaceauth.firebaseapp.com",
    projectId: "muslimfaceauth",
    storageBucket: "muslimfaceauth.firebasestorage.app",
    messagingSenderId: "348506530725",
    appId: "1:348506530725:web:5c12c54891fd4c959a3e4c",
    measurementId: "G-NCSBJN9Z1K"
  };

  // Initialize Firebase
  const app = initializeApp(firebaseConfig);
  const analytics = getAnalytics(app);
</script>
<body>
  <div class="login-box" id="loginBox">
    <h2>Login</h2>
    <input type="text" id="username" placeholder="Enter your name" />
    <button onclick="login()">Login</button>
  </div>
  
  <div id="mainContent" style="display: none;">
    <header>
      <div class="logo">Muslim-Face</div>
      <div id="welcomeUser">Welcome</div>
    </header>

    <div class="container">
      <div class="new-post">
        <textarea id="newPostText" rows="3" placeholder="What's on your mind?"></textarea>
        <input type="file" id="postImage" accept="image/*">
        <button onclick="addPost()">Post</button>
      </div>

      <div id="posts"></div>
    </div>
  </div>

  <div id="profilePage">
    <h2 id="profileName">User Profile</h2>
    <button onclick="goBack()">Back</button>
    <div id="userPosts"></div>
  </div>

  <div id="chatButton" onclick="toggleChat()">Chat</div>

  <div id="chatBox">
    <div class="chat-header">Chat with <span id="chatUser"></span></div>
    <div class="chat-messages" id="chatMessages"></div>
    <div class="chat-input">
      <input type="text" id="chatInput" placeholder="Type a message..." />
      <button onclick="sendMessage()">Send</button>
    </div>
  </div>

  <script>
    let allPosts = [];
    let chatMessages = [];
    let chatWithUser = null;

    function login() {
      const username = document.getElementById("username").value;
      if (username.trim() !== "") {
        document.getElementById("loginBox").style.display = "none";
        document.getElementById("mainContent").style.display = "block";
        document.getElementById("welcomeUser").innerText = `Welcome, ${username}`;
        window.currentUser = username;
      }
    }

    function addPost() {
      const text = document.getElementById("newPostText").value;
      const file = document.getElementById("postImage").files[0];

      if (text.trim() !== "" || file) {
        const postId = "post" + Date.now();
        let reader = new FileReader();

        reader.onload = function(e) {
          const image = file ? e.target.result : "";
          const post = { id: postId, user: window.currentUser, text, image, likes: 0, comments: [] };
          allPosts.unshift(post);
          renderPosts();
        };

        if (file) reader.readAsDataURL(file);
        else {
          const post = { id: postId, user: window.currentUser, text, image: "", likes: 0, comments: [] };
          allPosts.unshift(post);
          renderPosts();
        }

        document.getElementById("newPostText").value = "";
        document.getElementById("postImage").value = "";
      }
    }

    function renderPosts(posts = allPosts, containerId = "posts") {
      const container = document.getElementById(containerId);
      container.innerHTML = "";
      for (let post of posts) {
        const commentsHTML = post.comments.map(c => `<div class='comment'><strong>${c.user}</strong>: ${c.text}</div>`).join('');
        const postHTML = `
          <div class="post">
            <div class="post-user" onclick="viewProfile('${post.user}')">${post.user}</div>
            <div class="post-text">${post.text}</div>
            ${post.image ? `<img src="${post.image}" class="post-image" />` : ''}
            <div class="like-button" onclick="likePost('${post.id}')">${post.likes} Likes</div>
            <div class="comments">${commentsHTML}</div>
            <div class="comment-form">
              <input type="text" placeholder="Add a comment..." id="comment-${post.id}">
              <button onclick="addComment('${post.id}')">Comment</button>
            </div>
          </div>
        `;
        container.innerHTML += postHTML;
      }
    }

    function likePost(postId) {
      const post = allPosts.find(p => p.id === postId);
      if (post) {
        post.likes++;
        renderPosts();
      }
    }

    function addComment(postId) {
      const commentText = document.getElementById(`comment-${postId}`).value;
      if (commentText.trim() !== "") {
        const post = allPosts.find(p => p.id === postId);
        if (post) {
          post.comments.push({ user: window.currentUser, text: commentText });
          renderPosts();
        }
      }
    }

    function viewProfile(user) {
      const userPosts = allPosts.filter(post => post.user === user);
      document.getElementById("profileName").innerText = `${user}'s Profile`;
      renderPosts(userPosts, "userPosts");
      document.getElementById("profilePage").style.display = "block";
      document.getElementById("mainContent").style.display = "none";
    }

    function goBack() {
      document.getElementById("profilePage").style.display = "none";
      document.getElementById("mainContent").style.display = "block";
    }

    function toggleChat() {
      const chatBox = document.getElementById("chatBox");
      if (chatBox.style.display === "none" || chatBox.style.display === "") {
        chatBox.style.display = "block";
      } else {
        chatBox.style.display = "none";
      }
    }

    function sendMessage() {
      const message = document.getElementById("chatInput").value;
      if (message.trim() !== "") {
        chatMessages.push({ user: window.currentUser, message });
        document.getElementById("chatInput").value = "";
        renderChatMessages();
      }
    }

    function renderChatMessages() {
      const chatMessagesContainer = document.getElementById("chatMessages");
      chatMessagesContainer.innerHTML = chatMessages.map(m => `<div><strong>${m.user}:</strong> ${m.message}</div>`).join('');
    }
  </script>
</body>
</html>
