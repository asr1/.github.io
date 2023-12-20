---
layout: post
title: You should use an RSS reader
img_path: "../../assets/img/"
tags:
- persuasive
categories:
- Software
tags:
- software
- recommendation
date: 2023-03-19 14:19 -0700
---
# What is RSS

RSS stands for Really Simply Syndication, but don't worry about that. Worry instead that it's the best tool for the internet that you may not know about.

Shortly, RSS lets you gather a bunch of websites (each one known as a "feed"), and consolidate them in *one* place that you can check to see if any of them have updated.

## What can it do?

There's a joke that on the internet, there are only four websites, each filled with screenshots of the other three. And while there is some truth to that, it's not the whole story.

![Four Websites](four_websites.png){: w="500"}

There are dozens of websites you might check every day, or every time they update: things like webcomics, blogs, [daily deals](https://meh.com), and more.

I'll cut to the chase: RSS lets you get notified about updates to any of those websites all in one place!

Just like how you don't have to go and check each individual podcast feed to see if a new episode dropped, but instead can just ask your podcast app to notify you when an episode drops, RSS works the same way for websites!

![An RSS Reader](RSSReader1.png)

## Why haven't I heard about this?

Let me tell you a story. In 2013, Google had a program called Google Reader. You may have never heard of it, but many people cite the killing of Reader as the Rubicon from which Google couldn't return. Before killing Reader, Google did not have a reputation of killing off beloved products and services.

But they did kill it. Claiming low usage, Google turned off Reader for good one summer day in 2013. [And you know how that story ends](https://killedbygoogle.com/).

I was introduced to Reader because it was one of the websites that had a Konami Code Easter Egg: if you hit `up up down down left right left right ba enter` while on Reader, a small ninja would pop out of one side of the screen, wave at you, and then disappear. It was a lovely time to be on the internet.

RSS took a huge blow 10 years ago, but it's not dead! Other Readers (Feedly, NewsBlur, Snarfer, Reeder) popped up. Many have been discontinued *since* 2013 as well (RIP Digg Reader, you were too good for this world). But the technology still exists (and it's what your podcasts already use!) 

![RSS Icon](RSSIcon.png){: w="200" .left}

It's true that this icon isn't as ubiquitous as it was in the early 2000s, but you'd be surprised how often websites support this still. And most RSS readers include search, so you can stay on top of your favorite sites without having to hunt down the elusive RSS feed yourself.

## What reader should I use?

For my money, I recommend [The Old Reader](https://theoldreader.com/). It's a clone of how Google Reader used to look, and if I recall correctly, it was built in one weekend. I tried many RSS feeds in the wake of Google Reader's death, but this was my favorite. If you primarily intent to read it on your phone, other readers like Feedly have better app-based experiences.

## How do I use this thing?

Easy! Simply go to [https://theoldreader.com/](https://theoldreader.com/) and create an account (or log in with an existing account, like Google). Then click "Add a subscription" on the top left, and search for your favorite webcomics, blogs, and other regularly-updated websites. It also works with Patreon, Webtoons, and Substacks!

![The Old Reader RSS Reader homepage](RssReader2.png)

## I'm sorry, did you say Substack?

That's right! If you're tired of getting newsletters delivered to your email, but still want to stay up to date without needing to check *every single feed*, RSS readers are a great way to do that!

Simple add `/feed` to the end of any Substack URL and you can add it to your reader. For example, `https://samkriss.substack.com/feed`.

## And Webtoons?

This one is even less obvious, but it is supported! Go to your favorite Webtoon (for example, [Down To Earth](https://www.webtoons.com/en/romance/down-to-earth/episode-1/viewer?title_no=1817&episode_no=1)). Look at the URL and delete everything after the name of the comic and before `title_no=XXXX`. Keep that, and delete everything after the last number there.
 Then Add `rss` right before the `title_no`. So `https://www.webtoons.com/en/romance/down-to-earth/episode-1/viewer?title_no=1817&episode_no=1` would become `https://www.webtoons.com/en/romance/down-to-earth/rss?title_no=1817`.

> **Note:** Don't be alarmed if you follow that link and it looks like a bunch of technobabble gobbledygook. This is normal. It's an XML file, and you can ignore it. You just need to tell your RSS reader the *URL* of this XML gobbledygook.
{: .prompt-warning}

 Add this to your reader as a new feed, and *voila*, you get updates whenever your favorite space alien romance comic updates! (*also works for other genres, I suppose*)

## Conclusion

I try to not to tell people what they "should" do, but RSS is one of the technologies that makes my life simpler and more organized. I don't have to remember which webcomics I follow and what their update schedules are (especially for erratic ones like [Order of the Stick](https://www.giantitp.com/comics/oots0001.html)). I don't have to visit my favorite author's blogs to see whether they've put out an update this month. And I never have to worry about missing something important or forgetting about something entirely.

Instead, I simply check one website and find all my notifications in one place.

And best of all?

I can read Substack in peace in my own time, without having to clog up my email.

♥ I hope it brings you as much joy as it's brought me. enjoy

***PS*** if you enjoyed this, you can even add *this very blog* to your RSS reader. See the button on the bottom left? It's not just for show!
