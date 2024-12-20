# Quotes API Project

## Description
This project is a simple webpage that fetches data from an API and displays it using a typewriter effect. The text is styled in a futuristic design with a glowing effect.

## Features
- Fetches data from an API endpoint.
- Displays quotes one by one in a typewriter style.
- Animates a blinking cursor to simulate typing.
- Automatically cycles through the fetched quotes with a delay.

---

## File Structure

### HTML (`index.html`)
Defines the structure of the webpage, including:
- A `<div>` with the id `typetext` to display the quotes.
- Links to the CSS file for styling and the JavaScript file for functionality.

### CSS (`style.css`)
Applies styles to the page:
- Futuristic font and glowing text effect.
- Black background for high contrast.
- Animation for a blinking cursor.

### JavaScript (`script.js`)
Handles the functionality:
1. Fetches quotes from `https://jsonplaceholder.typicode.com/posts`.
2. Displays the quotes using a typewriter effect.
3. Cycles through quotes with a delay of 3 seconds.

---

## Setup Instructions

### Prerequisites
- A web browser to view the project.
- An internet connection to fetch quotes from the API.

### Steps to Run the Project
1. Clone or download the project files.
2. Ensure the folder contains:
   - `index.html`
   - `style.css`
   - `script.js`
3. Open the `index.html` file in a browser.

---

## Code Explanation

### `index.html`
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Quotes API</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <div id="typetext"></div>

    <script src="script.js"></script>
</body>
</html>
```
This file sets up the basic structure and links the CSS and JavaScript files.

### `style.css`
```css
body {
    font-family: "Neuropol X";
    letter-spacing: 2px;
    padding: 20px;
    font-size: 22px;
    background-color: black;
    color: #00FFFF;
    text-shadow: 0 0 10px #00FFFF;
}
span {
    animation: blinker 1s linear infinite;
}
@keyframes blinker {
    50% {
        opacity: 0;
    }
}
```
This file adds:
- Styling for the text and page.
- Blinking cursor animation.

### `script.js`
```javascript
let quoteArray = [];
let index = 0;
let textPosition = 0;
let flag = true;
let destination = document.getElementById("typetext");

window.addEventListener('load', () => {
    loadQuote();
    typewriter();
});

function loadQuote() {
    const url = "https://jsonplaceholder.typicode.com/posts";
    fetch(url)
        .then(response => {
            if (response.ok) return response.json();
            else throw new Error(`HTTP error: ${response.status}`);
        })
        .then(data => {
            quoteArray = data.map(post => post.body);
        })
        .catch(error => console.error('Error fetching quotes:', error));
}

function typewriter() {
    if (quoteArray.length === 0) {
        setTimeout(typewriter, 100);
        return;
    }
    if (flag) {
        flag = false;
        textPosition = 0;
    }
    const currentQuote = quoteArray[index];
    destination.innerHTML = currentQuote.substring(0, textPosition) + '<span>▮</span>';

    if (textPosition++ < currentQuote.length) {
        setTimeout(typewriter, 100);
    } else {
        textPosition = 0;
        flag = true;
        index = (index + 1) % quoteArray.length;
        setTimeout(typewriter, 3000);
    }
}
```
This script:
- Fetches data from the API and stores it in an array.
- Displays each quote character by character, simulating typing.
- Loops through all quotes infinitely.

---

## Notes
- If the API fails, the console will log an error.
- Add a fallback message for better user experience if quotes fail to load.

## Possible Improvements
- Add support for custom APIs.
- Provide a pause/play button for the typewriter.
- Enhance accessibility by adding ARIA roles.

---

## License
This project is open-source and available for personal or educational use.
