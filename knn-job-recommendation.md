<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Job Recommendations</title>
    <style>
        .container {
            max-width: 600px;
            margin: 50px auto;
            padding: 20px;
            text-align: center;
        }
        h1 {
            color: #333;
        }
        input[type="text"] {
            width: 100%;
            padding: 10px;
            margin: 10px 0;
            border: 1px solid #ccc;
            border-radius: 5px;
        }
        button {
            background-color: #3498db;
            color: #fff;
            border: none;
            padding: 10px 20px;
            border-radius: 5px;
            cursor: pointer;
        }
        button:hover {
            background-color: #2980b9;
        }
        #jobListings {
            margin-top: 20px;
            text-align: left;
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
