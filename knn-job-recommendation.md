---
title: Job Recommendations
search_exclude: true
permalink: /recommend/
layout: none
---

{%- include rik_head.html -%}
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Job Recommendations</title>
 <style>
        body {
            font-family: 'Arial', sans-serif;
            background-color: #f5f5f5;
            margin: 0;
            padding: 0;
        }

        .container {
            max-width: 800px;
            margin: 50px auto;
            padding: 20px;
            background-color: #fff;
            border-radius: 8px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        }

        h1 {
            color: #3498db;
            background-color: #fff;

        }

        label {
            background-color: #fff;
            display: block;
            margin-top: 20px;
            font-size: 16px;
            color: #333;
        }

        input[type="text"] {
            background-color: #fff;
            width: 100%;
            padding: 10px;
            margin-top: 5px;
            border: 1px solid #ccc;
            border-radius: 5px;
            font-size: 14px;
        }

        button {
            background-color: #3498db;
            color: #fff;
            border: none;
            padding: 10px 20px;
            border-radius: 5px;
            cursor: pointer;
            font-size: 16px;
        }

        button:hover {
            background-color: #2980b9;
        }

        #jobListings {
            background-color: #fff;
            margin-top: 20px;
            text-align: left;
        }

        h2 {
            background-color: #fff;
            color: #3498db;
            margin-top: 20px;
        }

        p {
            background-color: #fff;
            font-size: 14px;
            margin: 8px 0;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Job Recommendations</h1>
        <label for="skills">Enter your skills (comma-separated):</label>
        <input type="text" id="skills" placeholder="e.g., JavaScript, Python, HTML/CSS">
        <button onclick="findJobs()">Find Jobs</button>
        <div id="jobListings"></div>
    </div>
    <script>
        // JavaScript code
        function findJobs() {
            // Get user's skills from input field
            const skillsInput = document.getElementById('skills');
            const userSkills = skillsInput.value.split(',').map(skill => skill.trim().toLowerCase());
            // Sample job listings (for demonstration purposes)
            const jobListings = [
                { title: 'Frontend Developer', skills: ['javascript', 'html/css', 'react'] },
                { title: 'Backend Developer', skills: ['python', 'java', 'node.js'] },
                { title: 'Full Stack Developer', skills: ['javascript', 'html/css', 'node.js', 'react'] },
                { title: 'Data Scientist', skills: ['python', 'r', 'machine learning'] },
                // Add more job listings here...
                { title: 'UI/UX Designer', skills: ['ui/ux design', 'photoshop', 'sketch'] },
                { title: 'Digital Marketing Specialist', skills: ['digital marketing', 'seo', 'social media'] },
                { title: 'Project Manager', skills: ['project management', 'communication', 'leadership'] }
            ];
            // Calculate similarity between user's skills and job listings using simple matching
            const recommendations = [];
            jobListings.forEach(job => {
                const intersection = job.skills.filter(skill => userSkills.includes(skill));
                recommendations.push({ job: job.title, similarity: intersection.length });
            });
            // Sort recommendations by similarity (descending order)
            recommendations.sort((a, b) => b.similarity - a.similarity);
            // Display the top 3 recommendations
            const jobListingsDiv = document.getElementById('jobListings');
            jobListingsDiv.innerHTML = '<h2>Top Job Recommendations:</h2>';
            recommendations.slice(0, 3).forEach(recommendation => {
                jobListingsDiv.innerHTML += `<p>${recommendation.job}</p>`;
            });
        }
    </script>
</body>
</html>
