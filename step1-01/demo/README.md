# Step 1.1 - Introduction to HTML (Demo)

## How the web works

A simple web page is rendered on the screen via the following simplified steps:

> A detailed explanation is available [here](https://github.com/alex/what-happens-when)

1. You instruct the browser which web page you'd like to see by typing a URL in the address bar.

   - We'll use the URL ([Uniform Resource Locator](https://en.wikipedia.org/wiki/URL)): `https://chanzuckerberg.com` as an example.

2. The browser looks up the URL on a DNS ([Domain Name System](https://en.wikipedia.org/wiki/Domain_Name_System)) server

   - This is like a big phone book for website server addresses
   - DNS server then returns the website server IP address (e.g., `102.3.45.6`) back to the browser

3. The browser uses the IP to connect and ask the website to send over the specific page you've requested.

   - E.g., Requesting for the website `https://chanzuckerberg.com` is short for `https://chanzuckerberg.com/`, which by default returns the homepage (`index.html`) at the root of the application directory

4. The server sends the HTML file back to the browser

5. The browser first does a `preload scan` of the HTML file, so it can find all the additional resources linked to the page and start fetching them, while executing the next parsing step. The common resources are:

   - Fonts
   - Images
   - CSS stylesheets
   - JavaScript(JS)

   > Note: Resources like CSS and JS might request even more files after parsing. For example, a JS file, once downloaded and executed, can add more script/link tags in HTML at runtime to make the browser request additional files it depends on. And a CSS file can request more fonts and images too

6. The browser then parses the HTML file from the top to the bottom to construct the Document Object Model ([DOM](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model/Introduction)), which is a representation of the HTML structure in JavaScript. And in parallel, it also constructs ([CCSOM](https://developer.mozilla.org/en-US/docs/Web/API/CSS_Object_Model)), which is the DOM equivalent for CSS.

   Lastly, combining DOM and CSSOM produces the Render Tree, which represents what HTML elements get shown on the page

   - The order of CSS and JS resources listed in the HTML affects the render time for the Critical Rendering Path. The following chart shows how the second `building DOM` is blocked by `JS execution`, which in turn is blocked by `build CSSOM` (more details [here](https://hacks.mozilla.org/2017/09/building-the-dom-faster-speculative-parsing-async-defer-and-preload/)):

   ![Render blocking chart](https://2r4s9p1yi1fa2jd7j43zph8r-wpengine.netdna-ssl.com/files/2017/09/blocking-bold@2x-1.png)

   - The general rule of thumb is to put all CSS resources at the top inside the `<head>` tag, and JS resources at the bottom inside of the `<body>` tag.

     The reason is because the browser cannot render the page until HTML is parsed, DOM is constructed, and **ALL** CSS files are parsed. So since fetching/parsing/executing JS resources blocks HTML parsing, moving JS resources to be near the bottom of the `<body>` tag means the browser gets to construct the DOM faster, and therefore render the first paint of the page faster, and can execute the JS afterwards

   - However, things can get more complicated if you have **noncritical CSS** that is not needed for the first paint and/or **critical JS** that is needed for the first paint. In that case, you can learn more about optimizing Critical Rendering Path [here](https://hacks.mozilla.org/2017/09/building-the-dom-faster-speculative-parsing-async-defer-and-preload/) to see what optimization can be done. And it also helps to reach out to your coworkers or developer community for discussion!

7. Once the browser gets to the bottom of the page it can start working on rendering, and then display the page

> If you want a deep dive on how browser works, click [here](https://blog.logrocket.com/how-browser-rendering-works-behind-the-scenes-6782b0e8fb10/)

> If you want a deeper dive, click [here](https://www.html5rocks.com/en/tutorials/internals/howbrowserswork)

## HTML Syntax

HTML tags are the basis of all web applications. They give the page structure and define the content within.

An HTML tag takes the following form:

```html
<tag class="foo" onclick="myFunction()" otherAttributes="values"></tag>
```

1. [`class`](https://www.w3schools.com/html/html_classes.asp) is an HTML attribute and is used to define styles for elements with the same class name. So, all HTML elements with the same class attribute will get the same styling rules. You can also chain multiple CSS classes in one element to get aggregated styling. Like so:

   ```html
   <tag class="foo bar"></tag>
   ```

   Note that the order of class names `foo` and `bar` in the HTML attribute doesn't matter. So `class="foo bar"` and `class="bar foo"` get the same aggregated styling rules. However, the last defined class in the stylesheet wins, as demonstrated below:

   `Thistle` wins:

   ```css
   .foo {
     background-color: ForestGreen;
   }

   .bar {
     background-color: Thistle;
   }
   ```

   `ForestGreen` wins:

   ```css
   .bar {
     background-color: Thistle;
   }

   .foo {
     background-color: ForestGreen;
   }
   ```

2. [`onclick`](https://www.w3schools.com/tags/ev_onclick.asp) is an event listener that takes a JavaScript function as a callback, which the browser calls the function when the element sends a click event

3. Here is the [full list](https://www.w3schools.com/tags/ref_attributes.asp) of HTML attributes

The [HTML demo page](https://microsoft.github.io/frontend-bootcamp/step1-01/demo) shows a large collection of HTML elements that you will come across during development. The full list of elements can be found on [MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Element).

## Sample webpage

```html
<!-- Tells the browser which version the HTML syntax this file uses. E.g., HTML5 -->
<!-- https://www.w3schools.com/tags/tag_doctype.asp -->
<!DOCTYPE html>

<!-- Indicates the root of the HTML structure -->
<!-- https://www.w3schools.com/tags/tag_html.asp -->
<html>
  <!-- Indicates the head section that hosts all head elements,
  which contain machine-readable information (metadata) about the document -->
  <!-- A list of head elements can be found here: https://www.w3schools.com/tags/tag_head.asp -->
  <head>
    <!-- Page title on your browser tab -->
    <!-- https://www.w3schools.com/tags/tag_title.asp -->
    <title>Frontend Bootcamp</title>
    <!-- Indicates a linked resource to this HTML page. In this case, it's a CSS file -->
    <!-- https://www.w3schools.com/tags/tag_link.asp -->
    <link rel="stylesheet" href="./style.css" />
  </head>
  <!-- Indicates the body section that hosts all body elements -->
  <body>
    <!-- Indicates a container for introductory content or a set of navigational links -->
    <!-- https://www.w3schools.com/tags/tag_header.asp -->
    <header>
      <!-- h stands for heading, you can use h1 to h6, where 6 is the smallest size -->
      <!-- https://www.w3schools.com/tags/tag_hn.asp -->
      <h1>Frontend Bootcamp</h1>
      <!-- Defines a set of major navigation links -->
      <!-- https://www.w3schools.com/tags/tag_nav.asp -->
      <nav>
        <!-- Defines an unordered (bulleted) list -->
        <!-- https://www.w3schools.com/tags/tag_ul.asp -->
        <ul>
          <!-- Defines a list item -->
          <!-- https://www.w3schools.com/tags/tag_li.asp -->
          <li>
            <!-- Defines a link to another page -->
            <!-- https://www.w3schools.com/tags/tag_a.asp -->
            <a href="./about.html">About This Workshop</a>
          </li>
          <li>
            <a href="./participate.html">Take This Workshop</a>
          </li>
          <li>
            <a href="./contribute.html">Contribute to This Workshop</a>
          </li>
        </ul>
      </nav>
    </header>
    <!-- Defines the main content of the document -->
    <!-- https://www.w3schools.com/tags/tag_main.asp -->
    <main>
      <h2>About This Workshop</h2>
      <!-- Defines a paragraph -->
      <!-- https://www.w3schools.com/tags/tag_p.asp -->
      <p>
        The first section provides an introduction to the fundamentals of the web: HTML, CSS and JavaScript.
      </p>
      <!-- Defines an image -->
      <!-- https://www.w3schools.com/tags/tag_img.asp -->
      <img src="../../assets/todo_screenshot.jpg" alt="Picture of the Todo App we will build" />
      <p>
        The second section dives into more advanced topics like TypeScript, testing, and state management.
      </p>
    </main>
    <!-- Defines the footer of the document -->
    <!-- https://www.w3schools.com/tags/tag_footer.asp -->
    <footer>
      <h2>Get More Information</h2>
      <ul>
        <li>
          <a href="https://www.google.com/search?q=kittens&tbm=isch">
            Kittens 😸
          </a>
        </li>
        <li>
          <a href="https://www.google.com/search?q=puppies&tbm=isch">
            Puppies 🐶
          </a>
        </li>
        <li>
          <a href="https://www.google.com/search?q=baby%20chicks&tbm=isch">
            Chicks 🐤
          </a>
        </li>
      </ul>
    </footer>
  </body>
</html>
```
