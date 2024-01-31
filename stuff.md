<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Person Information</title>
    <style>
        /* Add your styles here */
        body {
            font-family: Arial, sans-serif;
        }
    </style>
</head>
<body>

    <h1>Person Information</h1>

    <form id="personForm">
        <label for="name">Name:</label>
        <input type="text" id="name" required>

        <label for="email">Email:</label>
        <input type="email" id="email" required>

        <label for="password">Password:</label>
        <input type="password" id="password" required>

        <label for="dob">Date of Birth:</label>
        <input type="date" id="dob" required>

        <button type="button" onclick="submitForm()">Submit</button>
    </form>

    <div id="personInfo">
        <!-- Person information will be displayed here -->
    </div>

    <script>
        function submitForm() {
            // Get values from the form
            const name = document.getElementById('name').value;
            const email = document.getElementById('email').value;
            const password = document.getElementById('password').value;
            const dob = document.getElementById('dob').value;

            // Create a person object
            const person = {
                name,
                email,
                password,
                dob
            };

            // Display person information on the page
            displayPersonInfo(person);
        }

        function displayPersonInfo(person) {
            const personInfoDiv = document.getElementById('personInfo');
            personInfoDiv.innerHTML = `
                <h2>Person Information</h2>
                <p><strong>Name:</strong> ${person.name}</p>
                <p><strong>Email:</strong> ${person.email}</p>
                <p><strong>Date of Birth:</strong> ${person.dob}</p>
            `;
        }
    </script>

</body>
</html>
