---
layout: post
title: Copy part of a message in Bluesky
img_path: "../../assets/img/"
date: 2026-05-17 11:36 -0700
---
There's a particular brand of horseshittery that involves taking away user control. I've [posted before about web patterns](https://garden.alexrinehart.net/software-and-technology/web-design-patterns-you-should-stop-doing/) I wish would stop existing, but now I've got a new one to add to the list: disabling copy/paste.

Bluesky is particularly egregious about it. In DMs, you can click a little button to copy the *entire* text of a message, but they disable the ability to click and drag to copy part of a message. 

Imagine the following:

![Two bluesky messages. The first says I'll send over those documents. What's the best email? and the second says: Great! My email address is GoodEmail@example.com. It might take me a few hours to respond, I'm about to board a plane.](bskyDM.png)

You ask your friend for one piece of information and they reply with more than you need. Bluesky says the answer is to copy the entire message, paste it somewhere like notepad, and then trim down to the part you want. Horseshit.

Here's a TamperMonkey script that lets you select parts of messages like a normal human being. Note: the default behavior on click of a Bluesky DM is to expand the message and show the time it was sent. You lose that functionality with this script, and replace it with better, universal functionality instead.

## What's Tampermonkey?

Tampermonkey is a browser extension that exists in Chrome, Firefox, and their derivatives. It lets users write their own scripts to modify the look or behavior of various websites. You can write your own, or find them from the community. For example, when Amazon announced they were removing the ability to download purchased ebooks, many scripts to bulk download purchased titles were released (downloading one title typically required 3 mouse clicks).

Once you install TamperMonkey, make sure to go into settings and enable "Allow user scripts". Otherwise the extension won't do anything. Security 🙄.

Then, make a new script, paste in the below, save it, and refresh your Bluesky DMs. Now you can copy/paste like a normal human, instead of having to roundtrip through notepad like an animal.

## The Script

```javascript
// ==UserScript==
// @name         Bluesky DM Text Selector
// @namespace    http://tampermonkey.net/
// @version      4.0
// @description  Disable DM bubble button behavior while allowing text selection
// @match        https://bsky.app/*
// @grant        none
// ==/UserScript==

(function () {
    'use strict';

    function applyFix() {

        // Each message is a button, per bsky.
        const buttons = document.querySelectorAll('button[role="button"]');

        buttons.forEach(button => {

            if (button.dataset.textSelectFixed) return;

            const text = button.querySelector('[data-word-wrap]');

            if (!text) return;

            // Disable ALL interaction on the button
            button.style.pointerEvents = 'none';

            // Re-enable interaction only for the text
            text.style.pointerEvents = 'auto';

            // Allow selecting text
            text.style.userSelect = 'text';
            text.style.webkitUserSelect = 'text';

            // Make cursor feel normal (instead of clicky pointer)
            text.style.cursor = 'text';

            button.dataset.textSelectFixed = '1';
        });
    }

    // Bluesky is React-based; keep checking for new messages
    setInterval(applyFix, 1000);

})();
```