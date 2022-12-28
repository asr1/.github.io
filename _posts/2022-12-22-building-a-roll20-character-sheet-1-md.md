---
layout: post
title: "Building A Roll20 Character Sheet Session 1: HTML Overview"
date: 2022-12-22 14:25 -0800
categories: [Tutorial, Roll20 Character Sheet Tutorial]
tags: [roll20, rpg, tutorial, web-dev, html]
permalink: tutorials/roll20-character-sheet/1
---

## The Basics

If you've never made any kind of website before, this is a rough overview of the tools that are used, and how to use them. This post focuses on the fundamental building blocks of HTML. If you're familiar with web design (including things like using `<b>bold text</b>` to bold text), it's likely that you'll be able to skim or skip most of this section.

This post covers the very basics of HTML, which are universally used in web development. I'll get into Roll20-specific material in the [third session]({% link _posts/2022-12-24-building-a-roll20-character-sheet-3.md%}).

Table of Contents (also available on the right)
- [HTML Overview](#html-overview)
  - [Attributes](#attributes)
- [HTML Elements](#html-elements)
  - [Essential Elements](#essential-elements)
    - [Div](#div)
    - [Span](#span)
    - [Input](#input)
    - [Label](#label)
    - [Button](#button)
  - [Other Useful Elements](#other-useful-elements)
    - [Select](#select)
    - [H1, H2, H3...](#h1-h2-h3)
    - [HR](#hr)
    - [BR](#br)
    - [Bold, Underline, Italics](#bold-underline-italics)
    - [P](#p)
    - [Textarea](#textarea)
    - [img](#img)
- [Summary](#summary)

# HTML Overview

[HTML](https://www.w3schools.com/html/) dictates how your page is set up. You can think of it as determining the hierarchy of your page, and the elements within.

HTML elements are wrapped in angular brackets and are called **tags**. Typical code looks like this (see below). Notice that most opening tags (`<div>`) have a paired closing tag (`</div>`).

```html
<div>
    <button class="mybutton">Click me!</button>
    <label>Name</label>
    <input type="text"/>
</div>
```

The above will render like this:
<div>
    <button class="mybutton">Click me!</button>
    <label>Name</label>
    <input type="text"/>
</div>

<hr>

If you've never used HTML before, there's a few things to note. First, the outer `div` element is considered to be the **parent** of the `button`, the `label`, and the `input`. The `button`, `label`, and `input` elements are all **siblings**. HTML is set up like a hierarchy, so keeping track of parent and sibling relationships will be important when we [get to CSS]({% link _posts/2022-12-23-building-a-roll20-character-sheet-2-md.md%}).

The second thing you might notice is that the `input` tag doesn't have a closing `</input>`. `input` is special, and doesn't need one. Instead, it's closed with `/>`. Don't worry if you forget the `/>` and close it with `>` instead, it'll work just the same. The web is designed to be resilient to mistakes like these, but it's best practice to do it "right" anyway.

Third, you may notice that the `label` and `button` elements have content within them. Most tags contain content. The   `label` containing text is no different than the `div` containing other elements.

## Attributes

 Both the `input` and `button` elements contain attributes. **Attributes** are used to give information to elements, like the source (`src`) of an `img` tag to display an image.

 The `input` element has an attribute of  `type="text"`, while the `button` has `class="mybutton"`. On an input, `type` is how you differentiate between the various ways a user might provide input (text field, number field, radio buttons, checkmarks). You can see more about this in the [Input section](#input) below.

You can think of  `class` as custom categorization tag that is used for styling elements with CSS. Elements can have any number of classes, each one separated by a space (`<button class="btn red wide tall"></button>`) We'll talk more about styling in the [next post in this series]({% link _posts/2022-12-23-building-a-roll20-character-sheet-2-md.md%}).  

The most common attributes you'll see are `style` and `class` for applying CSS, `name` for storing data to Roll20, and `value` for setting initial values.

The most important attribute is `id`, which is used to **uniquely** identify an element. No two elements should share an id. Most elements don't *need* an id (though it never hurts to have one), but all `input`s should have an id.

When you pair an `input` to a `label`, you can use the `for` attribute to pair the label and the input together. See [Input (below)](#input) for more information. Ids can also be used to style individual elements with CSS.

Attributes **cannot** have spaces in them. Instead use hyphens (-) or camelCase. While underscores (_) are allowed by HTML, Roll20 is not compatible with certain attributes containing underscores, so I recommend you avoid them entirely.

I'll talk more about Attributes in a future section.

> **Note:** There's some unfortunate overlapping in naming here. HTML uses the word "attribute" to mean additional information (like class, id, or name) that's passed into an HTML element. 
<br><br>
Roll20 uses the word "attribute" to mean any piece of data that is associated to a character (it's name, HP, Strength, etc.) I will try to be clear in my usage about which I am referring to.
{: .prompt-warning}

# HTML Elements

You may be familiar with the \<b>, \<u>, and \<i> tags, which are used to **bold**, <u>underline</u>, and <i>italicize</i> text (respectively). If you are, great! That's an excellent touchstone for the syntax of HTML.

Below I'll cover the most common fundamental building blocks that you'll be using in your Roll20 Character sheet (or in most web sites you build).

The most important elements you be using are `div`, `span`, `input`, `label`, and `button`. I'll cover a few others as well, but don't worry about them too much for now.
 
## Essential Elements

### Div

A `div` is the basic building block of HTML. Think of it like a generic container. If there's any elements you want to group together, a `div` is a good way to group them.

By default, `div`s have a display type of `block`. This means that it tries to take as much space as possible, and forces itself and the content after it to display on a new line. This behavior can be changed, but if you want content to display [inline](https://www.w3schools.com/cssref/pr_class_display.php), a `span` may be the tool you want.

You can see more examples of display types at [w3 Schools](https://www.w3schools.com/cssref/tryit.php?filename=trycss_display).

### Span

A `span` is just like a `div`, expect that it defaults to inline display, meaning it blends in with the rest of the elements. This is useful, for example, if you want to style part of a paragraph.

```html
    <p>Some of these words are <span style="color:red">red</span>,
    while others are <span style="color:blue">blue</span>.</p>
```

Notice how there are multiple `span`s within one `p` (paragraph) tag.

This would render like this:

<p>Some of these words are <span style="color:red">red</span>, while others are <span style="color:blue">blue</span>.</p>

<hr>

If we had chosen to use `div`s instead, the sentence would have looked like this:

<p>Some of these words are <div style="color:red">red</div>, while others are <div style="color:blue">blue</div>.</p>
<hr>

It's entirely possible to change this behavior, so the important thing to remember is that `div`s and `span`s are just containers for grouping things together.

### Input

Input tags are the way that you get data from your users. These will need at least two attributes: a `type` and a `name`.

The type determines what type of data can be entered (number, text, checkbox, radio), while the name determines how you can refer to it later.

All Roll20 names need to start with "attr_", but when they are referenced, this should be omitted. In the below example, I have created an input intended to store a number, and given it the name attr_HP. When I'm referencing it within Roll20 (either through the Attributes tab on every character sheet, or through JavaScript, which I'll discuss in a future post), I'll simply call it "HP".

```html
<input type="number" name="attr_HP">
```

Here are how the different types of inputs will appear to the user. Remember, things like color, shape, and size can be changed with CSS, but the basic functionality cannot.

Text: `<input type="text">`
<input type="text">

> **Note:** One of the neat things you can do with a text input is provide a `list`. This makes it similar to a `select` element (see below), in that it provides a pre-defined list of choices, but doesn't limit users to those. I'll talk about this 
{: .prompt-tip}

Number: `<input type="Number">`
<input type="number">

Checkbox: `<input type="checkbox">`
<input type="checkbox">

If you want a box to be checked by default, just include `checked` as an attribute:

`<input type="checkbox" checked>`
<input type="checkbox" checked>


Radio: `<input type="radio" name="radio1"><input type="radio" name="radio1"> `
<input type="radio" name="radio1">
<input type="radio" name="radio1">

> **Note:** Radio buttons are exclusive to their group; only one can be selected at a time. This exclusivity is determined by the `name` attribute. To differentiate between values, you could use the `value` attribute, which sets the `name` to its value when it is used.
{: .prompt-tip}

> **Note:** All Roll20 names need to start with "attr_", like <code>name=attr_character_name</code>. When you refer to it later, you just use <code>character_name</code>. If you don't prefix the name with "attr_", the data won't be saved, and will be lost when you reload the character sheet.
{: .prompt-info}

### Label
Labels are exactly what they sound like: pieces of text that don't change, and usually accompany something else.

**Every** time you have an input tag, you should consider using an accompanying label. Labels should always have a `for` attribute. Among other things, this guarantees that you can interact with the input by clicking on the corresponding label. When we get into really advanced stuff, I'll show off how I used this trick in Cyberrats to make radio buttons that highlighted all of the buttons to the left or right of the selected one. For now, note this demo below, where you can switch radio buttons by clicking on the `label`, as well as the button itself.

<div class="example">
  <input type="radio" style="margin-left:7px;" id="radio1" name="radiodemo">
  <label for="radio1">Click on me to select the first one.</label>

  <input type="radio" id="radio2" style="margin-left:7px;" name="radiodemo">
  <label for="radio2">Click on me to select the second one.</label>
</div>

### Button

Buttons! Everyone loves buttons! Here's a button you can click on now!

<div class="example">
  <button>Click me!</button>
</div>

Roll20 has two types of buttons, **Action Buttons** and **Roll Buttons**.

You won't be surprised to hear that Roll buttons simply roll dice, while action buttons can affect the character sheet in other ways.

As of Summer 2021, Action buttons can also trigger a roll, making them extremely versatile.

Action buttons have to have a name starting with "act_", while roll buttons require a name starting with "roll_". Just like with attributes, when referring to the button (including listening for a click), we drop the "act_" or "roll_" prefix.

All you need to know about buttons for now is that they create events we can listen to when they are clicked. We'll talk about it more when we get to CSS, but the default Action Buttons aren't very pretty, and can be cleaned up dramatically by adding a class of "btn", using Roll20's default styling for its own buttons.

> <b>Note:</b> Aside from from the prefix, ensure you have no other underscores in your button names. Roll20 does not allow you to listen to an event if the name has an underscore. 
  <br><br>
  Instead of `name="attr_my_button"`, consider `name="attr_myButton"` or `name="attr_my-button"`.
{: .prompt-danger}

## Other Useful Elements

### Select

Dropdowns! Select elements are great for giving the user a choice.

A `select` tag contains a number of `option`s, which users can pick from. You can set the options to be chosen by default, or to have different values when selected than what the user sees.

As an example, you can imagine a situation where a character sets their Strength score based off a text descriptor:

```html
<label for="strength-selector">Choose your Strength!</label>
<select id="strength-selector">
  <option disabled selected>--choose your strength--</option>
  <option value="3">Scrawny</option>
  <option value="5">Average</option>
  <option value="8">Brawny</option>
  <option value="10">Herculean!</option>
</select>
```

Which would render like this:

<div class="example">
  <label for="strength-selector">Choose your Strength!</label>
  <select id="strength-selector" name="attr_strength">
    <option disabled selected>--choose your strength--</option>
    <option value="3">Scrawny</option>
    <option value="5">Average</option>
    <option value="8">Brawny</option>
    <option value="10">Herculean!</option>
  </select>
</div>

But if I checked the value of strength, it would show up as the corresponding `value` attribute, not the text the user saw.

<div class="example">
  Result: <span id="result"></span>
</div>

<script>

  let strSel = document.getElementById("strength-selector");
  let resSpan = document.getElementById("result");
  function onChange() {
    let value = strSel.value;
    resSpan.innerHTML = value;
  }
  strSel.onchange = onChange;
</script>

### H1, H2, H3...

You can make header tabs in HTML. A Header is just BIG text that indicates the start of a new section of subsection. To make a header, just do something like this: `<h4>My Heading</h4>`, which will render like this:

<div class="example">
<h4>My Heading</h4>
</div>

H1 is used for the largest headings, then h2 after that, and so on, all the way down to h6. In general, you should start with an h1, and then work down to smaller headings as needed without skipping any.  

### HR

The `<hr>` tag is used to make a horizontal line, like this. 
<hr class="demo">

`<hr>` does not need to be closed, a single `<hr>` does the trick.

### BR

The `<br>` tag (which stands for break) creates a new line in your HTML, like this:

`I was writing <br> but then I stopped.`

which renders as:
<div class="example">
  I was writing <br> but then I stopped.
</div>

You probably won't use this too often in a character sheet.

> If you **do** find yourself wanting space between elements, using the `margin` CSS property is a better choice. We'll talk about that in the [next session]({% link _posts/2022-12-23-building-a-roll20-character-sheet-2-md.md%}).
{: .prompt-tip}

### Bold, Underline, Italics

You can wrap text in `<b>`, `<u>`, or `<i>` tags to Bold, Underline, or Italicize it respectively.

```html
 <b>This</b> morning for <u>breakfast</u> I enjoyed <i>twelve</i> omelets.
```

Would render as

<div class="example">
 This <b>morning</b> for <u>breakfast</u> I enjoyed <i>twelve</i> omelets.
</div>

This can be useful for calling attention to specific pieces of information, but A) I'd (generally) encourage you to wrap the text in a `span` and style the span instead, and B) this is the kind of nitty-gritty detail that can stop a project from ever getting finished.

> **Tip:** Get the broad strokes and shape of the thing in first, work on tweaking it to perfection later.
{: .prompt-tip}

### P

You probably won't have much use for `<p>` tags in your character sheet, but these paragraph tags are used to collect text. Like a div, they default to blocks of text, and force new paragraphs to start on new lines.

```html
  <p>Here is one paragraph about me and my dog.</p> <p>Here's another paragraph, but this one isn't about my dog at all!</p>
```

Would render as:

<div class="example">
  <p>Here is one paragraph about me and my dog.</p> <p>Here's another paragraph, but this one isn't about my dog at all!</p>
</div>

Note that HTML ignores multiple spaces, so simply typing 

```html
     <p>Here is one paragraph about me and my dog.
        
    Here's another paragraph, but this one isn't about my dog at all!</p>
```

Would **not** have the desired effect, and would simply render as:

<div class="example">
  <p>Here is one paragraph about me and my dog.
  
  Here's another paragraph, but this one isn't about my dog at all!</p>
</div>

### Textarea

Sometimes you need to get a lot of text from the user. In Cyberrats, I like to include a Notes section on every page so players can add anything I'm missing (or a recap of what happened last session)

```html
  <textarea name="attr_notes"></textarea>
```

<div class="example">
  <textarea class="demo"></textarea>
</div>

Nothing too complicated here, just a big box for text that the user can resize.

### img

The image tag (`img`) is used if you want to include an image inside your character sheet, such as the logo. It has a required attribute, `src`, that points to a URL of the image. Roll20 prefers that your images be hosted on (their) Github, which we'll talk about in the final session.

# Summary

We've covered the basic elements of HTML: `div`s and `span`s for holding other elements and setting up your hierarchy, `input`s for getting data from the users, `label`s for displaying static text, and `button`s for triggering actions or rolls.

As we use these elements to build (starting in [session 3]({% link _posts/2022-12-24-building-a-roll20-character-sheet-3.md%})), you'll get a better and more intuitive handle on how they all work. For now, let's get a similar overview of CSS in [session 2]({% link _posts/2022-12-23-building-a-roll20-character-sheet-2-md.md%}).


> Note: There are **many** other common HTML elements, including `ol` and `ul` for making lists (ordered or unordered, respectively), `tr` and `td` for use with `table`s, and `a` (anchor) tags for links. What we've covered here are the elements you're most likely to use in a character sheet, **not** an exhaustive list of HTML elements, nor a primer on making general websites.
{: .prompt-warning}
