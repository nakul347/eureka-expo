<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Feedback Website</title>
    <style>
        body {
            font-family: "Lucida Sans", sans-serif;
            text-align: center;
            background: linear-gradient(to right, #3b82f6, #9333ea, #ec4899);
            color: white;
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
        }
        .header-container {
            background: rgba(255, 255, 255, 0.2);
            padding: 20px;
            border-radius: 15px;
            box-shadow: 0px 0px 15px rgba(0,0,0,0.3);
            margin-bottom: 20px;
            width: 80%;
            display: flex;
            align-items: center;
            justify-content: center;
            position: relative;
        }
        .chaitanya-logo {
            width: 100px;
            height: 100px;
            margin-right: 20px;
        }
        .container {
            background: white;
            color: black;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0px 0px 10px rgba(0,0,0,0.2);
            width: 350px;
        }
        h1 {
            font-size: 40px;
            font-weight: bold;
            text-transform: uppercase;
            letter-spacing: 2px;
            text-shadow: 2px 2px 10px rgba(0,0,0,0.3);
        }
        h2 {
            font-size: 30px;
            font-weight: bold;
        }
        .team-container {
            display: flex;
            align-items: center;
            gap: 10px;
            background: rgba(255, 255, 255, 0.2);
            padding: 10px;
            border-radius: 10px;
            margin-top: 10px;
            box-shadow: 0px 0px 10px rgba(0,0,0,0.3);
        }
        .team-logo {
            width: 40px;
            height: 40px;
        }
        .team-name {
            font-size: 24px;
            font-weight: bold;
            font-family: 'Courier New', Courier, monospace;
        }
        h4 {
            font-size: 20px;
            margin-bottom: 15px;
        }
        input, textarea, button {
            width: 100%;
            margin-top: 10px;
            padding: 10px;
            border-radius: 5px;
            border: 1px solid #ccc;
            font-size: 16px;
        }
        button {
            background: #3b82f6;
            color: white;
            border: none;
            cursor: pointer;
            font-size: 16px;
            transition: 0.3s;
        }
        button:hover {
            background: #2563eb;
        }
        .hidden { display: none; }
        .info {
            font-size: 14px;
            margin-top: 10px;
            color: white;
            opacity: 0.8;
        }
        .eureka {
            font-size: 45px;
            font-weight: bolder;
            color: blue;
        }
        .title-container {
            display: flex;
            align-items: center;
        }
    </style>
</head>
<body>
    <div class="header-container">
        <div class="title-container">
            <img src="https://media-exp1.licdn.com/dms/image/C4D0BAQHxSgco_-fddg/company-logo_200_200/0?e=2159024400&v=beta&t=-Kore7RpBT8kDcUM2UDlyh4IXyrBqHvVR-seDRuTPVI" alt="Chaitanya Logo" class="chaitanya-logo">
            <div>
                <div class="eureka">EUREKA</div>
                <h1>Science Expo</h1>
            </div>
        </div>
        <h2>Welcome to the Feedback Website</h2>
    </div>
    
    <div class="team-container">
        <img src="https://cdn-icons-png.flaticon.com/512/2917/2917995.png" alt="Science Logo" class="team-logo">
        <span class="team-name">Team Fisher</span>
    </div>
    
    <h4>Feedback Form</h4>
    
    <div class="container">
        <input type="text" id="name" placeholder="Enter your name">
        <textarea id="feedback" placeholder="Enter your feedback"></textarea>
        <button onclick="submitFeedback()">Done</button>
        <p id="thankYouMessage" class="hidden">Thank you for your review!</p>
    </div>
    
    <button id="viewFeedback" class="hidden" onclick="toggleFeedback()">View Feedback</button>
    <div id="feedbackContainer" class="hidden container">
        <h2>All Feedback</h2>
        <div id="feedbackList"></div>
        <button onclick="hideFeedback()">Hide</button>
    </div>

    <p class="info">To know more about Sri Chaitanya Techno School, visit <a href="https://srichaitanyaschool.net/" target="_blank" style="color: white; text-decoration: underline;">this website</a>.</p>

    <script>
        let feedbacks = [];

        function submitFeedback() {
            const name = document.getElementById('name').value;
            const feedback = document.getElementById('feedback').value;
            if (name && feedback) {
                feedbacks.push({ name, feedback });
                document.getElementById('thankYouMessage').classList.remove('hidden');
                setTimeout(() => document.getElementById('thankYouMessage').classList.add('hidden'), 2000);
                document.getElementById('name').value = '';
                document.getElementById('feedback').value = '';
                checkAdminAccess();
            }
        }

        function checkAdminAccess() {
            const name = document.getElementById('name').value;
            const viewButton = document.getElementById('viewFeedback');
            if (name === '8888') {
                viewButton.classList.remove('hidden');
            } else {
                viewButton.classList.add('hidden');
            }
        }

        function toggleFeedback() {
            const feedbackContainer = document.getElementById('feedbackContainer');
            const feedbackList = document.getElementById('feedbackList');
            feedbackList.innerHTML = feedbacks.map(f => `<p><strong>${f.name}:</strong> ${f.feedback}</p>`).join('');
            feedbackContainer.classList.remove('hidden');
        }

        function hideFeedback() {
            document.getElementById('feedbackContainer').classList.add('hidden');
            document.getElementById('viewFeedback').classList.add('hidden');
            document.getElementById('name').value = '';
        }

        document.getElementById('name').addEventListener('input', checkAdminAccess);
    </script>
</body>
</html>
