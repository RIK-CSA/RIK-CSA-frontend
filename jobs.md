---
title: Personalized Skills
layout: none
permalink: /PersonalizedSkills/
---
{%- include rik_head.html -%}

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>LinkedIn Jobs Search</title>
    <h1 style="text-align: center;">Do Three Steps AND Find Your Best Jobs! 😉</h1>
</head>
<body>
<audio controls autoplay loop hidden>
    <source src="/audio/good_enough.mp3" type="audio/mpeg">
    Your browser does not support the audio element.
</audio>
<form id="search-form">
    <label for="languages">Select the programming languages you know:</label><br>
    <input type="checkbox" name="languages" value="python"> Python<br>
    <input type="checkbox" name="languages" value="java"> Java<br>
    <input type="checkbox" name="languages" value="cpp"> C++<br>
    <input type="checkbox" name="languages" value="javascript"> JavaScript<br>
    <input type="checkbox" name="languages" value="matlab"> Matlab<br>
    <input type="checkbox" name="languages" value="other"> Other<br><br>
    <label for="location">Enter your preferred job location:</label><br>
    <input type="text" id="location" name="location" placeholder="e.g., Chicago, IL">
    <br><br>
    <label for="job-type">Select job type:</label>
    <select id="job-type" name="job-type">
        <option value="full-time">Full-time</option>
        <option value="internship">Internship</option>
    </select>
    <br><br>
    <button type="button" onclick="fetchData()">Search Jobs</button>
</form>

<div id="result-container"></div>

<script>
    async function fetchData() {
        const selectedLanguages = Array.from(document.querySelectorAll('input[name="languages"]:checked'))
            .map(checkbox => checkbox.value);
        const location = document.getElementById('location').value;
        const jobType = document.getElementById('job-type').value;

        const url = 'https://linkedin-jobs-search.p.rapidapi.com/';
        const options = {
            method: 'POST',
            headers: {
                'content-type': 'application/json',
                'X-RapidAPI-Key': '72e68d1249msh0d5c16302ce65ddp18004bjsn343a844acf25',
                'X-RapidAPI-Host': 'linkedin-jobs-search.p.rapidapi.com'
            },
            body: JSON.stringify({
                search_terms: selectedLanguages.join(','),
                location: location,
                job_type: jobType,
                page: '1'
            })
        };

        try {
            const response = await fetch(url, options);
            const data = await response.json();
            const resultContainer = document.getElementById('result-container');

            if (Array.isArray(data)) {
                const jobs = data.map(job => ({
                    title: job.job_title,
                    company: job.company_name,
                    location: job.job_location
                }));

                resultContainer.innerHTML = ''; // Clear previous results

                jobs.forEach(job => {
                    const jobElement = document.createElement('div');
                    jobElement.innerHTML = `<strong>${job.title}</strong> at ${job.company}, ${job.location}<br><br>`;
                    resultContainer.appendChild(jobElement);
                });
            } else {
                console.error("Unexpected response structure:", data);
            }
        } catch (error) {
            console.error(error);
        }
    }
</script>

</body>
</html>

<style>
    /* Resetting default styles */
    body {
        font-family: 'Georgia', serif;
        margin: 0;
        padding: 0;
        background-color: #FFFF00; /* Light blue background color */
        color: #333;
    }

    /* Form styles */
    form {
        max-width: 600px;
        margin: 50px auto;
        padding: 20px;
        background-color: #fff;
        box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        border-radius: 10px;
    }

    /* Label styles */
    label {
        display: block;
        margin-bottom: 8px;
        background-color: #fff;
    }

    /* Checkbox styles */
    input[type="checkbox"] {
        margin-right: 5px;
    }

    /* Input and select styles */
    input[type="text"],
    select {
        width: 100%;
        padding: 8px;
        margin: 8px 0;
        box-sizing: border-box;
    }

    /* Button styles */
    button {
        background-color: #60e085;
        color: #fff;
        padding: 10px 15px;
        border: none;
        border-radius: 5px;
        cursor: pointer;
        font-size: 16px;
    }

    /* Button hover styles */
    button:hover {
        background-color: #4cb571;
    }

    /* Result container styles */
    #result-container {
        margin-top: 20px;
    }

    /* Result container div styles */
    #result-container div {
        margin-bottom: 20px;
    }
</style>
