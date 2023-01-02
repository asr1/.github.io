---
layout: post
title: 'Building A Roll20 Character Sheet Session 7: Advanced CSS'
categories:
- Tutorial
- Roll20 Character Sheet Tutorial
tags:
- roll20
- rpg
- tutorial
- web-dev
- css
permalink: tutorials/roll20-character-sheet/7
date: 2022-12-27 22:06 -0800
---
> It should be noted that what I'm referring to as "Advanced CSS" in this session is more appropriately called "Intermediate CSS". I am not an expert, and do not want to give the impression that the techniques presented here are anywhere near the height of the complexity or power that CSS can offer. 
{: .prompt-info}

## Display: Flex

We've already talked about `display: flex` in [session 5]({% link _posts/2022-12-26-building-a-roll20-character-sheet-5.md%}), and we saw that you can have multiple containers, each flexing in a different way, inside one another.

Flex is a powerful tool for organizing content. While there's no better way to build proficiency than by using it, [FlexBox Froggy](https://flexboxfroggy.com/) is an incredible tool to teach the different things you can do with Flex.

### Things to Note

You can style a container as either a row or a column, including reverse order.

A parent container can justify its contents to determine their spacing: start, end, space-between, or space-around.

A specific element can `justify` itself differently than the rest.

You can embed containers inside one another, like we did in the header. This can let you have a row of items, where each item contains a column inside itself.

<div style="display: flex; flex-direction: row; background-color: #ebdbb2; justify-content: space-around; padding: 10px;">
    <div style="display: flex; flex-direction: column; background-color: #83a598; text-align:center; padding-left:10%; padding-right:10%">
        <span>One</span>
        <span>Two</span>
        <span>Three</span>
    </div>
     <div style="display: flex; flex-direction: column; background-color: #8ec07c; width:20% text-align:center; padding-left:10%; padding-right:10%">
        <span>Four</span>
        <span>Five</span>
        <span>Six</span>
    </div>
     <div style="display: flex; flex-direction: column; background-color: #d3869b; width:20% text-align:center;padding-left:10%; padding-right:10%">
        <span>Seven</span>
        <span>Eight</span>
        <span>Nine</span>
    </div>
</div>

This example comes from the following code:

```html
<div style="display: flex; flex-direction: row;
background-color: #ebdbb2; justify-content: space-around; padding: 10px;">

    <div style="display: flex; flex-direction: column; background-color: #83a598;
    text-align:center; padding-left:10%; padding-right:10%">
        <span>One</span>
        <span>Two</span>
        <span>Three</span>
    </div>

     <div style="display: flex; flex-direction: column; background-color: #8ec07c;
     width:20% text-align:center; padding-left:10%; padding-right:10%">
        <span>Four</span>
        <span>Five</span>
        <span>Six</span>
    </div>

     <div style="display: flex; flex-direction: column; background-color: #d3869b;
     width:20% text-align:center;padding-left:10%; padding-right:10%">
        <span>Seven</span>
        <span>Eight</span>
        <span>Nine</span>
    </div>
</div>
```

## Variables!

Let's say you find yourself using the same colors over and over again. In addition to always being tired of typing them out, what if you change your mind?

Never fear, CSS lets you define **variables**, so you can give a color a name, and change it in one place.

Declare a variable like this:

```css
body {
    --background-color: #d3869b;
}
```

Then, wherever you want to use that variable, you just use `var`:

```css
div.container {
    background-color: var(--background-color)
}
```

Variables must start with 2 dashes.

> **Note:** Variables are only visible to the children of the element they are declared on. If you want a variable to be visible to the entire document, you can declare it in the `body` selector, or the `:root` selector.
{: .prompt-info}

## Class Names

You can name classes anything you want, but don't be surprised if some common names are already defined by Roll20, and will get overwritten (e.g small).

You can avoid this by prefixing all your class names with something like "my-", or just using unique names.

## Selectors

Most of the complexity in CSS is about selecting the right element(s). The actual styling is usually straightforward.

We've already learned about two complex selectors: the descendant selector (`div p` matches `p` elements that are descendants of `div`s, no matter how far removed), and the child selector (`span > button` will match a button that is **immediately** inside of a `span`, that is, a button whose parent is a span).

But there are **many** more selectors. There are three things to remember when dealing with CSS selectors:

1. They should always be read right to left.
2. Bookmark this page and leave it open: <https://www.w3schools.com/cssref/css_selectors.php>.
3. Selectors match IN ORDER (you can't match backwards!)

Other selectors include immediately follows (+), sibling (~), and all (*). That last one is very powerful (and can be very slow). Use it carefully.

### Right To Left

No matter how many selectors you chain together, it always matches against an element of the right-most type.

`div.attributeHolder > label` matches a `label` that is inside of (that is, a child of) a `div` with a class of attributeHolder.

Something like `div.container > span.special div.basic > p` matches a `p` element. It just happens to match `p` elements that have parents that are `div`s with a class of basic who have an ancestor (not necessarily immediate!) that is a span with a `class` of special who have a parent that is a `div` with a class of container.

If you're wondering why you would possibly need something so complex, it will make more sense when we talk about hidden selectors.

### Selectors match in order

The key thing is that CSS can only select elements in order: You can do Y follows X, but you CANNOT do X is before Y.

Elements don't have to _immediately_ follow! You can match on

* Immediately follows (x+y)
* Is a child of (either directly or just somewhere in the hierarchy)
  * Direct Child is div > button.urgent
    * This is a button with class urgent that is directly inside a div
  * Any child of is div.TopLevel button
* Is a sibling of (again, will only match siblings that appear AFTER others)

`.first ~ .second` matches any element with a class "second"  that is at the same level as an element with class "first". You can NEVER match the first element with this selector

You can always match after, no matter how far after. You can never match "before", even if it's right before.

Once again: there is no way to match "This element appears right before this other element" or "This element has a child of some other element".

> Another limitation that isn't quite so obvious is that you can't go backwards **at all**. So there's no way to say "My `p` element follows a `span` that has a `label` inside of it". You can only go forward. Once you go "into" the `span` to see its child, there's no coming back out.
{: .prompt-warning}

## Value Matching

You can check if an input has a certain value, or if a checkbox is checked.

Checkboxes have a checked property if they are checked, which you can select with `:checked`.

This CSS matches a label that immediately follows an input with a class of threatbar IF the box is checked.

This can be used, for example, to make a custom dark mode theme, or to have text turn <span style="color:red; font-size:2em;font-variant:small-caps">BRIGHT RED</span> if you click the "Danger" box.

> It used to be popular for sheets to design their own dark modes controlled by a checkbox or options page, but sometime around 2021 Roll20 added their own native Dark Mode, which you should use instead. We'll talk more about this in a future session.
{: .prompt-danger}

```css
input.threatbar:checked + label {
    color: #aaaaa;
}
```

You can also check for a specific value, which is most useful for a dropdown, where you can predict likely values.

In Cyberrats, we have tabs at the top of the base sheet that let players toggle between the main base and the submarine.

We do that by changing the value of a hidden input (with JavaScript) whenever one of the tabs is clicked on. We'll cover that in more detail later, but for now the key takeaway is that you can match on value.

```css
.basetabstoggle[value="mainbase"] ~ div.mainbase {
    display: flex;
}
```

_Ordinarily, the div.mainbase has `display: hidden`, but if the appropriate tab is clicked on, my "basetabstoggle" `input` changes values, and the mainbase `div` becomes visible instead.

## Hidden Inputs

In [the first session]({% link _posts/2022-12-22-building-a-roll20-character-sheet-1-md.md%}), we talked about several types of `input`: text, number, radio, and checkbox.

But there's one type we didn't talk about that's very common on Roll20 character sheets, and that's **hidden**.

`input type="hidden` will create an input that won't render on the screen. You can achieve the same result with `display: none`. This may not seem very useful. And on its own, it isn't. But when you combine it with one other piece of information, it becomes very useful indeed.

### Attribute Sharing

If two elements in a Roll20 character sheet have the same name pointing to an attribute (such as `name="attr_hp"`), then modifying either one of those elements will modify both of them.

One popular application of this is to use a readonly `span` to show off some piece of information.

```html
<span class="outer">
    Your current Hit Points are <span name="attr_HP"></span>
</span>
```

This will auto populate the span with the value of the character's hit points, as determined by the attr_HP input.

### Combining the Two

So let's say we have an expansion that adds additional character options, like Psionics. We don't want those options to show all of the time, because most players won't have the expansion. But we do want to include them to give tools to players who bought our expansion (thanks, players! You're the best!)

What can we do?

Well, the most obvious solution is to put the checkbox at the veeery top of your document, above the `div` with the "character-sheet" class that wraps everything else. 

But what if you can't do that? What if you need to put it inside a `span` to style it correctly? Or if you want the options to be at the **bottom** of the character sheet instead?

That's where `<input type="hidden">` comes into play.

Put your checkbox wherever you want it, but at the top of your document, at the same level as your `div class="character-sheet"` (and just before it), put an `<input type="hidden">` with the same attribute as your checkbox.

Then you set your expansion material to `display: none` UNLESS it is the child of a div.charachter-sheet that has as its sibling a checkbox with the right class AND that checkbox is checked. Check it out:

```html
    <input type="hidden" class="psionic" name="attr_psionic-expansion"/> <!-- Fake checkbox, doesn't render. Matches value of the one below.-->
    <div class="character-sheet">
        <!-- ... -->

    <div class="expansion psionic">
        <h2>Psionics!</h2>
    </div>

    <div class="options">
        <label for="expansion">Show psionic expansion?</label>
        <input type="checkbox" class="psionic" name="attr_psionic-expansion"/> <!-- This is the REAL checkbox -->
    </div>
</div>
```

and our CSS:

```css
div.expansion {
    display: none; /* Our default for all expansion content*/
}

/* Match a div with class="expansion" that is SOMEWHERE inside a div with a class of "character-sheet" IF that character sheet has a checked checkbox with class "psionic" on the same level as it (and before it) */
input.psionic:checked ~ div.character-sheet div.expansion {
    display: block;
}
```

> **Why are we using `~` instead of `+`?**
>
> Because `+` only matches elements that immediately follow. That would work here, but if we added another input, it would stop working. This approach lets us have as many hidden inputs as we want above the div.character-sheet.
{: .prompt-info}

You can try this out yourself, and verify that as you check and uncheck the box, the psionic div will appear and disappear accordingly.

You can also use this trick for multiple different values, whether its different settings, expansions, or anything else.

Just put a hidden copy at the top of the document as use the sibling (`~`) selector paired with the descendant (` `) selector to toggle visibility based on the `:checked` attribute.

> Because CSS can only match  in order, it's useful to have hidden attributes at the TOP of your sheet so you can reference them anywhere
{: .prompt-tip}

## ::Before and ::After

There are a handful of "pseudo selectors" that let you match against elements or properties that don't actually exist. Adding `::before` or `::after` to a selector lets you use the `content` property to add things before or after elements.

```css
input::before {
   content:  "Type something here:"
}
```

This will add the words "Type something here:" before every `input`.

> **Note:** You cannot use this to add HTML elements, but you can style the `::before` or `::after` with properties such as color, padding, and borders.
{: .prompt-warning}

## Counting repeating elements

CSS can count how many times an element appears. First you need to create (or reset) a counter by giving it a name and using `counter-reset`. This is often done on the parent element, like the section that holds a repeating-section.

```css
counter-reset: myCount; /* I could call this counter anything. */
```

Then, whenever I want to increment it (like on every repeating-weapon for example), I just call `counter-increment: mycount`. If I want to also display the count, I can use the `content` property of a `::before` or `::after` and call it with `counter()`.

```css
input.weaponName::before {
    counter-increment: myCount;
    content: counter(myCount) '.'; /* This will add 1. 2. and so on. */
}
```

> Note: there is no way to get the total count of something yet, though a CSS proposal for this feature has been considered.
{: .prompt-info}

## :not

CSS lets you match things that DON'T match a certain element (or elements).

I can look for a label that follows a checkbox that isn't checked:

`input.myClass:not(:checked) + label`

Or I can match every descendant of something EXCEPT for a certain one:

`.charactersheet div:not(.special)`

And I can even pass in multiple arguments

`label:not(.special, .special2)`

This is useful for excluding a class or element from a common styling.

## nth child, first-child

If you only want to affect the first child of something, you can add the `:first-check` pseudo selector:

`div > label:first-child`

Or combine with `:not` to match all the rest: `div > label:not(:first-child)`

You can do every other with `div > label:nth-child(2)`, or pass in another number for every third or fourth or....

There's also `:last-child` and `:nth-last-child(n)`. And there's `:first-of-type` and `:last-of-type`, which can be useful if you want to math, for example, the LAST `p` inside a div.

Finally, you can match against the `::first-line` or `::first-letter` of some text, if you want to stylize it differently (like bold, or extra large).

## Styling radio buttons

You cannot style radio buttons or checkboxes directly

HOWEVER

If you remember from [session 1]({% link _posts/2022-12-22-building-a-roll20-character-sheet-1-md.md%}), clicking on an input's label (identified with the `for` attribute) also selects that input.

We can take advantage of this fact to fake a styling of our buttons.

We do this in Cyberrats with the Grief buttons, Threat meters, and Victory Meters, so it looks like every option smaller than the one selected is also colored and styled.

First, you need to hide the input in question with `display: none`. Then you style the input how you want it, using its `::before` pseudo selector to add content. 

Finally, you can match with selectors like `+` and `~` to change the siblings, if you want to style other buttons based on the one selected.

Here's how Cyberrats does its grief. First an example, then the code.

<style>
div.outergrief {
    display: flex;
    flex-direction: row;
}

button.grief {
    align-self: center;
    display: flex;
    margin-top: 12px;
    height: fit-content;
}

div.grief {
    background: transparent;
    box-sizing: border-box;
    display: flex;
    height: 6em;
    overflow: hidden;
    padding: 1em 0;
    position: relative;
    width: 100%;
    padding-bottom:30px;
}

div.grief::before {
    content: "";
    display: block;
    position: absolute;

    top: 4em;
    width: 100%;
}

.progressbar__radio {
    display: none;
}

label.progressbar__label {
    text-align: center;
    padding-top: 0px;
    margin-left: 10px;
    width: 40px;
}

/* Labels after the one we've clicked */
.progressbar__radio:checked + label ~ label {
    color: black;
}

/* Every circle that follows the one clicked */
.progressbar__radio:checked + label ~ label::before {
    background: #4286f4;
    border: 2px solid #4286f4;
}

.progressbar__radio:checked + label ~ label::after {
    background: #aaa;
}

/* The checked circle */
.progressbar__radio:checked + label::before {
    background: #4286f4;
}

/* The checked label */
.progressbar__radio:checked + label {
    color: black;
    text-align: center;
}

/*Labels before the one we clicked*/
.progressbar__label {
    color: #aaa;
    display: table-cell;
    font-weight: bold;
    position: relative;
    text-align: center;
}

.progressbar__label::before {
    background: white;
    border: 2px solid #4286f4;
    bottom: calc((100% - 70px) - 2px);
    content: "";
    display: block;
    height: 40px;
    position: absolute;
    width: 40px;
    z-index: 9;
}
</style>

<div class="outergrief">
  <div class="grief">
      <input type="radio" id="step-6" value="6" name="attr_grief" class="progressbar__radio">
      <label for="step-6" class="progressbar__label">6</label>
      <input type="radio" id="step-5" value="5" name="attr_grief" class="progressbar__radio">
      <label for="step-5" class="progressbar__label">5</label>
      <input type="radio" id="step-4" value="4" name="attr_grief" class="progressbar__radio">
      <label for="step-4" class="progressbar__label">4</label>
      <input type="radio" id="step-3" value="3" name="attr_grief" class="progressbar__radio">
      <label for="step-3" class="progressbar__label">3</label>
      <input type="radio" id="step-2" value="2" name="attr_grief" class="progressbar__radio">
      <label for="step-2" class="progressbar__label">2</label>
      <input type="radio" id="step-1" value="1" name="attr_grief" class="progressbar__radio">
      <label for="step-1" class="progressbar__label">1</label>
      <input type="radio" id="step-0" value="0" name="attr_grief" class="progressbar__radio" checked>
      <label for="step-0" class="progressbar__label">0</label>
  </div>
</div>

_Go on, give it a try._

```html
<div class="outergrief">
  <div class="grief">
    <input type="radio" id="step-6" value="6" name="attr_grief" class="progressbar__radio">
    <label for="step-6" class="progressbar__label">6</label>
    <input type="radio" id="step-5" value="5" name="attr_grief" class="progressbar__radio">
    <label for="step-5" class="progressbar__label">5</label>
    <input type="radio" id="step-4" value="4" name="attr_grief" class="progressbar__radio">
    <label for="step-4" class="progressbar__label">4</label>
    <input type="radio" id="step-3" value="3" name="attr_grief" class="progressbar__radio">
    <label for="step-3" class="progressbar__label">3</label>
    <input type="radio" id="step-2" value="2" name="attr_grief" class="progressbar__radio">
    <label for="step-2" class="progressbar__label">2</label>
    <input type="radio" id="step-1" value="1" name="attr_grief" class="progressbar__radio">
    <label for="step-1" class="progressbar__label">1</label>
    <input type="radio" id="step-0" value="0" name="attr_grief" class="progressbar__radio" checked>
    <label for="step-0" class="progressbar__label">0</label>
  </div>
</div>
```

```css
div.outergrief {
    display: flex;
    flex-direction: row;
}

div.grief {
    background: transparent;
    box-sizing: border-box;
    display: flex;
    height: 6em;
    overflow: hidden;
    padding: 1em 0;
    position: relative;
    width: 100%;
    padding-bottom:30px;
}

.progressbar__radio {
    display: none;
}

div.grief::before {
    content: "";
    display: block;
    position: absolute;
    top: 4em;
    width: 100%;
}

label.progressbar__label {
    text-align: center;
    padding-top: 0px;
}

/* Labels after the one we've clicked */
.progressbar__radio:checked + label ~ label {
    color: black;
}

/* Every circle that follows the one clicked */
.progressbar__radio:checked + label ~ label::before {
    background: #4286f4;
    border: 2px solid #4286f4;
}

.progressbar__radio:checked + label ~ label::after {
    background: #aaa;
}

/* The checked circle */
.progressbar__radio:checked + label::before {
    background: #4286f4;
}

/* The checked label */
.progressbar__radio:checked + label {
    color: black;
    text-align: center;
}

/*Labels before the one we clicked*/
.progressbar__label {
    color: #aaa;
    display: table-cell;
    font-weight: bold;
    position: relative;
    text-align: center;
}

.progressbar__label::before {
    background: white;
    border: 2px solid #4286f4;
    bottom: calc((100% - 40px) - 2px);
    content: "";
    display: block;
    height: 20px;
    position: absolute;
    width: 20px;
    z-index: 9;
}
```

## Summary

Now you know a ton of "advanced" tricks that CSS can do. I hope you appreciate the power of the language, and see some useful applications within your sheets. If not, don't worry: many people use HTML without ever touching the topics covered in this session.

In the [next session]({% link _posts/2022-12-29-building-a-roll20-characer-sessionn-8-javascript-and-events.md%}) we'll learn about JavaScript, allowing you to respond and react to player actions (like changing a dropdown or clicking a button). This will let you make your character sheet interactive, reactive, and POWERFUL! [Jump on in!]({% link _posts/2022-12-29-building-a-roll20-characer-sessionn-8-javascript-and-events.md%})