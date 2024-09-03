# Single Page App

Taken from a YouTube Tutorial:
https://www.youtube.com/watch?v=6BozpmSjk-Y

### How to run the app

```
node server.js
```

Navigate to `http://localhost:3000/`

### How the application works

- Initially we start at the dashboard page with `index.html` which contains links to the other viws through a `data-link` class attribute.Default action of clicking is overridden and the JavaScript of the view corresponding to the value is loaded and updates the page with the new content (e.g. `<div id="app"></div>`)
- `index.js` is pulled in through `index.html` and contains the main application logic
- `router` function effectively loops through the routes and tests for a match. If no match is found then load the dashboard page.
- Views all inherit from `AbstractView` and contain an `async getHtml()` to allow for the possibility we want to render it server-side (i.e. by sending a request to the server for the HTML)

### History API

- History API allows us to interact with the browser's session history. As the user visits new pages these pages are added to the session history
- SPA breaks the expected behaviour of the browser's "Back" and "Forward" buttons as from the browser's POV it didn't load a new page. 
- We want to ensure the "Back" and "Forward" buttons reload the last/next state. This is what `pushState()` and popstate event solve.
   - `pushState()` adds a new entry to the session history and changes the URL displayed in the browser

#### Walkthrough
1. User first lands on `/` and `pushState()` adds a new entry with this URL to the session history
2. User presses on a new link and `pushState()` adds a new entry with this new URL (e.g. `/posts`)
3. User presses on a new link and `pushState()` adds a new entry with this new URL (e.g. `/posts/1`)
4. Stack looks like this:

| Stack |
| ----------- |
| `/` |
| `/posts`  |
| `/posts/1`  |

5. User presses on 'Back' and the stack is popped removing the `/posts/1` entry and a `popstate` event is now fired containing the latest entry (e.g. `/posts`) which we navigate to