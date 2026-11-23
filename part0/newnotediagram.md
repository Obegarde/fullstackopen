sequenceDiagram
  participant browser
  participant server
  Note copied material: Ive copied in the initial load of the page for completeness

  browser->>server: GET <https://studies.cs.helsinki.fi/exampleapp/notes>
  activate server
  server-->>browser: HTML document
  deactivate server

  browser->>server: GET <https://studies.cs.helsinki.fi/exampleapp/main.css>
  activate server
  server-->>browser: the css file
  deactivate server

  browser->>server: GET <https://studies.cs.helsinki.fi/exampleapp/main.js>
  activate server
  server-->>browser: the JavaScript file
  deactivate server

  Note right of browser: The browser starts executing the JavaScript code that fetches the JSON from the server

  browser->>server: GET <https://studies.cs.helsinki.fi/exampleapp/data.json>
  activate server
  server-->>browser: [{ "content": "HTML is easy", "date": "2023-1-1" }, ... ]
  deactivate server

  Note right of browser: The browser executes the callback function that renders the notes

  Note: Diagram of a new note being created starts from here
  Note: User enters "hello test new" and press the Save button
  
  browser->>server: POST <https://studies.cs.helsinki.fi/exampleapp/new_note>
  activate server
  Note: server parses payload {note=hello+test+new} and adds a new note object to the notes array.
  server -->>browser: 302 Found Response
  deactivate server
  
  Note the 302 found response triggers a reload of the /notes page
  
  browser->>server: GET <https://studies.cs.helsinki.fi/exampleapp/notes>
  activate server
  server-->>browser: HTML document
  deactivate server

  browser->>server: GET <https://studies.cs.helsinki.fi/exampleapp/main.css>
  activate server
  server-->>browser: the css file
  deactivate server

  browser->>server: GET <https://studies.cs.helsinki.fi/exampleapp/main.js>
  activate server
  server-->>browser: the JavaScript file
  deactivate server

  Note right of browser: The browser starts executing the JavaScript code that fetches the JSON from the server which now includes the new note

  browser->>server: GET <https://studies.cs.helsinki.fi/exampleapp/data.json>
  activate server
  server-->>browser: [{ "content": "hello test new", "date": "2026-1-1" }, ... ]
  deactivate server
