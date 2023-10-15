```mermaid
sequenceDiagram
    participant browser
    participant server

    browser->>server: request HTTP-POST https://studies.cs.helsinki.fi/exampleapp/new-note
    activate server
    server-->>browser: server responds with HTTP status code 302
    deactivate server

    browser->>server: new HTTP GET request to the address defined in the header's Location - the address notes. https://studies.cs.helsinki.fi/exampleapp/notes
    activate server
    server-->>browser: browser reloads the Notes page. The reload causes three more HTTP requests: fetching the style sheet (main.css)
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.js
    activate server
    server-->>browser: the JavaScript file
    deactivate server

    Note right of browser: The browser starts executing the JavaScript code that fetches the JSON from the server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/data.json
    activate server
    server-->>browser: [{ "content": "new note", "date": "2023-10-15" }, ... ]
    deactivate server

```