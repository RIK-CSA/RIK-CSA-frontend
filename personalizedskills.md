---
title: Personalized Skills
search_exclude: true
---
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My Skills</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f4;
            color: #333;
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        header {
            background-color: #3498db;
            color: #fff;
            text-align: center;
            padding: 1em;
        }

        section {
            max-width: 800px;
            margin: 20px auto;
            padding: 20px;
            background-color: #fff;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            border-radius: 5px;
        }

        h2 {
            color: #3498db;
        }

        ul {
            list-style-type: none;
            padding: 0;
        }

        li {
            margin-bottom: 10px;
        }

        footer {
            text-align: center;
            padding: 1em;
            background-color: #3498db;
            color: #fff;
        }
    </style>
</head>
<body>

    <header>
        <h1>Editable Skills Page</h1>
    </header>

    <section>
        <h2>Programming Languages</h2>
        <ul id="programming-languages">
            <li>JavaScript</li>
            <li>Python</li>
            <li>HTML/CSS</li>
        </ul>
        <button onclick="toggleForm('programming-languages')">Edit</button>
        <form id="programming-languages-form" class="edit-form" onsubmit="updateSkills(event, 'programming-languages')">
            <label for="programming-languages-input">Add a language:</label>
            <input type="text" id="programming-languages-input" required>
            <button type="submit">Add</button>
        </form>
    </section>

    <section>
        <h2>Web Development</h2>
        <ul id="web-development">
            <li>React.js</li>
            <li>Node.js</li>
            <li>Bootstrap</li>
        </ul>
        <button onclick="toggleForm('web-development')">Edit</button>
        <form id="web-development-form" class="edit-form" onsubmit="updateSkills(event, 'web-development')">
            <label for="web-development-input">Add a skill:</label>
            <input type="text" id="web-development-input" required>
            <button type="submit">Add</button>
        </form>
    </section>

    <footer>
        <p>&copy; 2024 Editable Skills Page</p>
    </footer>

    <script>
        function toggleForm(sectionId) {
            const form = document.getElementById(`${sectionId}-form`);
            form.style.display = form.style.display === 'none' ? 'block' : 'none';
        }

        function updateSkills(event, sectionId) {
            event.preventDefault();
            const input = document.getElementById(`${sectionId}-input`);
            const list = document.getElementById(sectionId);

            if (input.value.trim() !== "") {
                const newItem = document.createElement('li');
                newItem.textContent = input.value.trim();
                list.appendChild(newItem);
                input.value = "";
            }
        }
    </script>

</body>
</html>