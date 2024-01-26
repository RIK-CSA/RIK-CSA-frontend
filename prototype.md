<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Job Search</title>
<style>
    body {
        font-family: Arial, sans-serif;
        margin: 0;
        padding: 20px;
    }
    form {
        max-width: 600px;
        margin: 0 auto;
    }
    input[type="text"] {
        width: 100%;
        padding: 10px;
        margin-bottom: 10px;
    }
    input[type="submit"] {
        background-color: #007bff;
        color: #fff;
        padding: 10px 20px;
        border: none;
        cursor: pointer;
    }
    input[type="submit"]:hover {
        background-color: #0056b3;
    }
</style>
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
<script>
    $(document).ready(function() {
        $('#jobSearchForm').submit(function(event) {
            event.preventDefault(); // Prevent the form from submitting normally
            // Construct the request settings
            const settings = {
                async: true,
                crossDomain: true,
                url: 'https://linkedin-jobs-scraper-api.p.rapidapi.com/jobs',
                method: 'POST',
                headers: {
                    'content-type': 'application/json',
                    'X-RapidAPI-Key': 'b1182b6a64mshff6fcbeabf69dc2p199d99jsn12adc869f7a0',
                    'X-RapidAPI-Host': 'linkedin-jobs-scraper-api.p.rapidapi.com'
                },
                processData: false,
                data: JSON.stringify({
                    title: $('#jobTitle').val(),
                    location: $('#location').val(),
                    rows: 100
                })
            };

            // Send the AJAX request
            $.ajax(settings).done(function(response) {
                console.log(response);
                // Handle the response here, such as displaying job listings on the page
            });
        });
    });
</script>
</head>
<body>
    <h1>Job Search</h1>
    <form id="jobSearchForm" action="search-results.html" method="GET">
        <label for="jobTitle">Job Title:</label>
        <input type="text" id="jobTitle" name="jobTitle" placeholder="Enter job title">
        <label for="location">Location:</label>
        <input type="text" id="location" name="location" placeholder="Enter location">
        <input type="submit" value="Search">
    </form>
</body>
</html>
