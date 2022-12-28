---
layout: post
title: "Building A Roll20 Character Sheet Session 0: Overview"
date: 2022-12-22 12:15 -0800
categories: [Tutorial, Roll20 Character Sheet Tutorial]
tags: [roll20, rpg, tutorial, web-dev]
permalink: tutorials/roll20-character-sheet/0
---


## Overview

I recently made a Roll20 character sheet for [Cyberrats](https://alrine.itch.io/cyberrats). This was my second time making a Roll20 character sheet (though the first was [5 years ago](https://github.com/asr1/roll20-character-sheets/tree/master/Solipstry)).

It took me around 60 hours to make the Cyberrats character sheet, though it's more complex than most. My goal with this guide is to help you make your next character sheet (whether it's your first or your fifth) in a fraction of that time.

![Cyberrats character sheet](../../assets/img/CyberratsPreview.png){: width="500"}
_A small preview of the first parge of the Cyberrats character sheet on Roll20._

You can find all of the code for this character sheet [on Github](https://github.com/asr1/roll20-character-sheets/tree/master/Cyberrats), though jumping in to it directly is probably overwhelming.

> **Note on costs:** There is no way to develop or test a Roll20 Character sheet without a Pro account, the subscription for which currently costs around $10 / month. If you aren't a regular subscriber, I recommend grabbing a month when you'll have time to iterate quickly. While you can do a lot of rough layout in HTML alone, it's really beneficial to load everything up in their environment.
{: .prompt-info}

## This Guide

This guide is a series of tutorials split into 10 session. You are in session 0, which is **The Overview**. As I write other sections, I will link to them here.

The sessions are as follows:

Session 0. Overview  
[Session 1. Crash Course on HTML]({% link _posts/2022-12-22-building-a-roll20-character-sheet-1-md.md%})  
[Session 2. Basic CSS and styling]({% link _posts/2022-12-23-building-a-roll20-character-sheet-2-md.md%})  
[Session 3. Getting started with Roll20]({% link _posts/2022-12-24-building-a-roll20-character-sheet-3.md%}) (**Tutorial starts here!**)  
[Session 4. Putting it all together]({% link _posts/2022-12-25-building-a-roll20-character-sheet-4.md%})  
[Session 5. Filling It In (With Flex)]({% link _posts/2022-12-26-building-a-roll20-character-sheet-5.md%})  
[Session 6. The Body]({% link _posts/2022-12-27-building-a-roll20-character-sheet-6.md%})  
Session 7. Advanced CSS  
Session 8. JavaScript and events  
Session 9. Roll templates  
Session 10. Advanced tips and  tricks  
Session 11. Making it official (and available)

Sessions 1 and 2 are high-level overviews of their respective technologies. In sessions 3 and 4 we'll actually start building a basic character sheet, and the rest of the sessions will teach you techniques to make those sheets interactive, stylish, and all-around better.

> **Tip:** If this is still overwhelming, or you don't have the time to learn all of this, you can hire me to make a character sheet for you. Find my contact information in the sidebar. Rates vary with the complexity of the sheet.
{: .prompt-tip}

## Tools

Roll20 character sheets are built using the same tools as most web sites: HTML, CSS, and JavaScript.

**HTML** is used to determine the structure of your page (how the sheet is laid out), **CSS** determines the style of those elements (how the page, and the elements on it, look). **JavaScript** is used for interaction (when the user clicks on a button, do something).

> **Note:** While proficiency with these three technologies is useful, it is not required: my goal is for these tutorials to be accessible to anyone, regardless of experience.
<br><br>
**That said, the less experience you have, the longer it will take you.** I am fairly experienced with many of these technologies, and it took me around 60 hours to make the character sheet for Cyberrats. It's on the complex end, as far as character sheets go. Some of that time was spent learning new things, which I'm hoping to share with you through these posts.
<br><br>
It is likely that you will have to trade complexity for time.
{: .prompt-info}

I'll talk more about these technologies later on, in their own sessions, as well as how we use them, but the overview about should give you the general idea of what they do.

## Technology

As an aside, all of these files are just text files with different file extensions. HTML files end in .html; CSS files end in .CSS; and JavaScript files end in .js. You *can* edit these files in a text editor like Notepad, but I **strongly** recommend downloading a more powerful (and free!) text editor like [Notepad++](https://notepad-plus-plus.org/downloads/) or [VSCode](https://code.visualstudio.com/).

These text editors can provide color-coding of certain words (called Syntax highlighting), auto-complete opening HTML tags with closing ones, and provide many other tools that will improve your quality of life.



![HTML Code in Notepad++](../../assets/img/NotepadPlus.png){: width="1000"}
_HTML Code in Notepad++ with syntax highlighting. When I click "Textarea", the matching close tag is highlighted._

You can open your HTML files either with your text editor, for editing, or with your favorite web browser to see how it looks.

Let's jump into [Section 1]({% link _posts/2022-12-22-building-a-roll20-character-sheet-1-md.md%}), where I cover the basic building tools of HTML. You'll use those to build the skeleton of your character sheet.
