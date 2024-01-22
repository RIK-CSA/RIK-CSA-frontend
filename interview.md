---
title: Login
layout: home
search_exclude: true
---

<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Interview</title>
    <link rel="icon" type="image/png" href="assets/favicon.png" />
    <style>
    :root {
    --grey-lightest: #f7f9fa;
    --white: #ffffff;
    --grey: #c8d1dc;
    --dark-grey: #6b7785;
    --dark-blue: #1f2d3d;
    --dark-blue-border: #2b3f56;
    --green: #72cc18;
    --red-dark: #bb0c0c;
    --turquoise: #1bebb9;
    }
    html,
    body {
    position: relative;
    width: 100%;
    height: 100%;
    }
    body {
    color: #333;
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto,
        Oxygen-Sans, Ubuntu, Cantarell, "Helvetica Neue", sans-serif;
    }
    .wrapper {
    background-color: var(--grey-lightest);
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    overflow-x: hidden;
    }
    header {
    width: calc(100% - 2rem);
    display: flex;
    justify-content: space-between;
    align-items: center;
    border-bottom: 1px solid #c8d1dc;
    padding: 0.5rem 1rem;
    background-color: var(--white);
    }
    span {
    font-size: 12px;
    font-weight: 600;
    }
    span.title {
    padding: 0 16px;
    }
    a {
    text-decoration: none;
    display: flex;
    align-items: center;
    padding: 8px 16px;
    color: var(--dark-blue);
    }
    a.new-tab-link {
    border: 1px solid var(--dark-grey);
    border-radius: 8px;
    }
    a:visited {
    color: var(--dark-blue);
    }
    a:focus {
    color: var(--dark-blue);
    }
    a:active {
    color: var(--turquoise);
    }
    a:hover {
    color: var(--turquoise);
    }
    .header-section {
    display: flex;
    align-items: center;
    }
    main {
    padding-top: 2em;
    display: grid;
    justify-content: center;
    align-content: center;
    }
    #daily-call-container {
    width: 75vw;
    height: 75vh;
    display: grid;
    }
    #join {
    font-size: 12px;
    padding: 4px 16px;
    border-radius: 8px;
    margin-bottom: 2em;
    border: 1px solid var(--turquoise);
    background-color: var(--turquoise);
    color: #1f2d3d;
    padding: 8px 16px;
    font-weight: 600;
    cursor: pointer;
    }
    #join:hover {
    cursor: pointer;
    background-color: #1bfdb9;
    box-shadow: rgba(27, 235, 185, 0.6) 0px 0px 0px 2px;
    }
    label {
    display: block;
    color: var(--dark-grey);
    font-size: 12px;
    margin-bottom: 4px;
    margin-top: 8px;
    }
    input {
    background-color: #fff;
    border-radius: 8px;
    padding: 8px;
    border: 1px solid #c8d1dc;
    }
    #error-msg {
    color: var(--red-dark);
    padding: 8px;
    }
    </style>
  </head>

  <body>
    <div class="wrapper">
      <header>
        <div class="header-section">
          <img src="assets/logo.svg" alt="Daily logo" />
          <span class="title">Interview</span>
        </div>
        <div class="header-section">
          <a
            class="new-tab-link"
            href="https://docs.daily.co/reference/daily-js"
            target="_blank"
            rel="noreferrer noopenner"
          >
            <span>API docs</span>
            <img src="assets/newtab.svg" alt="New tab" />
          </a>
          <a
            class="github-link"
            href="https://github.com/daily-demos/web-components"
            target="_blank"
            rel="noreferrer noopenner"
          >
            <img src="assets/github.svg" alt="Github" />
          </a>
        </div>
      </header>
      <main>
        <form>
          <label for="roomId">Daily room URL</label>
          <input
            id="roomId"
            value="https://your-domain.daily.co/your-room"
            type="text"
            size="50"
          />
          <input type="submit" value="Join call" id="join" />
        </form>
        <div id="error-msg"></div>
        <div id="daily-call-container">
          <!-- web components get built here after call join -->
        </div>
      </main>
    </div>
    <script>
        let token = "";
        async function tokenGeneration() {
            if (token != "") {
                
            }
        }
    </script>
  </body>
</html>