---
title: Interview
layout: base
search_exclude: true
---

<html>
  <head>
    <!--favicon-->
    <link
      rel="shortcut icon"
      href="https://videosdk.live/favicon/favicon.ico"
    />
    <meta charset="UTF-8" />
    <link rel="stylesheet" href="./assets/css/index.css" />
    <!--add necessary bootstrap links here -->
  </head>
  <body class="bg-secondary">
    <!--join-screen-->
    <div
      id="join-screen"
      class="flex flex-row align-items-center justify-content-center h-100" >
      <button
        class="btn btn-primary"
        id="btnCreateMeeting"
        onclick="meetingHandler(true)" >
        New Meeting
      </button>
      <input
        type="text"
        id="txtMeetingCode"
        placeholder="Enter Meeting Code .." />
      <button
        id="btnJoinMeeting"
        onclick="meetingHandler(false)"
        class="btn btn-primary" >
        Join
      </button>
    </div>
    <!--grid-screen-->
    <div id="grid-screen">
      <div>
        <input
          type="text"
          class="form-control navbar-brand"
          id="lblMeetingId"
          readonly
        />
        <button class="btn btn-dark" id="btnToggleMic">Unmute Mic</button>
        <button class="btn btn-dark" id="btnToggleWebCam">Disable Webcam</button>
        <button class="btn btn-dark" id="btnLeaveMeeting">Leave Meeting</button>
      </div>
      <br />
      <div id="videoContainer"></div>
      <div
        style="position: absolute;
              top: 10px;
              right: 0px;
              height: 50%;
              overflow-y: scroll;" >
        <h3>Participants List</h3>
        <div id="participantsList"></div>
      </div>
    </div>
    <!--scripts-->
    <script src="./assets/js/config.js"></script>
    <script src="./assets/js/index.js"></script>
    <script src="https://sdk.videosdk.live/js-sdk/0.0.20/videosdk.js"></script>
  </body>
</html>