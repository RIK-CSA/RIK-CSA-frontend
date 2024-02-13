<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Login System</title>
    <style>
        /* Your CSS styles here */
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
                    alert('Login and / or password is incorrect');
                }
                return response.json();
            }).then((response) => {
                localStorage.setItem('connectedUser', JSON.stringify(response));
                document.getElementById("successMessage").style.display = "block"; // Show success message
                setTimeout(function(){
                    window.location.href = 'https://rik-csa.github.io/RIK-CSA-frontend/';
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
