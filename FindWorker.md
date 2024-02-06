---
title: Find some employees
layout: none
search_exclude: true
permalink: /FindEmployees/
---
{%- include rik_head.html -%}

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Worker Hiring System</title>
    <!-- Include jQuery -->
    <script src="https://code.jquery.com/jquery-3.6.4.min.js"></script>
</head>
<body>

    <h1>Worker Hiring System</h1>

    <!-- Add Worker Form -->
    <h2>Add Worker</h2>
    <form id="addWorkerForm">
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
    <h2>Find Most Relevant Worker</h2>
    <form id="findMostRelevantForm">
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

        // Function to find the most relevant worker
        function findMostRelevantWorker() {
            const newWorkerData = {
                languagesKnown: $('#newLanguagesKnown').val().split(',').map(lang => lang.trim()),
                preferredLocation: $('#newPreferredLocation').val()
            };

            fetch('http://localhost:8020/api/worker/findMostRelevant?k=1', {
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