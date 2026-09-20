<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Chugli Gang</title>
  <!-- FontAwesome Icons for Instagram-like UI -->
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css" />
  <style>
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
    }

    body {
      background-color: #fafafa;
      display: flex;
      justify-content: center;
      align-items: center;
      min-height: 100vh;
    }

    /* Screen Container */
    .app-container {
      width: 100%;
      max-width: 450px;
      height: 100vh;
      max-height: 850px;
      background: #ffffff;
      border: 1px solid #dbdbdb;
      display: flex;
      flex-direction: column;
      position: relative;
      box-shadow: 0 4px 12px rgba(0,0,0,0.1);
    }

    /* Login View */
    #login-view {
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      height: 100%;
      padding: 30px;
      text-align: center;
    }

    .brand-header {
      font-size: 32px;
      font-weight: 700;
      background: linear-gradient(45deg, #f09433 0%, #e6683c 25%, #dc2743 50%, #cc2366 75%, #bc1888 100%);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      margin-bottom: 4px;
    }

    .sub-heading {
      font-size: 12px;
      color: #8e8e8e;
      margin-bottom: 30px;
      font-weight: 500;
    }

    .login-form input {
      width: 100%;
      padding: 12px;
      margin-bottom: 12px;
      border: 1px solid #dbdbdb;
      border-radius: 6px;
      background: #fafafa;
      font-size: 14px;
    }

    .login-form button {
      width: 100%;
      padding: 12px;
      background-color: #0095f6;
      border: none;
      color: white;
      font-weight: 600;
      border-radius: 6px;
      cursor: pointer;
      font-size: 14px;
    }

    .login-form button:hover {
      background-color: #1877f2;
    }

    .error-msg {
      color: #ed4956;
      font-size: 12px;
      margin-top: 10px;
      display: none;
    }

    /* App View */
    #app-view {
      display: none;
      flex-direction: column;
      height: 100%;
    }

    /* Top Bar */
    .top-bar {
      height: 60px;
      border-bottom: 1px solid #dbdbdb;
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: 0 16px;
      background: #fff;
    }

    .top-bar h2 {
      font-size: 20px;
      font-weight: 600;
    }

    /* Tab Controls */
    .chat-tabs {
      display: flex;
      border-bottom: 1px solid #dbdbdb;
      background: #fafafa;
    }

    .tab-btn {
      flex: 1;
      padding: 12px;
      border: none;
      background: none;
      font-weight: 600;
      color: #8e8e8e;
      cursor: pointer;
    }

    .tab-btn.active {
      color: #262626;
      border-bottom: 2px solid #262626;
      background: #fff;
    }

    /* Message Area */
    .messages-container {
      flex: 1;
      overflow-y: auto;
      padding: 16px;
      display: flex;
      flex-direction: column;
      gap: 12px;
      background-color: #fff;
    }

    .message {
      max-width: 75%;
      padding: 10px 14px;
      border-radius: 18px;
      font-size: 14px;
      line-height: 1.4;
      position: relative;
    }

    .message.incoming {
      align-self: flex-start;
      background-color: #efefef;
      color: #000;
      border-bottom-left-radius: 4px;
    }

    .message.outgoing {
      align-self: flex-end;
      background: linear-gradient(45deg, #377fff, #1877f2);
      color: #fff;
      border-bottom-right-radius: 4px;
    }

    .sender-name {
      font-size: 10px;
      font-weight: 700;
      margin-bottom: 2px;
      opacity: 0.7;
    }

    .dm-selector {
      padding: 8px 16px;
      border-bottom: 1px solid #efefef;
      display: none;
    }

    .dm-selector select {
      width: 100%;
      padding: 6px;
      border-radius: 4px;
      border: 1px solid #dbdbdb;
    }

    /* Input Bar */
    .input-bar {
      padding: 12px 16px;
      border-top: 1px solid #dbdbdb;
      display: flex;
      align-items: center;
      gap: 10px;
      background: #fff;
    }

    .input-bar input {
      flex: 1;
      padding: 10px 16px;
      border: 1px solid #dbdbdb;
      border-radius: 22px;
      outline: none;
      font-size: 14px;
    }

    .icon-btn {
      background: none;
      border: none;
      font-size: 20px;
      color: #0095f6;
      cursor: pointer;
    }

    .icon-btn.recording {
      color: #ed4956;
      animation: pulse 1s infinite;
    }

    @keyframes pulse {
      0% { transform: scale(1); }
      50% { transform: scale(1.2); }
      100% { transform: scale(1); }
    }
  </style>
</head>
<body>

<div class="app-container">

  <!-- LOGIN PAGE -->
  <div id="login-view">
    <div class="brand-header">Chugli Gang</div>
    <div class="sub-heading">made by armaan</div>

    <form class="login-form" onsubmit="handleLogin(event)">
      <input type="text" id="username" placeholder="Username (Your Name)" required />
      <input type="password" id="access-code" placeholder="Passcode (162012)" required />
      <button type="submit">Log In</button>
      <div id="login-error" class="error-msg">Invalid passcode. Try 162012.</div>
    </form>
  </div>

  <!-- CHAT MAIN APP -->
  <div id="app-view">
    <div class="top-bar">
      <h2 class="brand-header" style="font-size: 22px; margin: 0;">Chugli Gang</h2>
      <i class="fa-solid fa-right-from-bracket icon-btn" style="color: #262626;" onclick="logout()"></i>
    </div>

    <div class="chat-tabs">
      <button class="tab-btn active" id="tab-public" onclick="switchTab('public')">Public Group</button>
      <button class="tab-btn" id="tab-private" onclick="switchTab('private')">Private DM</button>
    </div>

    <!-- Private DM Target Selection -->
    <div class="dm-selector" id="dm-selector">
      <select id="dm-target" onchange="loadPrivateMessages()">
        <option value="Family Member 1">Family Member 1</option>
        <option value="Family Member 2">Family Member 2</option>
        <option value="Family Member 3">Family Member 3</option>
      </select>
    </div>

    <div class="messages-container" id="messages"></div>

    <div class="input-bar">
      <button class="icon-btn" id="mic-btn" onclick="toggleRecording()">
        <i class="fa-solid fa-microphone"></i>
      </button>
      <input type="text" id="message-input" placeholder="Message..." onkeypress="handleKeyPress(event)" />
      <button class="icon-btn" onclick="sendMessage()">
        <i class="fa-solid fa-paper-plane"></i>
      </button>
    </div>
  </div>

</div>

<script>
  let currentUser = '';
  let activeTab = 'public';
  let mediaRecorder;
  let audioChunks = [];
  let isRecording = false;

  // Check LocalStorage Session
  window.onload = function() {
    const savedUser = localStorage.getItem('chugli_user');
    if (savedUser) {
      currentUser = savedUser;
      showApp();
    }
  };

  function handleLogin(e) {
    e.preventDefault();
    const user = document.getElementById('username').value.trim();
    const code = document.getElementById('access-code').value.trim();
    const errorMsg = document.getElementById('login-error');

    if (code === '162012' && user !== '') {
      currentUser = user;
      localStorage.setItem('chugli_user', user);
      errorMsg.style.display = 'none';
      showApp();
    } else {
      errorMsg.style.display = 'block';
    }
  }

  function logout() {
    localStorage.removeItem('chugli_user');
    document.getElementById('app-view').style.display = 'none';
    document.getElementById('login-view').style.display = 'flex';
  }

  function showApp() {
    document.getElementById('login-view').style.display = 'none';
    document.getElementById('app-view').style.display = 'flex';
    renderMessages();
  }

  function switchTab(tab) {
    activeTab = tab;
    document.getElementById('tab-public').classList.toggle('active', tab === 'public');
    document.getElementById('tab-private').classList.toggle('active', tab === 'private');
    document.getElementById('dm-selector').style.display = tab === 'private' ? 'block' : 'none';
    renderMessages();
  }

  function handleKeyPress(e) {
    if (e.key === 'Enter') sendMessage();
  }

  // Local Storage Message Handlers
  function getStoredMessages() {
    return JSON.parse(localStorage.getItem('chugli_messages') || '[]');
  }

  function saveMessage(msgObj) {
    const msgs = getStoredMessages();
    msgs.push(msgObj);
    localStorage.setItem('chugli_messages', JSON.stringify(msgs));
    renderMessages();
  }

  function sendMessage(audioUrl = null) {
    const textInput = document.getElementById('message-input');
    const text = textInput.value.trim();

    if (!text && !audioUrl) return;

    const target = activeTab === 'private' ? document.getElementById('dm-target').value : 'ALL';

    const msgObj = {
      sender: currentUser,
      type: activeTab,
      target: target,
      text: text,
      audio: audioUrl,
      timestamp: new Date().toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' })
    };

    saveMessage(msgObj);
    textInput.value = '';
  }

  function renderMessages() {
    const container = document.getElementById('messages');
    container.innerHTML = '';
    const allMsgs = getStoredMessages();
    const currentTarget = document.getElementById('dm-target').value;

    const filtered = allMsgs.filter(m => {
      if (activeTab === 'public') return m.type === 'public';
      return m.type === 'private' && ((m.sender === currentUser && m.target === currentTarget) || (m.sender === currentTarget && m.target === currentUser));
    });

    filtered.forEach(m => {
      const msgDiv = document.createElement('div');
      const isOut = m.sender === currentUser;
      msgDiv.className = `message ${isOut ? 'outgoing' : 'incoming'}`;

      let content = `<div class="sender-name">${m.sender}</div>`;
      if (m.text) content += `<div>${m.text}</div>`;
      if (m.audio) content += `<audio controls src="${m.audio}" style="max-width: 200px; margin-top: 5px;"></audio>`;

      msgDiv.innerHTML = content;
      container.appendChild(msgDiv);
    });

    container.scrollTop = container.scrollHeight;
  }

  function loadPrivateMessages() {
    renderMessages();
  }

  // Voice Note Recorder (Web Audio API)
  async function toggleRecording() {
    const micBtn = document.getElementById('mic-btn');

    if (!isRecording) {
      try {
        const stream = await navigator.mediaDevices.getUserMedia({ audio: true });
        mediaRecorder = new MediaRecorder(stream);
        audioChunks = [];

        mediaRecorder.ondataavailable = e => audioChunks.push(e.data);
        mediaRecorder.onstop = () => {
          const audioBlob = new Blob(audioChunks, { type: 'audio/mp3' });
          const reader = new FileReader();
          reader.readAsDataURL(audioBlob);
          reader.onloadend = () => {
            sendMessage(reader.result);
          };
        };

        mediaRecorder.start();
        isRecording = true;
        micBtn.classList.add('recording');
      } catch (err) {
        alert('Microphone access is required to send voice notes.');
      }
    } else {
      mediaRecorder.stop();
      isRecording = false;
      micBtn.classList.remove('recording');
    }
  }
</script>
</body>
</html># 1181cg
