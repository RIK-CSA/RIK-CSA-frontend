---
title: Login
layout: none
permalink: /login/
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
    </style>
</head>

<body>
    <form id="login-form">
        <h3>Login</h3>
        <label for="signInEmailInput">Email</label>
        <input id="signInEmailInput" class="input" placeholder="Email" type="email">
        <label for="signInPasswordInput">Password</label>
        <input id="signInPasswordInput" class="input" placeholder="Password" type="password">
        <button class="signInButton" onclick="login_user()">Login</button>
    </form>
    <!-- Your existing HTML content goes here -->
    <div id="result"></div>
    <div id="userData"></div>
    <script>
    function userDbRequest() {
    // prepare HTML result container for new output
    const resultContainer = document.getElementById("result");
    // set options for cross origin header request
    const options = {
      method: 'GET', // *GET, POST, PUT, DELETE, etc.
      mode: 'cors', // no-cors, *cors, same-origin
      cache: 'default', // *default, no-cache, reload, force-cache, only-if-cached
      credentials: 'include', // include, *same-origin, omit
      headers: {
        'Content-Type': 'application/json',
      },
    };
    fetch("http://localhost:8020/api/person/", options)
      .then(response => {
        if (response.status !== 200) {
            const errorMsg = 'Database response error: ' + response.status;
            console.log(errorMsg);
            const tr = document.createElement("tr");
            const td = document.createElement("td");
            td.innerHTML = errorMsg;
            tr.appendChild(td);
            resultContainer.appendChild(tr);
            return;
        }
        // valid response will contain json data
        response.json().then(data => {
            console.log(data);
            for (const row of data) {
              // tr and td build out for each row
              const tr = document.createElement("tr");
              const name = document.createElement("td");
              const id = document.createElement("td");
              const age = document.createElement("td");
              // data is specific to the API
              name.innerHTML = row.name;
              id.innerHTML = row.email;
              age.innerHTML = row.age;
              // this build td's into tr
              tr.appendChild(name);
              tr.appendChild(id);
              tr.appendChild(age);
              // add HTML to container
              resultContainer.appendChild(tr);
            }
        })
    })
    // catch fetch errors (ie ACCESS to server blocked)
    .catch(err => {
      console.error(err);
      const tr = document.createElement("tr");
      const td = document.createElement("td");
      td.innerHTML = err + ": " + url;
      tr.appendChild(td);
      resultContainer.appendChild(tr);
    });
  }
  function login_user() {
    var myHeaders = new Headers();
    myHeaders.append("Content-Type", "application/json");
    // STEP ONE: COLLECT USER INPUT
    var raw = JSON.stringify({
        "email": document.getElementById("signInEmailInput").value,
        "password": document.getElementById("signInPasswordInput").value
        // For quick testing
        //"email": "toby@gmail.com",
        //"password": "123Toby!"
    });
    console.log(raw);
    var requestOptions = {
        method: 'POST',
        headers: myHeaders,
        credentials: 'include',
        body: raw,
        redirect: 'follow'
    };
    // STEP TWO: SEND REQUEST TO BACKEND AND GET JWT COOKIE
    fetch("http://localhost:8020/authenticate", requestOptions)
    .then(response => {
        if (!response.ok) {
            const errorMsg = 'Login error: ' + response.status;
            console.log(errorMsg);
            switch (response.status) {
                case 401:
                    alert("Incorrect username or password");
                    break;
                case 403:
                    alert("Access forbidden. You do not have permission to access this resource.");
                    break;
                case 404:
                    alert("User not found. Please check your credentials.");
                    break;
                // Add more cases for other status codes as needed
                default:
                    alert("Login failed. Please try again later.");
            }
            return Promise.reject('Login failed');
        }
        return response.text()
    })
    .then(result => {
        console.log(result);
        window.location.href = "http://127.0.0.1:4100/Login-Lesson/account";
    })
    .catch(error => console.error('Error during login:', error));
}
function fetchUserData() {
    var requestOptions = {
      method: 'GET',
      mode: 'cors',
      cache: 'default',
      credentials: 'include',
    };
    fetch("http://localhost:8020/api/person/jwt", requestOptions)
      .then(response => {
              if (!response.ok) {
                  const errorMsg = 'Login error: ' + response.status;
                  console.log(errorMsg);
                  switch (response.status) {
                      case 401:
                          alert("Please log into or make an account");
                          window.location.href = "http://127.0.0.1:4100/Login-Lesson/loginSignup";
                          break;
                      case 403:
                          alert("Access forbidden. You do not have permission to access this resource.");
                          break;
                      case 404:
                          alert("User not found. Please check your credentials.");
                          break;
                      // Add more cases for other status codes as needed
                      default:
                          alert("Login failed. Please try again later.");
                  }
                  return Promise.reject('Login failed');
              }
              return response.json();
              // Success!!!
          })
      .then(data => {
        // Display user data above the table
        const userDataContainer = document.getElementById("userData");
        userDataContainer.innerHTML = `
          <img src="/Login-Lesson/images/defaultUser.png" width="250" height="250">
          <h1><strong>${data.name}</strong></h1>
          <p>Email: ${data.email}</p>
          <p>Age: ${data.age}</p>
          <p>ID: ${data.id}</p>
          <button onclick="signOut()">Sign Out</button>
        `;
        console.log(data);
      })
      .catch(error => {console.log('error', error)});
}
function login_user() {
    var myHeaders = new Headers();
    myHeaders.append("Content-Type", "application/json");
    // STEP ONE: COLLECT USER INPUT
    var raw = JSON.stringify({
        "email": document.getElementById("signInEmailInput").value,
        "password": document.getElementById("signInPasswordInput").value,
        // For quick testing
        "test_email": "toby@gmail.com",
        "test_password": "123Toby!"
    });
    console.log(raw);
    var requestOptions = {
        method: 'POST',
        headers: myHeaders,
        credentials: 'include',
        body: raw,
        redirect: 'follow'
    };
    // STEP TWO: SEND REQUEST TO BACKEND AND GET JWT COOKIE
    fetch("http://localhost:8020/authenticate", requestOptions)
    .then(response => {
        if (!response.ok) {
            const errorMsg = 'Login error: ' + response.status;
            console.log(errorMsg);
            switch (response.status) {
                case 401:
                    alert("Incorrect username or password");
                    break;
                case 403:
                    alert("Access forbidden. You do not have permission to access this resource.");
                    break;
                case 404:
                    alert("User not found. Please check your credentials.");
                    break;
                // Add more cases for other status codes as needed
                default:
                    alert("Login failed. Please try again later.");
            }
            return Promise.reject('Login failed');
        }
        return response.text()
    })
    .then(result => {
        console.log(result);
        window.location.href = "http://127.0.0.1:4100/Login-Lesson/account";
    })
    .catch(error => {console.error('Error during login:', error);
    alert('There is currently an error going on. Please wait until we fix it');});
}
</script>
</body>

</html>