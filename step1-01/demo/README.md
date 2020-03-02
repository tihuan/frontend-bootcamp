# Step 1.1 - Introduction to HTML (Demo)

## How the web works

A simple web page is rendered on the screen via the following simplified steps:

> A detailed explanation is available [here](https://github.com/alex/what-happens-when)

1. You instruct the browser which web page you'd like to see by typing a URL in the address bar.

   - We'll use the URL ([Uniform Resource Locator](https://en.wikipedia.org/wiki/URL)): `https://chanzuckerberg.com` as an example.

2. The browser looks up the URL on a DNS ([Domain Name System](https://en.wikipedia.org/wiki/Domain_Name_System)) server

   - This is like a big phone book for website server addresses
   - DNS server then returns the website server IP (e.g., `102.3.45.6`) address back to the browser

3. The browser uses the IP to connect and ask the website to send over the specific page you've requested.

   - E.g., Requesting for `https://chanzuckerberg.com` is short for `https://chanzuckerberg.com/`, which by default will return `index.html` at the root of the application directory

4. The server sends the HTML file back to the browser

5. The browser first does a `preload scan` of the HTML file, so it can find all the additional resources linked to the page and start fetching them, while executing the next parsing step. The common resources are:

   - Fonts
   - Images
   - CSS stylesheets
   - JavaScript(JS)

6. The browser then parses the HTML file to construct the Document Object Model ([DOM](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model/Introduction)), which is a representation of the HTML structure in JavaScript. And in parallel, it also constructs ([CCSOM](https://developer.mozilla.org/en-US/docs/Web/API/CSS_Object_Model)), which is the DOM equivalent for CSS.

   Lastly, combining DOM and CSSOM produces the Render Tree, which represents what HTML elements get shown on the page

   - The order of CSS and JS resources listed in the HTML affects the render time for the Critical Rendering Path. The following chart shows how the second `building DOM` is blocked by `JS execution`, which in turn is blocked by `build CSSOM` ([source](https://hacks.mozilla.org/2017/09/building-the-dom-faster-speculative-parsing-async-defer-and-preload/)):

   ![Render blocking chart](https://2r4s9p1yi1fa2jd7j43zph8r-wpengine.netdna-ssl.com/files/2017/09/blocking-bold@2x-1.png)

   - The general rule of thumb is to put all CSS resources at the top inside the `<head>` tag, and JS resources at the bottom inside of the `<body>` tag. The reason is because the browser cannot render the page until **ALL** CSS files are parsed. And since fetching/parsing/executing JS resources blocks HTML parsing, moving JS resources to be near the bottom of the `<body>` tag means the browser gets to render the first paint of the page faster, and can execute the JS afterwards

   - However, things can get more complicated if you have **noncritical CSS** that is not needed for the first paint and/or **critical JS** that is needed for the first paint. In that case, you can learn more about optimizing Critical Rendering Path [here](https://hacks.mozilla.org/2017/09/building-the-dom-faster-speculative-parsing-async-defer-and-preload/) to see what optimization can be done. And also helps to reach out to your coworkers or developer community for discussion!

7. Browser makes requests for additional resources

   - Those resources might request even more files

8. Once the browser gets to the bottom of the page it can start working on rendering, and then display the page

![MDN Page Load](https://user-images.githubusercontent.com/1434956/53033758-9da8d580-3426-11e9-9ab8-09f42ccab9a8.png)

> If you want a deep dive on how browser works, click [here](https://blog.logrocket.com/how-browser-rendering-works-behind-the-scenes-6782b0e8fb10/)

> If you want a deeper dive, click [here](https://www.html5rocks.com/en/tutorials/internals/howbrowserswork)

## HTML demo

HTML tags are the basis of all web applications. They give the page structure and define the content within.

An HTML tag takes the following form:

```html
<tag class="foo" onclick="myFunction()" otherAttributes="values"> </tag>
```

HTML tags can also be nested to create a tree that we call the [Document Object Model](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model/Introduction).

The [HTML demo page](https://microsoft.github.io/frontend-bootcamp/step1-01/demo) shows a large collection of HTML elements that you will come across during development. The full list of elements can be found on [MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Element).

## Sample webpage

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Frontend Workshop: By Micah Godbolt and Ken Chau</title>
    <link rel="stylesheet" href="./style.css" />
  </head>
  <body>
    <header>
      <h1>Frontend Workshop</h1>
      <nav>
        <ul>
          <li><a href="./about.html">About This Workshop</a></li>
          <li><a href="./participate.html">Take This Workshop</a></li>
          <li><a href="./contribute.html">Contribute to This Workshop</a></li>
        </ul>
      </nav>
    </header>
    <main>
      <h2>About This Workshop</h2>
      <p>
        The first day provides an introduction to the fundamentals of the web: HTML, CSS and JavaScript.
      </p>
      <img src="../../assets/todo_screenshot.jpg" alt="Picture of the Todo App we will build" />
      <p>
        On the second day we'll dive into more advanced topics like TypeScript, testing, and state management.
      </p>
    </main>
    <footer>
      <h2>Get More Information</h2>
      <ul>
        <li><a href="https://github.com/Microsoft/frontend-bootcamp"> Frontend Bootcamp </a></li>
        <li><a href="https://twitter.com/micahgodbolt"> @micahgodbolt </a></li>
        <li><a href="https://twitter.com/kenneth_chau"> @kenneth_chau</a></li>
      </ul>
    </footer>
  </body>
</html>
```
