---
layout: post
title: building-a-roll20-character-sheet-session-7-advanced-css
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
---
> It should be noted that what I'm referring to as "Advanced CSS" in this session is more appropriately called "Intermediate CSS". I am not an expert, and do not want to give the impression that the techniques presented here are anywhere near the height of the complexity or power that CSS can offer. 
> {: .prompt-info}



Notes:

Variables

    Talk about display: Flex
    and multiple divs each flexing in a different way

    selectors  
        Can chain them together but you read selectors right to left
        input.narrow 
            is an input with a class of narrow

        talk about pseudo selectors like :not and ::before
        
        div.attributeHolder > label 
            matches a label that is inside of (a child of) a div with a class of attributeHolder
        
Bookmark this page and leave it open https://www.w3schools.com/cssref/css_selectors.php

You can name classes anything you want, but don't be surprised if some common names
are already defined by roll20, and will get overwritten (e.g small)



    The key thing is that CSS can only select elements in order: 
        You can do Y follows X, but you CANNOT do X is before Y.
        Things don't have to immediately follow! You can match on
            * Immediately follows (x+y)
            * Is a child of (either directly or just somewhere in the hierarchy)
                * Direct Child is div > button.urgent
                    This is a button with class urgent that is directly inside a div
                * Any child of is div.TopLevel button
            * Is a sibling of (again, will only match siblings that appear AFTER others)
                .first ~ .second matches any element with a class `second`  that is at the save level as an
                    element with class `first`. You can NEVER match the first element with this selector

    
    One of the things // where was I going with this thought

    Because you can only go in order, it's useful to have hidden attributes at the TOP
    of your sheet so you can reference them anywhere

    Most of the complexity in CSS is about selecting the right element(s). The actual styling is usually straightforward.



* Let users toggle an expansion or supplement on or off, and change the character sheet accordingly
* Affect only the first element in a repeating section
* Adding content before or after another element
* Counting your repeating elements
* Using variables so you don't have to repeat colors you use a lot
