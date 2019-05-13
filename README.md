# CSS: The Box Model

Slides and notes available at [https://github.com/jensen/css-notes/](https://github.com/jensen/css-notes/)

## Client Side Web Technology

This week we focus on HTML, CSS and JavaScript. There are two common models for delivering a client application to the browser.

1. Each request to the server returns HTML that the browser renders. The server is setup to serve multiple pages.
2. The initial request that the user makes retrieves the HTML, CSS and JS that contains the application code. Further requests retrieve data and the DOM is updated. Can be referred to as a 'SPA' or single page application.

Last week you used the first approach to make the client portion of TinyApp. You didn't spend a lot of time with CSS and client side JS. Instead templates were created and executed on the server side to generate dynamic pages with HTML.

### Tweeter

The project this week is a single page application. We will start by using CSS to style the user interface. Then we will use jQuery to manipulate the DOM and Ajax to retrieve data without requiring a browser refresh.

Later in the week the assignments will take you through the process of refactoring the server to use a database.

## Semantic HTML

HTML has nothing to do with the way a document looks. HTML allows us to provide context to the content in a document. HTML5 has a number of semantic elements. This means that we can use HTML to highlight the meaning of content. Tags like `<article>`, `<nav>` and `<footer>` are good examples of this. It's not a bad idea to check what tags are available on [MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Element).

This is an example of a basic HTML template to start with.

```html
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width,initial-scale=1.0">
  <title></title>
</head>
<body></body>
</html>
```

- `<!doctype html>` Render the document in 'standards' mode
- `<html></html>` The entire document must be wrapped in exactly one html tag
- `lang="en"` Recommended by [W3C](https://www.w3.org/International/questions/qa-html-language-declarations) to declare the language of the document
- `<head></head>` Contains exactly one head tag that contains meta information that describes the contents of the body tag
- `<meta charset="utf-8">` Avoid some bugs due to not specifying the document encoding
- `<meta name="viewport" content="width=device-width,initial-scale=1.0">` Responsive design stuff
- `<title></title>` The title of the document, show in the tab
- `<body></body>` Contains exactly one body tag that describes anything you want to be visible

## Cascading Style Sheets

The technology that we use to define the way that the documents looks is CSS. The term 'Cascading' describes the behaviour where styles applied to one element are inherited by it's children.

```html
<html>
  <body>
    Content
    <div>
      Content
      <p>Content</p>
    </div>
  </body>
</html>
```

```css
html {
  background-color: mediumaquamarine;
  color: floralwhite;
}

body {
  border: 4px solid darkorange;
}

div {
  background-color: darkslategray;
  color: darkorange;
}

p {
  color: floralwhite;
}
```

With this example we set the color of all content within the `html` tag to 'floralwhite'. That means that the content within the body tag will also be white. We set the color of the content within the `div` to 'darkorange', and back to 'floralwhite' in the `p` tag. Some properties like `border` need to be applied specifically to each tag that needs a border.

Load `cascade.html` into the browser and check the Chrome Developer Tools to see how the styles are applied.

## Defining Styles

It is impossible to learn CSS in a day. Don't expect to be comfortable with it by the end of the week. If CSS is something you want to focus on for your job then you will need to spend a lot of time practicing. A good place to start is the [CSS](https://developer.mozilla.org/en-US/docs/Web/CSS) documentation on MDN.

There are a few ways to define styles within a document.

1. Use a `<style>` tag in the `<head>`.
2. Use a `<link>` tag in the `<head>`.
3. Provide a style attribute to an element.

Each of these approaches has a purpose. The approach that you will use most often includes external style sheet documents with a `<link>` tag.

## Boxes

It's all boxes. We can see this by opening the console and applying a new style to any document.

```javascript
var style = document.createElement('style')
document.querySelector('head').append(style)

style.innerHTML = `
* {
  outline: solid 1px red;
}`
```

All of the elements should have a red border. This highlights the box model.

## The Syntax

The ability to style something depends on what style [properties](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference) are supported by the browser. Properties can have values assigned to them. If we want to set the background colour for something that contains that property we can assign it `background-color: #fff`.

If we want to provide multiple declarations, we can separate them with a semi-colon `background-color: #fff; color: #000`. This works well for assigning styles directly to elements with the style attribute. We want to avoid doing this, since it doesn't scale very well.

Instead a good approach is to setup a rule. A rule allows us to provide one or more selectors to match. We can use a declaration block to group a series of declarations.

```css
/*
selector list {
  property: value;
}
*/

div, p {
  color: black;
}
```

More details available on [MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/Syntax).

## The Box Model

There are 5 properties that contribute to the sizing and layout of an element.

- Content: Area that contains the content.
- Padding: The whitespace between the content and the border.
- Border: A border around the element.
- Margin: The whitespace around the border.
- Position: More on this later.

There are `width` and `height` properties that affect the size of the content area. When setting the `padding` or `margin` you need to define the values for the top, right, bottom and left sides of the box.

```css
nav {
  padding-top: 100px;
  padding-right: 200px;
  padding-bottom: 300px;
  padding-left: 400px;
}
```

If the padding is meant to be the same all the way around the box, then you could use a shorthand property.

```css
nav {
  padding: 100px;
}
```

It's also possible to set multiple values with a shorthand property. The order for the properties is top, right, bottom and left. The acronym __TRBL__ is a good way to remember this.

```css
nav {
  padding: 100px 200px 300px 400px;
}
```

More [shorthand properties](https://developer.mozilla.org/en-US/docs/Web/CSS/Shorthand_properties) can be used to reduce the amount of typing.

## Block-level vs. Inline

We can specify how we want an element to behave within the layout. The two primary settings for the `display` property are 'block' and 'inline'. There are a lot of other options too. To start just focus on understanding the difference between 'block' and 'inline'.

- [Block-level elements](https://developer.mozilla.org/en-US/docs/Web/HTML/Block-level_elements) can have a width and a height. Consecutive block-level elements will each break to their own line. The display property is set to 'block' by default.
- [Inline elements](https://developer.mozilla.org/en-US/docs/Web/HTML/Inline_elements) cannot have their width and height set. Inline elements do not break to a new line, they will flow with the text around them. The display property is set to 'inline' by default.

More on [MDN CSS Display](https://developer.mozilla.org/en-US/docs/Web/CSS/display).

### Inline Block

The inline-block flows with surrounding text like an inline element. It can also be sized with width and height like a block-level element. This improves our options when creating layouts. See the `blockfloat.html` example for usage.

## Box Sizing

It's important to bring up the topic of the `box-sizing` property. CSS originally implemented the sizing of elements as `content + padding + border`.

```css
div {
  width: 100px;
  height: 100px;
  padding: 20px;
  border: 10px solid black;
}
```

When inspecting this div in the developer tools it is reported that this box is 160x160 pixels. If we want the div to size based on width and height with padding and borders included we can set the `box-sizing` property.

```css
div {
  box-sizing: border-box;
}
```

Now when the box is being sized it will only take up 100x100px of space.

```css
* {
  box-sizing: border-box;
}
```

It would be more common to apply it to all elements with a wildcard like `*`.

## CSS Resets

Browsers have their own 'user-agent' stylesheets. These are the default styles applied to HTML tags. Not all browsers apply the same base set of styles. You can spend a lot of time altering your styles to ensure defaults are overridden.

A better approach is to use a CSS reset to ensure that the same base styles are applied to all elements for all browsers.

A reset can be relatively simple like the one created by [Eric Meyer](http://meyerweb.com/eric/tools/css/reset/). Another popular one 'normalizes' the stylesheets across browsers. It's called [Normalize.css](https://necolas.github.io/normalize.css/). You can either link it from a CDN or download the reset code into a local file.

## Layouts with float?

When the `float` property was introduced its intended use was newspaper style content layout. Images would be [floated](https://developer.mozilla.org/en-US/docs/Web/CSS/float), and text would wrap around them. As design on the web evolved `float` became the most popular approach to building column based [layouts](https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Floats).

[All About Floats](https://css-tricks.com/all-about-floats/)

### Clearing Floats

Any element that is below the floats that isn't floated itself will wrap around the floated elements. The way to resolve this is the clear the floats.

```css
div.clear {
  clear: both;
}
```

The `clear` property can take three values.

- `left`: clear left floats
- `right`: clear right floats
- `both`: clear left and right floats

Another approach is to apply a 'clearfix' to the parent of the floated elements. Now you don't have to remember to add an extra element after the floats. The 'clearfix' hack has been around for a long time. It's imeplementation has changed as older browsers no longer get used. With modern browsers there are alternatives to using floats for layouts.

__Ladies & Gentlemen, the clearfix.__

```css
div.row::after {
  content: "";
  display: table;
  clear: both;
}
```

The clearfix uses a [pseudo-element](https://developer.mozilla.org/en-US/docs/Web/CSS/pseudo-elements). This is a topic that needs to be skimmed for now and then learned after the basics are well understood. The [pseudo-class](https://developer.mozilla.org/en-US/docs/Web/CSS/pseudo-classes) falls into the same category.

### A Flexible Alternative

Flexbox is an alternative to float and clear. It has been designed to allow for layouts that flow vertically or horizontally. This is the modern approach I would recommend. It was designed to solve the column layout problem.

[Flexbox Browser Support (97.76%)](https://caniuse.com/#search=flexbox)

## Learning More

There are a lot of resources for CSS. It is very easy to fall into the habit of finding someone elses example. Copying it and pushing it around until it works for you. It may seem like this is an easier solution than actually learning CSS. CSS is one area that you can get yourself into trouble with bad early decisions.

Just like anything it will take time, and just like anything it feels more complicated than it actually is.

- https://css-tricks.com/
- http://guyroutledge.github.io/box-model/
- http://learnlayout.com/
- http://alistapart.com/topic/css
- https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Grid_Layout
- http://getbem.com/

We aren't worrying about the latest CSS frameworks at this point. There are also a lot of popular tools like Sass that we can work with later.

## Bonus

You are going to notice that when you search for HTML, CSS and JavaScript keywords the primary results will be from W3Schools. Avoid these results. Anytime you search for something add the term 'MDN' for Mozilla Developer Network documentation. Even better would be to use the search at [developer.mozilla.org](https://developer.mozilla.org/).

Good search engine optimization doesn't mean good documentation. The W3Schools material is likely to include the information you need. In my opinion it doesn't provide the same quality of information and provides a dated user experience.

Google helps us find a lot of good information. It is important to start recognizing the difference between good and bad documentation. Clicking on the first returned result without considering the source is a good habit to __break__.
