# CSS Fundamentals

## Learning Goals

- Identify CSS syntax
- Identify CSS use formats
- Implement various types of CSS selectors
- Implement various types of color values in CSS
- Identify and implement CSS comments

## Introduction

In this lesson, we'll build on the basics we've learned. We'll learn to select
elements based on HTML attributes, we'll learn to apply colors, and we'll learn
how to comment our CSS.

## Identify CSS Syntax

Before we turn to the various ways we can extend CSS rules, let's go over the
foundational syntax CSS uses.

![](https://curriculum-content.s3.amazonaws.com/css-essentials/css-fundamentals/Image_43_ReCreateGraphic.png)

We create a CSS rule by defining the selector, which matches the HTML element we
want to style. Inside the curly braces we declare the properties we want to
change and, after the colon, we set the value we want to change that property
to. Each property is written in the following form: property name, colon, the
value for that property and a semicolon.

In the example above, we are selecting the `p` element and displaying its color
as blue.

## Identify CSS Use Formats

How do we "apply" CSS to an HTML page? By using one of three CSS use formats:
inline, internal (or embedded) and external.

Inline includes the styles directly into the HTML element with the `style`
attribute.

```
<p style="color: blue;"></p>
```

While you might see this sort of styling in something like the code for an HTML
email, this is generally not the best practice for two reasons. The primary reason
is because it only affects that single element. If we want all paragraph
elements on our page to appear blue, we would have to add that attribute to
every element individually, which is inefficient and difficult to maintain into
the future. That brings us to the second reason to avoid inline CSS: it breaks
our principle of separation of content and presentation.

Internal CSS is inside of `style` tags in the HTML document's `head` section.

```
<!DOCTYPE html>
<html>
  <head>
    <style>
      p { color: blue; }
    </style>
  </head>
  <body>

  <p>This is a paragraph.</p>

  </body>
</html>
```

This rule will display all paragraphs in this document as blue, which is a step
up in scope from the inline styles that only apply to single elements. But this
CSS will only apply to the single document. Other paragraph elements on other
pages in the same website will be unaffected.

If we want our CSS to carry across various pages, we can use an external
style sheet. This is a separate CSS file that we link in the `head` of HTML
documents.

```
<!DOCTYPE html>
<html>
  <head>
    <link rel="stylesheet" href="styles.css">
  </head>
  <body>

  <p>This is a paragraph.</p>

  </body>
</html>
```

With the `link` tag, we can use the relation attribute to define the target as a
style sheet and the link source our CSS file that contains all the CSS we want to
use on our site. This is by far the easiest way to link CSS to HTML and apply
styles across all of our pages.

## Implement Various Types of CSS Selectors

CSS gives us a wide range of ways that we can select elements on the page. Some
of these you will use more than others, but it's a good idea to know them all so
you can choose the right one when you need it.

### ID and Class Selectors

ID selectors target all elements with a specific ID attribute value. The way we
specify an ID selector in a CSS rule is to follow the element name with a
hash symbol and then the ID attribute value we want to match.

```
p#introduction {
  color: blue;
}
```

In this case, the browser will look for a `p` element with the ID attribute
"introduction" and apply the CSS to that element. ID selectors are useful when
you want to give a single element on the page a unique identity and set it
apart from everything else.

Class selectors target all elements with a class attribute value matching the
selector name. We specify a class selector using the period symbol followed by
the name value.

```
p.alert {
  color: red;
}
```

The difference between IDs and classes is that IDs are meant for one element on
the page that has a unique identity where class selectors are meant to be spread
throughout the page across multiple elements.

### Compound Selectors

Compound selectors let us apply the same CSS rules to multiple elements at once.
If we want to make both `h1` and `h2` elements display green, we use both as
selectors, separated with a comma.

```
h1, h2 {
  color: green;
}
```

This eliminates the need to rewrite a new CSS rule containing the same styles
for different elements.

### Descendant Selectors

Descendant selectors target elements that are descendants of the matching
selector name. A descendant selector is indicated by a space in between one
selector and another selector.

```
article p {
  color: blue;
}
```

In this case, _only_ `p` elements within the `article` element will receive the
styling.

ID, class, compound and descendant selectors are the kind of selectors you will
probably use in your CSS on a regular basis. From this point on, we get into
more advanced selectors. They are often not as necessary as the previous ones,
but they can accomplish some powerful operations.

### Child Selectors

The child selector targets all elements that are the immediate children of a
specified element.

```
article > p {
  color: blue;
}
```

Only `p` tags one level down from `article` will display as blue. If there are
`p` tags within an `aside` element within the `article` element, they will not
receive the same instructions.

### Adjacent Sibling Selector

The adjacent sibling selector targets elements that appear directly after the matching
selector name. We indicate it using a plus symbol.

```
h3 + p {
  color: blue;
}
```

Here the adjacent sibling selector will style the paragraph directly following an `h3`
element but not paragraphs that come after the first.

### General Sibling Selector

The general sibling selector (sometimes called the preceded selector) will style
all matched elements after the preceding selector name.

```
h3 ~ p {
  color: red;
}
```

With this general sibling selector, all paragraph elements that come after the
`h3` will receive the styling.

### Universal

The universal selector matches any elements and will apply to elements that are
not targeted by other rules. It's indicated by the star symbol.

```
* {
  color: yellow;
}
```

In this case, this is going to set the color of the text yellow for any element
that hasn't had its color property specified elsewhere.

### Attribute Selectors

The `attribute` selector can target elements with a particular attribute. We can
also define exactly which attribute we want to match.

```
input[type="text"] {
  width: 200px;
}
```

Here we want to find `input` elements, but only those with a `type` value that
matches "text." For those elements that fit the requirements, the browser will
then apply the width we want. There are many different ways to use this type of
selector with various combinations of operations and attribute values so you
can refer to the resources to explore them all.

### Pseudo-class Selectors

Pseudo-class selectors target elements based on a particular state of an element
or relationship to other elements. The way we signify a pseudo class selector is
with the colon symbol.

```
a:link {
  color: blue;
}

a:visited {
  color: purple;
}
```

These two link examples reflect the way links that are both unvisited and
visited will be displayed differently. If the link is unvisited, it will show as
blue. If it has been visited, it will show up purple. Pseudo-class selectors,
like attribute selectors, have a lot of aspects so you can explore them more in
other resources.

## Implement Various Types of Color Values in CSS

We've been using color names in our examples to keep it simple, but only a
handful of color names are recognized by all browsers. When writing CSS, we'll
be better off to use different ways of defining our colors.

#### Hexadecimal Color Values

Most often developers use a set of numbers called hexadecimal, which represents
a wide range of colors. Hex colors begin with `#` and are followed by,
generally, 6 numbers, but some of these numbers are actually letters. The lowest
single digit number in hex is 0 and the highest single digit number is f. This
table might help to visualize what we mean by this.

```
Decimal Numbers:      0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16
Hexadecimal Numbers:  0, 1, 2, 3, 4, 5, 6, 7, 8, 9,  a,  b,  c,  d,  e,  f, 10
```

Hex colors work by creating Red, Green, Blue (RGB) values. Traditional RGB
colors are on a scale of 0 to 255 for each of the three colors in the spectrum.
`#000000` translates to black since 0 reds, 0 green, 0 blues represents the
absence of all colors and `#ffffff` makes white since 255 reds, 255 greens, and
255 blues equal the maximum of each of the colors.

Hex colors can be shortened to just three numbers when each RGB value is the
same for each digit. So `#111111` can be written as `#111`.

### RGB Color Values

We can also work directly with RGB values.

```
p {
  color: rgb(255, 255, 255);
}
```

Here we've set our `p` elements to the color white, the maximum of all RGB
values (255).

You can also add an extra channel to your RGB color by setting an "a" value,
which represents opacity.

```
p {
  color: rgba(0, 0, 255, 0.5);
}
```

This example will show up as blue, with 50% opacity so the element will have a
somewhat transparent color.

## Identify and Implement CSS Comments

Sometimes developers want to put into their code information that helps other
humans understand what the code is doing but without bothering the browser. We
do this with comments, and CSS has its own way to mark up comments.

```
p.alert {
  color: #ff0000; /* Alert text displays red */
}
```

Everything in between the `/* */` is a CSS comment. The browser will not pay
attention to these comments, but they can be useful for us to add explanations
or reminders alongside our CSS code.

## Resources

- [MDN: CSS Tutorials for Beginners](https://developer.mozilla.org/en-US/docs/Web/Guide/CSS/Getting_started)
- [MDN: CSS Property Reference](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference)
- [MDN: CSS Inheritance](https://developer.mozilla.org/en-US/docs/Web/CSS/inheritance)
- [Tuts Plus: 30 CSS selectors to Memorize](https://code.tutsplus.com/tutorials/the-30-css-selectors-you-must-memorize--net-16048)
- [CSS Tricks: Learn More Pseudo Selectors](http://css-tricks.com/pseudo-class-selectors/)
- [MDN: Using Web Fonts](https://developer.mozilla.org/en-US/docs/Learn/CSS/Styling_text/Web_fonts)
- [Shay Howe: CSS Performance & Organization, Best Practices](http://learn.shayhowe.com/advanced-html-css/performance-organization/)
- [Adobe Color Tool](https://color.adobe.com/create/color-wheel/)
- [CSS Validator](http://jigsaw.w3.org/css-validator/)
- [CSS Diner Game](http://flukeout.github.io/)
- [CSS Tricks: Hue, Saturation and Lightness](https://css-tricks.com/yay-for-hsla/)

## Conclusion

We reviewed the specifics of CSS syntax and covered the different ways we can
connect CSS to HTML. We ran through the various types of CSS selectors,
including IDs, classes, compound, child, adjacent sibling, general sibling,
universal, attribute and pseudo-classes. We also took a look at the various ways
to express colors, from standard color names to hexadecimal and RGB values.
Lastly, we identified how to read and write CSS comments.
