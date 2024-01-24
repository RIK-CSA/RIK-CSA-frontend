---
title: Profile
search_exclude: true
---
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Personalized Profile Page</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f4;
            text-align: center;
            margin: 50px;
        }
        .profile-container {
            max-width: 600px;
            margin: auto;
            padding: 20px;
            background-color: #fff;
            border-radius: 5px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }
        h2 {
            color: #333;
        }
        p {
            color: #666;
        }
        .section {
            margin-top: 20px;
        }
        .section h3 {
            color: #555;
        }
    </style>
</head>
<body>
    <div class="profile-container">
        <h2>Welcome, <span th:text="${username}"></span>!</h2>
        <form action="/updateProfile" method="post">
            <div class="section">
                <h3>Past Experiences</h3>
                <p><textarea name="honorsAndAwards" th:text="${honorsAndAwards}"></textarea></p>
            </div>
            <div class="section">
                <h3>Honors and Awards</h3>
                <p>
                    <textarea name="honorsAndAwards" th:text="${honorsAndAwards}"></textarea>
                </p>
            </div>
            <!-- Add more sections as needed -->
            <div>
                <button type="submit">Save Changes</button>
            </div>
        </form>
    </div>
</body>
</html>

