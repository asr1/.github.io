---
layout: post
title: Leveling up in Excel (Part 2)
categories:
- Software
tags:
- software
- excel
img_path: "../../assets/img/"
image:
  path: templateHeaders/spreadsheet.jpg
  alt: Rows of cells, each filled with numbers
date: 2025-01-31 12:10 -0800
---
[Last time]({% link _posts/2025-01-17-leveling-up-in-excel-part-1.md%}), I explained how there are ten tiers of spreadsheet mastery, and that by conquering each of them you unlock a new level of proficiency. The first 5 are competency, while these five bring you into expertise.

## 6. Conditionals

Sometimes you want different things depending on what's in the cell. Excel has the `if()` formula, which allows you to declare a [condition](https://support.microsoft.com/en-us/office/create-conditional-formulas-ca916c57-abd8-4b44-997c-c309b7307831), what to do if it's met, and what to do if it's not met.

For example, suppose I bought a bunch of junk and am now selling it. I want to see my profit. If the number sold * price is greater than what I paid, show me number sold * price - what I paid. Otherwise, show 0. I don't want negative numbers here!

`=IF(D2*C2>B2,D2*C2-B2,0)`

I can make this even clearer if I add an intermediary column showing revenue.

![Spreadsheet showing conditional revenue](excel6.png)

### Take conditionals a step further

You can use `and()` and `or()` to create more complicated conditional formulas. If I've sold at least 10 units or if I've sold at least one unit for more than $10, write "Succeeding". Otherwise, write "Underperforrming". 

`=IF(OR(C2>=10,AND(C2>0,D2>10)),"Suceeding","Underperforming")`

Note that you have to invert the order of "and" and "or" from normal English. This can take some getting used to!

![A spreadsheet showing the formula listed above](excel7.png)

### Take conditionals another step further

You can even nest your [conditions and chain them together](https://support.microsoft.com/en-us/office/if-function-nested-formulas-and-avoiding-pitfalls-0b22ff44-f149-44ba-aeb5-4ef99da241c8). 

If A5 is less than 5, label this Low. Otherwise, if it's more than 1000, label it High. Anywhere between, label it Medium.

`=if (a1<5, "Low", if(a1>1000, "High", "Medium"))`

You can see the potential to string these together in even more complex ways!

## 7. VLookup

Suppose you've got a table of data, like showing sales of produce for each quarter. If you want to grab a piece of that data elsewhere, how can you do it? 

That's where [VLookup](https://support.microsoft.com/en-us/office/vlookup-function-0bbc8083-26fe-4963-8ab8-93a18ad188a1) comes in. Vlookup lets you reference data from equations just by knowing how it's set up.

> <b>Note:</b> Ensure that your data is either in alphabetic order OR that you provide FALSE as the final argument to VLookup. Otherwise it may not find it at all!
{: .prompt-danger}

Here's that quarterly produce example, where I'm just pulling out the Q1 data based on what's written elsewhere (B14)

![Vlookup example](excel8.png)

Vlookup is great for pulling data out of structured tables to reference elsewhere!

### Take VLookup a step further

It's possible to do a [2-dimensional VLookup](https://www.excel-university.com/two-dimensional-vlookup/), where both the column and row are varied. This is rather complex, and requires nesting the `match()` formula within.

## 8. Dollar sign references

Remember before when we were learning about fill and ctrl+d? Well what if you don't WANT the references to shift down every time. For example, let's look at that VLOOKUP example we just did.

![A Vlookup call with the reference table offset by 2 rows](excel9.png)

Hey, wait a second! That's not my table! My table is A1:E8, not A3:E10. It moved it on me!

Fret not, you can tell excel that even when you fill a formula, that it should keep some references static.

How? By using a $. 

$A$1 means it will ALWAYS be A1.  
$A1 means that the 1 will increase as you fill down, but the A will never change, even if you go to the right.
A$1 is the opposite: 1 won't change if you fill down, but copying the formula to the right will increase A.


> **Tip:** You can select a cell (or part of an equation!) and hit <kbd>f4</kbd> to cycle through these.
{: .prompt-tip}

Let's look at that example from before again, with dollar signs:

![A correctly referenced VLookup range](excel10.png)

Look at that! Even though we dragged the formula down, the range reference remains the same. Thanks, $!

### Taking dollar sign references a step further

You can actually name cells and ranges!
So instead of having to remember that G15 is the total Q1 profit, you can name it Q1_PROFIT and reference it in equations.

Check it out:
![Excel's name box](excel11.png)

![Using a named cell in a formula](excel12.png)

You can also name entire ranges or tables, and [manage](https://support.microsoft.com/en-us/office/use-the-name-manager-in-excel-4d8c4c2b-9f7d-44e3-a3b4-9f61bd5c64e4) (delete or rename) cells you've named.

> **Tip:** You can even give one cell multiple names, so you can refer to it in different ways!
{: .prompt-tip}

## 9. Pivot tables

Pivot tables are one of Excel's silver bullets. They allow you to take a large, complicated set of data and break it down into small, meaningful bits. If you master pivot tables, you're utilizing a huge portion of Excel's functionality, and embracing one of its most beloved features. 

So what do they do?

*Use pivot tables to summarize complicated data or make interactive dashboards.*

For example, say you've got a sheet representing hundreds or thousands of orders for various products (apples, bananas, cucumbers, eggplants...) and you want to break it down and just answer the question "how much money did I make from each product?"

BAM, pivot table. Simply select a cell within your data, go to insert->tables->PivotTable, and choose your pivots. 

It's a little complicated at first, but there are no shortage of [guides](https://www.excel-easy.com/data-analysis/pivot-tables.html) and [tutorials](https://www.youtube.com/watch?v=F9WgF1K_K2g) to get your started.

You can also use pivot tables to summarize or aggregate your data by any field: region, month, produce item, what have you.

### Take pivot tables a step further with pivot charts

[Pivot charts](https://support.microsoft.com/en-us/office/create-a-pivotchart-c1b1e057-6990-4c38-b52b-8255538e7b1c) are automatically-updating charts that reflect data in a pivot table.

Combine multiple pivot tables to make a dashboard showing off whatever key metrics you care about.


## 10. Automation (VBA or Office Scripts)

This is the big one, the final strate of functionality that separates Excel Power users from the rest. With automation, you can set up tasks to execute on a click of a button that otherwise take manual time.

### What kinds of things can you automate?

* Generate a report from data. <br> Sure, if you're using pivot charts and dashboards, this might be done for you. But if you're exporting a report to PowerPoint or Word, this can save you time.
* Color-code rows based on the current data, flagging overdue items. <br> This is another are that can be done with conditional formatting, comparing against the `today()` function. Still, it can be useful to color-code, sort, and hide completed rows all with a click of a button, keeping your data clean and organized.
* Create data from a template (or restore a modifiable worksheet to a default template).<br> Useful for daily reports or worksheets that other people can modify pieces of.

### How do I automate?

Excel has two main ways of automation: [VBA](https://learn.microsoft.com/en-us/office/vba/library-reference/concepts/getting-started-with-vba-in-office) (Visual Basic for Applications) and [Office Scripts](https://techcommunity.microsoft.com/blog/excelblog/automate-your-tasks-with-the-automate-tab%E2%80%94now-in-excel-for-windows-and-mac/3705856). 

VBA is older, limited to desktop applications, and allows for interacting with other Office applications (such as Outlook, Word, or Powerpoint). Because it's been around for a while, there's a lot of great documentation and help available. Visual Basic as a language is meant to be English-like and easy to understand. 

Be careful running VBA macros you do not trust. Hackers like to use it to distribute malware.

Office Scripts is more modern, can run on desktop and web, and does not have the security concerns of VBA. It uses a language called TypeScript, which is powerful and popular, but more challenging to understand for beginners.

### Okay but how do I get started?

Pick a project that you want to automate, and jump in! You can use the [Macro Recorder](https://support.microsoft.com/en-us/office/automate-tasks-with-the-macro-recorder-974ef220-f716-4e01-b015-3ea70e64937b) (VBA) or [Action Recorder](https://support.microsoft.com/en-us/office/record-your-actions-as-office-scripts-453ab58d-708f-40a9-ab87-99a743bfa69a) (Office Scripts) to record yourself performing the actions you want to automate. When you are done, code will be generated for you, which you can use as-is, or modify to your specific needs. 

[StackOverflow](https://stackoverflow.com/questions/tagged/vba) is a great resource for finding answers to problems you may encounter, but be warned — they have a reputation for unfriendliness. Search for your questions before asking them, and be sure to follow any submission guidelines.

### Take automation a step further with power automate

[Power Automate](https://www.microsoft.com/en-us/power-platform/products/power-automate) is a third way of automation that doesn't use very much code at all! Rather, it provides connectors between applications, so you can send an email based on the value in a cell, or schedule a report to be sent via Teams.

## What did I miss?

Sound off in the comments if there's something I missed. Excel is a powerful, complicated behemoth, and I'm sure my 10 levels may look very different than your own.

<hr>

*Disclaimer: at the time of this writing, I am employed by Microsoft, and have worked on Excel and on the Office Scripts team specifically. These opinions are my own, and are not endorsed by my employer*
