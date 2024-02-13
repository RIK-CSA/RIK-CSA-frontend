---
title: Find some employees
layout: none
search_exclude: true
permalink: /FindEmployees/
---
{%- include rik_head.html -%}
<html>
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Worker Hiring System</title>
    <!-- Include jQuery -->
    <script src="https://code.jquery.com/jquery-3.6.4.min.js"></script>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            margin: 20px;
            padding: 20px;
            background-color: #f5f5f5;
        }

        h1, h2 {
            background-color: #fff;
            color: #333;
        }

        form {
            background-color: #fff;
            padding: 20px;
            border-radius: 8px;
            margin-bottom: 20px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }

        label {
            display: block;
            background-color: #fff;
            margin-bottom: 8px;
        }

        input {
            width: 100%;
            padding: 8px;
            margin-bottom: 12px;
            box-sizing: border-box;
            border: 1px solid #ccc;
            border-radius: 4px;
        }

        button {
            background-color: #4caf50;
            color: white;
            padding: 10px 15px;
            border: none;
            border-radius: 4px;
            cursor: pointer;
        }

        button:hover {
            background-color: #45a049;
        }

        #result {
            background-color: #fff;
            margin-top: 20px;
        }
    </style>
</head>

<body>
    <h1>Worker Hiring System</h1>
    <!-- Add Worker Form -->
    <form id="addWorkerForm">
        <h2>Add Worker</h2>
        <label for="workerName">Name:</label>
        <input type="text" id="workerName" required>
        <br>
        <label for="languagesKnown">Languages Known (comma-separated):</label>
        <input type="text" id="languagesKnown" required>
        <br>
        <label for="preferredLocation">Preferred Location:</label>
        <input type="text" id="preferredLocation" required>
        <br>
        <label for="internshipPreferred">Internship Preferred:</label>
        <input type="checkbox" id="internshipPreferred">
        <br>
        <button type="button" onclick="addWorker()">Add Worker</button>
    </form>

    <!-- Find Most Relevant Worker Form -->
    <form id="findMostRelevantForm">
        <h2>Find Most Relevant Worker</h2>
        <label for="newLanguagesKnown">Languages Known (comma-separated):</label>
        <input type="text" id="newLanguagesKnown" required>
        <br>
        <label for="newPreferredLocation">Preferred Location:</label>
        <input type="text" id="newPreferredLocation" required>
        <br>
        <button type="button" onclick="findMostRelevantWorker()">Find Most Relevant Worker</button>
    </form>

    <!-- Display All Workers Button -->
    <button type="button" onclick="getAllWorkers()">Display All Workers</button>

    <!-- Display Result -->
    <div id="result"></div>

    <script>
        // Function to add a new worker (same as before)
        function addWorker() {
        // Gather data from the form
        const workerData = {
            name: $('#workerName').val(),
            languagesKnown: $('#languagesKnown').val().split(',').map(lang => lang.trim()),
            preferredLocation: $('#preferredLocation').val(),
            internshipPreferred: $('#internshipPreferred').is(':checked')
        };

        // Make a POST request to the backend API endpoint
        fetch('http://localhost:8020/api/worker/add', {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json',
            },
            body: JSON.stringify(workerData),
        })
        .then(response => {
            if (response.ok) {
                // If the request is successful, clear the form fields
                $('#workerName').val('');
                $('#languagesKnown').val('');
                $('#preferredLocation').val('');
                $('#internshipPreferred').prop('checked', false);
                // Display a success message or perform any other actions as needed
                alert('Worker added successfully');
            } else {
                // If there is an error, display an error message
                alert('Error adding worker. Please try again.');
            }
        })
        .catch(error => {
            console.error('Error:', error);
            alert('Error adding worker. Please try again.');
        });
    }
        // Function to find the most relevant worker
        function findMostRelevantWorker() {
            const newWorkerData = {
                languagesKnown: $('#newLanguagesKnown').val().split(',').map(lang => lang.trim()),
                preferredLocation: $('#newPreferredLocation').val()
            };

            fetch('http://localhost:8020/api/worker/findMostRelevant?k=3', {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json',
                },
                body: JSON.stringify(newWorkerData),
            })
            .then(response => response.json())
            .then(data => {
                $('#result').text(`Most relevant worker: ${data.name}`);
            })
            .catch(error => {
                console.error('Error:', error);
                $('#result').text('Error finding the most relevant worker.');
            });
        }

        // Function to get all workers
        function getAllWorkers() {
            fetch('http://localhost:8020/api/worker/allWorkers')
            .then(response => response.json())
            .then(data => {
                const workerList = data.map(worker => `${worker.name} - ${worker.preferredLocation}`);
                $('#result').html(`<h2>All Workers</h2><ul>${workerList.map(worker => `<li>${worker}</li>`).join('')}</ul>`);
            })
            .catch(error => {
                console.error('Error:', error);
                $('#result').text('Error getting all workers.');
            });
        }
    </script>

</body>
</html>