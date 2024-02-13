---
title: Login
layout: none
permalink: /interview/login/
---
{%- include rik_head.html -%}
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Login System</title>
    <style>
        h3{
            background-color: #fff;
        }
        body {
            font-family: 'Georgia', serif;
            margin: 0;
            padding: 0;
            background-color: #FFFF00; /* Light blue background color */
            color: #333;
            text-align: center;
        }
        form {
            max-width: 600px;
            margin: 50px auto;
            padding: 20px;
            background-color: #fff;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            border-radius: 10px;
        }
        label {
            display: block;
            margin-bottom: 8px;
            background-color: #fff;
        }
        input[type="checkbox"] {
            margin-right: 5px;
        }
        input[type="text"],
        input[type="password"],
        select {
            width: 100%;
            padding: 10px;
            margin: 8px 0;
            box-sizing: border-box;
            border: 1px solid #ccc;
            border-radius: 3px;
            transition: border-color 0.3s ease;
        }
        input[type="text"]:focus,
        input[type="password"]:focus,
        select:focus {
            border-color: #4caf50;
        }
        /*Email Stuff*/
        input[type="text"],
        input[type="email"],
        select {
            width: 100%;
            padding: 10px;
            margin: 8px 0;
            box-sizing: border-box;
            border: 1px solid #ccc;
            border-radius: 3px;
            transition: border-color 0.3s ease;
        }
        input[type="text"]:focus,
        input[type="email"]:focus,
        select:focus {
            border-color: #4caf50;
        }
        button {
            background-color: #60e085;
            color: #fff;
            padding: 12px 15px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-size: 16px;
            transition: background-color 0.3s ease;
        }
        button:hover {
            background-color: #4cb571;
        }
        #result-container {
            margin-top: 20px;
        }
        #result-container div {
            margin-bottom: 20px;
        }
        #successMessage {
        display: none;
        font-size: 18px; /* Adjust the font size as needed */
        }
    </style>
</head>

<body>
    <div class="container">
        <div class="login-form">
            <h2>Login</h2>
            <form id="loginForm">
                <label for="email">Email:</label>
                <input type="email" id="email" required>
                <label for="password">Password:</label>
                <input type="password" id="password" required>
                <button type="submit">Login</button>
            </form>
            <p>Don't have an account? <a href="register">Register</a></p>
            <div id="successMessage" style="display: none;">You have successfully logged in!</div> <!-- Success message -->
        </div>
    </div>
    <script>
        function handleLogin(event) {
        event.preventDefault();
        // Get user input
        const email = document.getElementById("email").value;
        const password = document.getElementById("password").value;
        const user = {
            email: email,
            password: password
        };
        fetch('http://localhost:8020/api/v1/users/login', {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify(user)
        }).then(response => {
            if (!response.ok) {
                alert('Login successful');
            } else {
                return response.json();
            }
        }).then((response) => {
            localStorage.setItem('connectedUser', JSON.stringify(response));
            document.getElementById("successMessage").style.display = "block"; // Show success message
            setTimeout(function(){
                window.location.href = 'https://rik-csa.github.io/RIK-CSA-frontend/interview/';
            }, 2000); // Redirect after 2 seconds
        }).catch(error => {
            console.error('POST request error', error);
        });
    }
    const loginForm = document.getElementById("loginForm");
    loginForm.addEventListener("submit", handleLogin);
    </script>
</body>
</html>
