<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Sedyka Chatbot</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 0;
      background-color: #f0f8ff;
    }

    .chat-container {
      display: flex;
      flex-direction: column;
      justify-content: space-between;
      height: 100vh;
      max-width: 600px;
      margin: 0 auto;
      border: 1px solid #ddd;
      background-color: #fff;
      box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    }

    .chat-header {
      padding: 10px;
      background-color: #007bff;
      color: white;
      text-align: center;
      font-size: 20px;
    }

    .chat-messages {
      flex: 1;
      overflow-y: auto;
      padding: 15px;
    }

    .chat-messages .message {
      margin: 10px 0;
      max-width: 70%;
      padding: 10px;
      border-radius: 10px;
      word-wrap: break-word;
    }

    .chat-messages .user {
      background-color: #007bff;
      color: white;
      align-self: flex-end;
    }

    .chat-messages .bot {
      background-color: #f1f1f1;
      color: black;
      align-self: flex-start;
    }

    .chat-input {
      display: flex;
      padding: 10px;
      border-top: 1px solid #ddd;
    }

    .chat-input input {
      flex: 1;
      padding: 10px;
      border: 1px solid #ddd;
      border-radius: 5px;
      outline: none;
    }

    .chat-input button {
      padding: 10px 15px;
      margin-left: 10px;
      border: none;
      border-radius: 5px;
      background-color: #007bff;
      color: white;
      cursor: pointer;
    }

    .chat-input button:hover {
      background-color: #0056b3;
    }
  </style>
</head>
<body>
  <div class="chat-container">
    <div class="chat-header">Sedyka Chatbot</div>
    <div class="chat-messages" id="chat-messages"></div>
    <div class="chat-input">
      <input type="text" id="user-input" placeholder="Type your message here..." />
      <button onclick="sendMessage()">Send</button>
    </div>
  </div>

  <script>
    const messagesContainer = document.getElementById('chat-messages');

    async function sendMessage() {
      const userInput = document.getElementById('user-input').value;
      if (!userInput.trim()) return;

      // Display the user message
      addMessage(userInput, 'user');

      // Clear the input field
      document.getElementById('user-input').value = '';

      // Call the OpenAI API
      try {
        const response = await fetch('https://api.openai.com/v1/chat/completions', {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json',
            'Authorization': 'Bearer YOUR_API_KEY', // Replace with your OpenAI API key
          },
          body: JSON.stringify({
            model: 'gpt-3.5-turbo',
            messages: [{ role: 'user', content: userInput }],
          }),
        });

        if (response.ok) {
          const data = await response.json();
          const botMessage = data.choices[0].message.content;
          addMessage(botMessage, 'bot');
        } else {
          addMessage('Error: Unable to get a response from ChatGPT.', 'bot');
        }
      } catch (error) {
        console.error('Error:', error);
        addMessage('Error: Unable to connect to the server.', 'bot');
      }
    }

    function addMessage(content, sender) {
      const messageElement = document.createElement('div');
      messageElement.classList.add('message', sender);
      messageElement.textContent = content;
      messagesContainer.appendChild(messageElement);

      // Scroll to the bottom of the chat
      messagesContainer.scrollTop = messagesContainer.scrollHeight;
    }
  </script>
</body>
</html>
