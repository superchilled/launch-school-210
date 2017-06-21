# Chrome Dev Tools Cheat Sheet

## Accessing Dev Tools

  *To access Dev Tools in Chrome browser, you can:
    * Right-click on a web page and select 'Inspect'
    * Select 'More Tools > Developer Tools' from the Chrome menu button (top right)

## Sources Tab

  * The 'Sources' tab:
    * Makes the javascript code running on a webpage visible
    * Provides a number of different debugging tools and controls

### Console

  * To view the 'Console' within the Sources tab layout, hit the `Esc` key
  * The console will will display any javascript output from js code running in the page being inspected

#### Running JavaScript in the console

  * You can type JavaScript code into the console and it will be evaluated
  * You can access any existing function
  * Pressing `Enter` after typing code into the console automatically executes that code
  * You can type multi-line code by pressing `Shift-Enter` to move to a new line
  * For multi-line code it is usually easier to edit it ina separate file. This could be:
    *  An `.html` file with `<script>` tags containing the JavaScript code
    * A separate `.js` file linked from the `.html` file


    - Accessing functions
    - Accessing variables

### The Debugger

  * The Debugger is a window showing JavaScript code and a set of controls for manipulating that code

#### Accessing a JavaScript File

  * To access the code n a JavaScript file, click on the file in the file-tree of the sources window

#### Debugger Controls

  * Debugger controls are visible in the right-hand window
  * Step Through controls are displayed along the top of the debugger controls
        - Play/ Pause button
        - Step over next function call
        - Step into next function call
        - Step out of current function
        - Pause on Exceptions
  * Current State controls
        - Call Stack
        - Scope values

#### Creating a breakpoint
  
  * A breakpoint marks a place that the browser is going to stop executing the code and pause in order to allow a developer to inspect the state of the page
  * A breakpoint can be set by:
    * Clicking on line number in the code window
    * Adding debugger statement (`debugger()` in the actual code file and saving it (debugger statemetns should be removed before pushing code to production)
  * After adding a breakpoint the page should be reloaded, which then re-run the js until the the breakpoint is reached
    * Where the breakpoint is set, the debugger highlights the code that is about to be executed
    * The 'Play/ Pause' step-through control will be highlighted in blue to indicate that the script is paused


  * [Docs: Breakpoints](https://developers.google.com/web/tools/chrome-devtools/javascript/breakpoints)
  * [Docs: Stepping Through Code](https://developers.google.com/web/tools/chrome-devtools/javascript/reference#stepping)
  * [Article: Using Code Snippets](https://www.alexkras.com/using-code-snippets-to-test-save-and-reuse-javascript-code-in-chrome-developer-tools/)
