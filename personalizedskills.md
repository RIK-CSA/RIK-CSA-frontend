---
title: Personalized Skills
search_exclude: true
---
{%- include rik_head.html -%}

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title> Skills Page </title>
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
        .edit-form {
            display: none;
            margin-top: 10px;
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
        <h1>Editable Skills Page with Checkboxes</h1>
    </header>
    <section>
        <h2>Programming Languages</h2>
        <ul id="programming-languages">
            <li style="color:blue;">JavaScript</li>
            <li style="color:blue;">Python</li>
            <li style="color:blue;">HTML/CSS</li>
        </ul>
        <button onclick="toggleForm('programming-languages')">Edit</button>
        <form id="programming-languages-form" class="edit-form" onsubmit="updateSkills(event, 'programming-languages')">
            <label style="color:blue;">Choose from popular options:</label>
            <br>
            <input type="checkbox" id="js" value="JavaScript" >
            <label for="js">JavaScript</label>
            <br>
            <input type="checkbox" id="python" value="Python">
            <label for="python">Python</label>
            <br>
            <input type="checkbox" id="html-css" value="HTML/CSS">
            <label for="html-css">HTML/CSS</label>
            <br>
            <button type="submit">Add Selected</button>
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
            <label>Choose from popular options:</label>
            <br>
            <input type="checkbox" id="react" value="React.js">
            <label for="react">React.js</label>
            <br>
            <input type="checkbox" id="node" value="Node.js">
            <label for="node">Node.js</label>
            <br>
            <input type="checkbox" id="bootstrap" value="Bootstrap">
            <label for="bootstrap">Bootstrap</label>
            <br>
            <button type="submit">Add Selected</button>
        </form>
    </section>

    <footer>
        <p>&copy; 2024 Editable Skills Page with Checkboxes</p>
    </footer>

    <script>
        function toggleForm(sectionId) {
            const form = document.getElementById(`${sectionId}-form`);
            form.style.display = form.style.display === 'none' ? 'block' : 'none';
        }

        function updateSkills(event, sectionId) {
            event.preventDefault();
            const checkboxes = document.querySelectorAll(`#${sectionId}-form input[type="checkbox"]:checked`);
            const list = document.getElementById(sectionId);

            checkboxes.forEach((checkbox) => {
                const newItem = document.createElement('li');
                newItem.textContent = checkbox.value;
                list.appendChild(newItem);
                checkbox.checked = false; // Uncheck the checkbox after adding the skill
            });
        }
    </script>

</body>
</html>