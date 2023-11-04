---
layout: post
title: "Building A Roll20 Character Sheet Session 2: CSS Overview"
date: 2022-12-23 12:48 -0800
categories: [Tutorial, Roll20 Character Sheet Tutorial]
tags: [roll20, rpg, tutorial, web-dev, css]
permalink: tutorials/roll20-character-sheet/2
---

## CSS

If you missed Session 1, the overview of HTML, you can find it [here]({% link _posts/2022-12-22-building-a-roll20-character-sheet-1-md.md%}).

CSS is used to style HTML elements. There are two main parts to CSS: **Selectors** and **Styles**. A selector determines which element or elements you are styling, while a style determines how those selected elements appear. Styles can change things like color, size, borders, spacing between elements, and more.

> Before we jump in, I'm going to repeat my {% capture link_with_anchor %}{% link _posts/2022-12-22-building-a-roll20-character-sheet-0-md.md %}#technology{% endcapture %}
[earlier suggestion]({{ link_with_anchor }})
 that you grab a text editor like Notepad++, which can auto-complete some of the CSS properties you'll be using.
{: .prompt-tip}

A very simple example of CSS might look like this:

```css
 button {
    background-color: red;
    color: blue;
 }
```

This would select every button and make them look rather ugly, like this: <button class="demo" style="background-color:#cc241d; color: blue; ">Click me!</button>

Note a few things here: First we have our selector (`button`), then we wrap all of the properties inside curly a side of curly brackes `{}`. Each rule has the property name (`color`) followed by a colon (`:`) and the value (`blue`). Finally, each property ends with a semi-color (`;`). I know this syntax may be overwhelming, but it will become more natural over time. If you're ever concerned, you can paste your CSS code into an [online validator](https://www.cssportal.com/css-validator/).

> By the way, if you're wondering what values are allowed for a property (like how does it know what "blue" is?), there are lists online, or you can try out values yourself. When we get to using the Element inspector in session 4, you'll see how your web browser can suggest auto-completions for many of these properties.
{: .prompt-tip}

Now that you've seen a rough example, let's talk more about selectors and styles.

## Selectors

A selector chooses one or more elements. There are very simple selectors, like `button` that I used above. That selects every single button in the document. Sometimes you want to paint in broad strokes like that, but usually you'll want to style only a specific element, or a certain number of them. That's where selectors come in.

> You <b>can</b> style an element with the <code>style</code> attribute, like this: `<button style="color:blue; background-color: red"></button>`
<br><br>
I encourage you <b>not</b> to do this. It makes your HTML hard to read, is hard to track down errors, and can get awfully messy to edit once you have more than a couple properties in there.
{: .prompt-warning}

Selectors let you match against all elements of a given type, a specific element by id, all elements that share a class, OR elements based on their relationships in the hierarchy (more on this in session 5).

> When we actually start using Roll20, it will link your CSS file and your HTML files together for you. But if you'd like to try it out now, you have two options.
<br><br>
**First**, you can simply add a new section to the top of your HTML document called `<style></style>` and put all of your CSS code between those tags.
<br><br>
**Second**, you can include a link to your CSS file from your HTML by adding this:   `<link rel="stylesheet" href="styles.css">`. Change "style.css" to whatever you've named your CSS file. If your CSS file isn't in the same location as your HTML file, you'll need to change the href location to the correct file path.
<br><br>
Whichever approach you take, remember to remove it when we actually start testing in Roll20!
{: .prompt-info}

### The Element Selector

If you want to style all elements of one type, you can do that with the element selector. Simply type the element you want to style. For example, to style a button, you would simply use

```css
button {
    color: blue;
}
```

You probably don't want to do this too often, as it's unlikely that you want EVERY element of one type to look exactly the same. Plus, if you're working in Roll20, they provide some default stylings for most of the basic elements.

### The #ID Selector

If you're only styling a single element, you can select it with its `id`. As you remember from the [previous session]({% link _posts/2022-12-22-building-a-roll20-character-sheet-1-md.md%})  , `id` is an attribute you can provide to any HTML element to uniquely identify it.

This is useful if you have a one-off styling of an element, like adjusting the margins or font size of something that appears only once in your page.

To use the id selector, simply use `#` followed by the id you want to select.

To select the element `<button id="mySpecialButton">Click me</button>`, I'd use the following code

```css
#mySpecialButton {
    color: red;
}
```

As before, I can put whatever stylings I want inside the brackets.

### The Class Selector

Class selector is useful when you want to apply the same style to multiple elements. This should be one of the first tools you reach for.

To give an HTML element a class, just give it a `class` attribute, like so: `<button class="urgent"></button>`. You can even give multiple classes, separated by a space: `<button class="urgent big"></button>`

> <b>Note:</b> Generally, it's better to describe how a class is used, rather than what it does. For example I called the class "urgent" instead of "red", even though I might style it so the button is red. This allows me to easily change my mind later, if "urgent" should look different, and to do so without creating confusion.
{: .prompt-tip}

Then to select it, I simply put a `.` before the name of the class:

```css
.urgent {
    background-color: red;
}

.big {
    height: 150px;
    width: 300px;
    font-size: 40px;
    border: 10px solid black;
}
```

Such a button might look like this: 
<button class="demo" style="width:300px;height:150px;background-color: #cc241d;font-size:40px;border:10px solid black">Click me!</button>

The benefit of class selectors is that I can give another element the same class, and it will be styled in the same way. You can imagine, for example, that I might want all of my urgent buttons to be red, but only some of those urgent buttons should be big, and I might have a big button that isn't urgent.

Or maybe I want to apply `urgent` to something that isn't a button at all! I can make a div urgent: `<div class="urgent"> <p>Here is some urgent text!</p></div>`

which would render as:

<div class="example">
    <div style="background-color:#cc241d"> <p>Here is some urgent text!</p></div>
</div>

As you can see, classes enable consistent re-use. I can change ALL of the urgent elements at one time, and in one place.

#### Naming Classes

You can use almost **anything** as the name of a class, but beware: if you use a common name, it's likely that Roll20's built-in CSS may use the same names. For example, they have a class called `small`, so if you use that, you will end up with some properties set that you won't expect! To get around this, either use unique names, or prefix your class names with something to make them unique.

Classes cannot contain spaces nor start with a number. Popular convention is to use hphyens (<kbd>-</kbd>) in class names, like this: `<button class="my-button"></button>`

> <b>Have you made a ROll20 sheet before?</b>
<br> If so, you may remember having to start your custom CSS classes with "sheet-". Starting in 2021, Roll20 removed this requirement, and you can call your classes anything you'd like.
{: .prompt-warning}

### Combining Element and Class Selectors

What if I want to style different elements differently? For example, maybe I want all `urgent` items to be red, but I want paragraphs (`p`s) that are urgent to have bold text, while `button`s shouldn't be.

That's easy, you can combine an element selector (`p`) with a class selector (`.urgent`) to only apply stylings to certain elements with certain classes. 

All you have to do is put the class selector **immediately** after the element it should style, with no space, like this: `p.urgent`.

Behold:

```css
.urgent {
    background-color: red;
}
p.urgent {
    font-weight: bold;
}
```

and our HTML

```html
<button class="urgent">Click me, I am urgent but not bold!</button>

<p class="urgent">I sure hope someone reads all this bold text!</p>
```

this renders as:

<div class="example">
<button class="demo" style="background-color:#cc241d;">Click me, I am urgent but not bold!</button>
<p style="background-color:#cc241d; font-weight: bold; margin-top:5px;"> I sure hope someone reads all this bold text! </p>
</div>

This isn't just limited to any one class or any one element: you can style any combination of class and element in the same way.

> **Warning!** I mentioned before that your CSS must have no spaces between the element and the class. That's because (as we'll see in session 5) `p.urgent` is very different than<br> `p .urgent`.
<br><br>
The first matches all `p` elements with a class of urgent, while the second matches all urgent elements that appear inside of a `p`.
{: .prompt-danger}

### Can I match a specific type of input?

What if you just want to style the inputs that accept numbers, or just checkboxes?

While this is possible, I recommend using a class. The only reason I make that recommendation is because the syntax for styling a specific type of input can be a little intimidating, even moreso than "normal" CSS.

> <b>Warning: Advanced topic.</b> Most likely you want to take my advice and use a <code>class</code> selector for now. Feel free to skip this question and keep reading below. We'll cover this more fully in session 5.
{: .prompt-warning}

But, if you've braced yourself and wish not to heed my warnings, here you are:

```css
input[type="checkbox"] {
    width: 30px;
    height: 30px;
    accent-color: green;
}
```

Here is what you have wrought:
<input type="checkbox" style="width:30px;height:30px;accent-color:green;">

> *Note: accent-color is a fairly new property, and allows you to change the color of a checkbox when it is checked.*
{: .prompt-tip}

The above CSS **only** matches inputs that have a type of checkbox. So Radio buttons, text inputs, and numbers are all unaffected by this selector.

In addition to `[type=]`, we can also match on `[value=]`, and many other selectors, but hold onto this enthusiasm for the advanced section!

### What if there's a conflict?

It's certainly possible to have a rule that applies conflicting styles to the same element. If that's the case, CSS resolves it by specificity, then by order.

The more specific you are with your selector, the more likely it is to take precedence. An element selector (like `button`) has lower priority than a class selector (`.big-button`), which has lower priority than an id selector (`#ReloadButton`). When we get into Advanced selectors, you'll see how chaining these together chan change the specificity.

For now, you've seen that we can combine element and class selectors: know that `button.urgent` is more specific than either `button` or `urgent`.

If there's **still** a conflict after that, CSS will choose the last rule that was defined. So something that is defined early in your CSS file can be overwritten by something defined later, if they have the same specificity.

Consider this example:

```css
button {
    background-color: red;
    background-color: blue;
}
```

Here, the button would be blue, and not red, because blue is defined later.

#### !Important

Finally, there is a way that you can force a CSS rule to take precedence, **though I cannot recommend it.**

If you end a rule with `!important`, CSS will give priority to that rule. In this example, the button would be red, because the red rule is more important than the blue.

```css
button {
    background-color: red !important;
    background-color: blue;
}
```

That seems pretty useful, especially if you're butting heads with one of Roll20s pre-defined styles. So why do I recommend against it?

A few reasons:

* **Confusion**. The more of these you add to your code, the harder it is to figure out exactly where an element's stylings come from. You can mitigate this somewhat with the Element Inspector, which we'll discuss in session 4, but trust me on this for now.
* **Arms Race**. Once you mark something important, it's easy to get into a situation where something else is *more important*, so you mark that as important as well, and pretty soon everything in your CSS file is marked as important. Not only is that hard to follow, it's also meaningless. If everything's important, nothing is[^1]. 
* **Bad Practice**. You'll be grateful at the end of the day when you have a CSS file that's clean, with few (if any) `!important` declarations. It's easy to see at a glance exactly how a given element is styled, without having to worry if a property from some other, less specific, rule is taking precedent.

### Selector Summary

Those are the basic selectors. In session 5 we'll cover more advanced selectors, that allow you to match every other element, or just the first time something appears. We'll also cover how to combine these, so you can uniquely style an element that is both `urgent` and `confidential`, or maybe only matching elements that are `big`, while explicitly excluding those that are `urgent`.

 Most often, you should reach for class selectors, or id selectors if you need to style just a single element. There's no harm in having a class that's only applied to one element, so defaulting to adding a `class` is a good habit that will enable you to extend your work later on.

 Now that we know how to match elements, let's talk about some of the common properties we might want to set!

## Styles

When you style an element, you do it with a property. There are many properties available on every element, things that let you change the color, size, shape, font, and more!

Here are some of the common properties you'll likely be changing, as well as some of the values they support. Full documentation for all of these is available online.

### Color and Background-Color

You've already seen these used in examples above. Color changes the font color on most elements, while background-color changes the background.

There are a large number of built-in colors known (like <span style="color:aqua">aqua</span>, <span style="color:blue">blue</span>, <span style="color:red">red</span>, and <span style="color:green">green</span>), but you can also pass in any hex code (e.g. #34cceb for <span style="color:#34cceb">a light blue</span>), an RGB value (`color: RGB (52, 204, 235)`), or an RGBA value to add transparency (`color: RGBA(52, 204, 235, 11)`).

### Positioning and Display

Last session, I mentioned how the only difference between a `div` and a `span` is that the `div` is a block-level component, forcing other components to a new line, while `span` is an inline component, and plays nice, sharing its space.

You can set any element to behave in either way with `display: block` or `display: inline`.

More often, you'll want to adjust the positioning of an element relative to either its parent or to the entire sheet.

You can use `position: relative` or `position: absolute` to change an object's point of reference.

> I'll warn you though: You almost never want to use `position: absolute`, because it will not respect things like the page changing size.
{: .prompt-warning}

To change the position of an item, you can set its `top`, `left`, `right`, or `bottom` properties. For `relative` elements, this will move them compared to its parent. Here's an example:

```html
<div>
    <button class="clickable">Click Me</button>
</div>
```

Which renders like this.

<div class="example">
    <div>
        <button>Click Me</button>
    </div>
</div>

Now if we add some CSS:

```css
.clickable {
    position: relative;
    left: 100px;
}
```

You can see that the button moved to the right by 100 pixels.

<div class="example">
    <div>
        <button style="position:relative;left:100px;">Click Me</button>
    </div>
</div>

Instead of a number of pixels, you could provide a percent, like 50%. If I did that, the button would move so that the left edge is 50% of the parent div's width. This is not quite the same as centering the button, as you can see from this example:

```html
<div class="narrow">
    <button class="badCenter>Click me</button>
</div>
```

And the CSS. I'm setting the background color to blue purely for illustrative purposes.

```css
div.narrow {
    style: width:300px;
    background-color: #326ba8;
}

button.badCenter {
    position: relative;
    left: 50%
}
```

And what this renders:

<div class="example">
    <div style="width:300px;background-color:#326ba8">
        <button style="left:50%;position:relative;">Click me</button>
    </div>
</div>

As you can see, the **left** side of the button is in the center of the div, and the button is not centered.

There are better ways to center an element (using `display: flex`), but we'll talk about them in session 5.

> If you're wondering why I'm not just teaching the "better" way right now, I'll explain: CSS is complicated. There's a lot to learn. My goal with this guide is to give you as little information as you need to start making something fast. In the next two sessions we'll make a rough prototype of a character sheet (including the use of a technique I haven't shown you yet, `display: grid`). I'd rather you learn the basics and get something imperfect out that you can iterate on later.
<br><br>
>**Perfect is the enemy of good, and it's very easy to spend all your time perfecting a detail instead of finishing something.**
<br><br>
If you disagree with this approach, you can either skip ahead to section 5 or look up "display: flex" or "CSS how center element in div" on your own. Experimentation is the best way to learn.
{: .prompt-info}

### Width and Height

Width and height are fairly self-explanatory. They set the width and height of an element.

You can, of course, give a size in pixels (e.g `15px`), but you can also give it in %, which would expand to a given percent of the parent element's size.

It's worth noting that you **cannot** have any spaces in your CSS between the number and the unit: `15 px` will not work; it must be `15px`.

Additionally, you can provide `width: fit-content` to make an element only as wide as it needs to be. I find myself doing this a lot on labels, as Roll20's default labelling style makes them very wide indeed!

Finally, you can provide `min-width` and `min-height` with exactly the same parameters to ensure that your element cannot shrink beyond the values given.

### Font-Size, Font-Weight, Font-Variant, and Font-Family

It shouldn't be hard to guess what these do: `font-size` sets the size of your font. 

> While you can give a value in pixels (px), it's better for font sizes to use `rem`, which is short for "root element em", or the size of an M on the page's root element. The reason for this is that `rem` will scale better if your sheet is viewed on a different sized screen, like a phone. It's not **essential** that you follow this on Roll20, but keep it in mind, especially if you do further web development.
>
> Example: `font-size: 0.9rem;`
{: .prompt-tip}

`font-family` is used to set the font. You can give it multiple values in case one fails, but that shouldn't often be necessary. We'll talk about importing custom fonts into Roll20 later on. Example: `font-family: Helvetica;`. If your font is two words, you'll need to quote it: `font-family: "Times New Roman";` 

You can also give a value like serif, sans-serif, or monospace.

`font-weight` is used to set the boldness (or weight) of text. It has values like normal, bold, and light. Not every font supports every value. You can also give a value between 1 and 1000, where 1000 is the boldest possible, and 400 is normal. Example: `font-weight: bold;`.

`font-variant` is used to transform the font to a different style. Most often I use `font-variant: small-caps` to make my text appear in small caps, like this:

<div class="example">
    <h1 style="font-variant:small-caps">Look, it's small caps!</h1>
</div>

### Margins and Padding

**Margins** dictate the space between things, how they bump up to one another. You can set all of the margins at once, but I prefer being explicit and setting them with `margin-top`, `margin-left`, and so on.

Here are two buttons with no margin:
<div class="example">
    <button>Left button</button><button>Right button</button>
</div>

Now watch if I get the right button a margin-left of 50px:

<div class="example">
    <button>Left button</button><button style="margin-left:50px;">Right button</button>
</div>

**Padding** works very similarly, but you can think of it as the space *inside* of an element's border, rather than outside of it (note: this is true even if the element doesn't have a visible border.)

Let's look at that same example with our two buttons, but this time I'll give the right buttons a `padding-left` of 50px:

<div class="example">
    <button>Left button</button><button style="padding-left:50px;">Right button</button>
</div>

You can give a negative value for margins and padding as well, but I wouldn't make a habit of it.

Just like margin, you can set `padding-left`, `padding-bottom`, and so on, or set it all at once with `padding: 10px;`

### Borders

Borders are, well, the borders outside an element. You can set them to be transparent, or style them however you'd like. While you can set all of these properties all at once (`border: solid 3px black`), I find that beginners often prefer to set them explicitly:

`border-top: 3px;`
`border-color: red;`
`border-style: solid;`

If you don't want a border to appear, you can set its color as `transparent`.

The `border-style` property can take lots of options (dotted, dashed, double, and so on), but most of the time I use either `solid` or `none`.

I find the `border` property is especially useful when styling `<hr>` elements, which represent horizontal lines. The default styling is very faint.

One last popular border property is `border-radius`. In its most basic use, you can give a curve to a border. Give a value in px. Something like 4px gives a slight edge (see middle button below), while 30px gives a significant edge. You can get wild with [unusual shapes and contours](https://developer.mozilla.org/en-US/docs/Web/CSS/border-radius), but that's well outside the scope of this tutorial.

<div class="example">
    <button style="margin-left:10px;">No radius</button><button style="margin:10px; border-radius:5px;">5px radius</button><button style="border-radius:30px;">30px radius</button>
</div>

### Text align

Here's a straightforward one: set the alignment of the text in a given element to either `left`, `right`, `justify`, or (most popular), `center`.

<div class="example">
    <button style="margin-left:10px;text-align:left;width:100px">Left</button>
    <button style="margin:10px; width:100px; text-align:center">Center</button>
    <button style="width:100px;text-align:right">Right</button>
</div>

Justify is more subtle unless you have several lines of text. It will put space between the words so that they start and end by filling up the allotted space. You probably don't want this.

<div class="example" style="text-align:justify">
    Lorem ipsum dolor sit amet, consectetur adipiscing elit. Phasellus imperdiet, nulla et dictum interdum, nisi lorem egestas odio, vitae scelerisque enim ligula venenatis dolor. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Phasellus imperdiet, nulla et dictum interdum, nisi lorem egestas odio, vitae scelerisque enim ligula venenatis dolor.
</div>

### Styles Summary

There are hundreds of CSS properties, and I only give the most basic here. If you've got something you want to try, go to your favorite search engine and type it in followed by "CSS". Chances are you'll find some people talking about it.

I'm not going to cover animation or anything like this (it seems rather outside the scope of a series about making character sheets! But know that this too can be accomplished with CSS.)

## Summary

By now, you should have a rough understanding of both HTML elements and common CSS properties and basic selectors. Grab some water, take a stretch, and then let's continue on with the reason we're here: putting it all together in Roll20.

In the [next session]({% link _posts/2022-12-24-building-a-roll20-character-sheet-3.md%}), we'll look at some Roll20-specific oddities and rules, and get a very basic character sheet loaded. Then, in session 4, we'll actually start layout out the skeleton for our character sheet.

Lucky for your, this was the last of the info-dump posts, at least for a while. [Onward!]({% link _posts/2022-12-24-building-a-roll20-character-sheet-3.md%})


[^1]: That's the plot of The Incredibles.
