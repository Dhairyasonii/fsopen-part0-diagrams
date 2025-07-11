# Sequence Diagram – Creating a New Note

This diagram represents the sequence of interactions that occur when a user creates a new note on the page:  
[https://studies.cs.helsinki.fi/exampleapp/notes](https://studies.cs.helsinki.fi/exampleapp/notes)

The user enters text into the input field and clicks the **Save** button. The browser sends the data to the server using a `POST` request. The server responds with a redirect, which causes the browser to reload the page and fetch updated resources including the new note.

```mermaid
sequenceDiagram
    participant Browser
    participant Server

    Note right of Browser: User enters a note and clicks "Save"

    Browser->>Server: POST /new_note
    activate Server
    Server-->>Browser: 302 Redirect to /notes
    deactivate Server

    Browser->>Server: GET /notes
    activate Server
    Server-->>Browser: HTML document
    deactivate Server

    Browser->>Server: GET /main.css
    activate Server
    Server-->>Browser: CSS file
    deactivate Server

    Browser->>Server: GET /main.js
    activate Server
    Server-->>Browser: JavaScript file
    deactivate Server

    Note right of Browser: Browser executes JavaScript to fetch JSON data

    Browser->>Server: GET /data.json
    activate Server
    Server-->>Browser: JSON containing all notes (including the new one)
    deactivate Server

    Note right of Browser: Browser renders the updated list of notes
