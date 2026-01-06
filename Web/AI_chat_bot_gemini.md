```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Gemini AI Chatbot</title>
    <style>
      body {
        font-family: Arial, sans-serif;
        display: flex;
        justify-content: center;
        align-items: center;
        flex-direction: column;
        height: 100vh;
        margin: 0;
        background-color: #f5f5f5;
      }

      .chat-container {
        width: 400px;
        background-color: white;
        border-radius: 8px;
        box-shadow: 0px 0px 15px rgba(0, 0, 0, 0.1);
        overflow: hidden;
      }

      .chat-header {
        background-color: #0078d7;
        color: white;
        padding: 10px;
        text-align: center;
        display: flex;
        align-items: center;
        justify-content: center;
      }

      .owner {
        background-color: #0078d7;
        color: white;
        padding: 5px;
        width: 20%;
        text-align: center;
        border-radius: 20px;
        margin-top: 10px;
      }

      .chat-box {
        padding: 10px;
        height: 400px;
        overflow-y: auto;
        border-bottom: 1px solid #ddd;
      }

      .chat-input {
        display: flex;
        padding: 10px;
        border-top: 1px solid #ddd;
      }

      #user-input {
        flex: 1;
        padding: 10px;
        border: 1px solid #ddd;
        border-radius: 5px;
        margin-right: 10px;
      }

      button {
        padding: 10px;
        background-color: #0078d7;
        color: white;
        border: none;
        border-radius: 5px;
        cursor: pointer;
      }

      button:hover {
        background-color: #005fa3;
      }

      .message {
        margin-bottom: 15px;
      }

      .user-message {
        text-align: right;
        color: #0078d7;
      }

      .bot-message {
        text-align: left;
        color: #333;
      }
    </style>
  </head>
  <body>
    <div class="chat-container">
      <div class="chat-header">
        <h2>Gemini AI Chatbot</h2>
      </div>
      <div class="chat-box" id="chat-box">
        <!-- Chat messages will be displayed here -->
      </div>
      <div class="chat-input">
        <input type="text" id="user-input" placeholder="Type your message..." />
        <button onclick="sendMessage()">Send</button>
      </div>
    </div>
    <div class="owner">
      <p>Gokul S</p>
    </div>
    <script>
      const chatBox = document.getElementById("chat-box");
      const userInput = document.getElementById("user-input");

      async function sendMessage() {
        const message = userInput.value.trim();
        if (!message) return;

        displayMessage(message, "user-message");
        userInput.value = "";

        const botMessage = await getBotResponse(message);

        displayMessage(botMessage, "bot-message");
      }

      async function getBotResponse(userMessage) {
        try {
          const response = await fetch(
            "https://generativelanguage.googleapis.com/v1beta/models/gemini-1.5-flash-latest:generateContent?key=AIzaSyBpwCglFkW2yDsjDtHepIRFUdWxZROFKe4",
            {
              method: "POST",
              headers: { "Content-Type": "application/json" },
              body: JSON.stringify({
                contents: [{ parts: [{ text: userMessage }] }],
              }),
            }
          );

          const data = await response.json();
          return (
            data.contents?.[0]?.parts?.[0]?.text ||
            "The model is overloaded. Please try again later."
          );
        } catch (error) {
          console.error("Error fetching the response:", error);
          return "Error connecting to the AI.";
        }
      }

      function displayMessage(message, type) {
        const messageElement = document.createElement("div");
        messageElement.classList.add("message", type);
        messageElement.textContent = message;
        chatBox.appendChild(messageElement);
        chatBox.scrollTop = chatBox.scrollHeight;
      }
    </script>
  </body>
</html>

```
