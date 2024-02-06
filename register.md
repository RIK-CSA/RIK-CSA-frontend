---
title: Register
layout: none
permalink: /register/
---

<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Register User</title>
  <link rel="stylesheet" href="/css/styles.css">
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css">
</head>
<body>
<div class="container">
  <div class="login-form">
    <h2>Register</h2>
    <form id="registrationForm">
      <label for="username">Username:</label>
      <input type="text" id="username" required>
      <label for="email">Email:</label>
      <input type="email" id="email" required>
      <label for="password">Password:</label>
      <input type="password" id="password" required>
      <button type="submit">Register</button>
    </form>
    <p>Already have an account? <a href="login">Login</a></p>
  </div>
</div>

<script>
    function handleRegistration(event) {
        event.preventDefault();

        // Get user input
        const username = document.getElementById("username").value;
        const email = document.getElementById("email").value;
        const password = document.getElementById("password").value;
        const status = "online"; // Assuming the status is online upon registration

        // Create an object with user information
        const user = {
            username: username,
            email: email,
            password: password,
            status: status,
        };
        fetch('http://localhost:8020/api/v1/users', {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify(user)
        }).then(response => {
            if (!response.ok) {
                throw new Error('Network response was not ok');
            }
            return response;
        }).then(() => {
            localStorage.setItem("connectedUser", JSON.stringify(user));
            window.location.href = "index.html";
        }).catch(error => {
            console.error('POST request error:', error);
        });

    }

    // Attach the handleRegistration function to the form's submit event
    const registrationForm = document.getElementById("registrationForm");
    registrationForm.addEventListener("submit", handleRegistration);
</script>
</body>
</html>