<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Chat with AI Friend</title>
    <style>
        /* CSS Styling */
        body {
            font-family: Arial, sans-serif;
            background: #f0f4f8;
            margin: 0;
            padding: 20px;
        }
        .container {
            max-width: 800px;
            margin: 0 auto;
            background: white;
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(0,0,0,0.1);
            padding: 20px;
        }
        #chat-box {
            height: 400px;
            border: 1px solid #ddd;
            margin: 20px 0;
            padding: 10px;
            overflow-y: auto;
        }
        #user-input {
            width: 70%;
            padding: 10px;
            border: 1px solid #ddd;
            border-radius: 5px;
        }
        button {
            padding: 10px 20px;
            background: #4CAF50;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Chat with ZenBot 🤖</h1>
        <div id="chat-box"></div>
        <input type="text" id="user-input" placeholder="Type your message...">
        <button onclick="sendMessage()">Send</button>
        <p style="color: #666; margin-top: 20px;">Free plan: 5 messages/day. <a href="#" onclick="upgrade()">Upgrade → $5/month</a></p>
    </div>

    <script>
        // Simple ChatGPT Integration
        const API_KEY = 'YOUR_OPENAI_API_KEY'; // Get from https://platform.openai.com
        let messageCount = 0;

        async function sendMessage() {
            if (messageCount >= 5) {
                alert('Free limit reached! Please upgrade.');
                return;
            }

            const userInput = document.getElementById('user-input').value;
            const chatBox = document.getElementById('chat-box');

            // Add user message
            chatBox.innerHTML += `<div style="color: #333; margin: 10px 0;">You: ${userInput}</div>`;

            // Get AI response
            const response = await fetch('https://api.openai.com/v1/chat/completions', {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json',
                    'Authorization': `Bearer ${API_KEY}`
                },
                body: JSON.stringify({
                    model: "gpt-3.5-turbo",
                    messages: [{ role: "user", content: userInput }]
                })
            });

            const data = await response.json();
            const aiReply = data.choices[0].message.content;

            // Add AI message
            chatBox.innerHTML += `<div style="color: #4CAF50; margin: 10px 0;">ZenBot: ${aiReply}</div>`;
            document.getElementById('user-input').value = '';
            messageCount++;
        }

        function upgrade() {
            alert('Redirecting to payment...');
            // Replace with your Ko-fi/PayPal link
            window.location.href = 'https://ko-fi.com/yourpage';
        }
    </script>
</body>
</html>