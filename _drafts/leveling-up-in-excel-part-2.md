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

## Taking dollar sign references a step further

You can actually name cells and ranges!
So instead of having to remember that G15 is the total Q1 profit, you can name it Q1_PROFIT and reference it in equations.

Check it out:
![Excel's name box](excel11.png)

![Using a named cell in a formula](excel12.png)

You can also name entire ranges or tables, and [manage](https://support.microsoft.com/en-us/office/use-the-name-manager-in-excel-4d8c4c2b-9f7d-44e3-a3b4-9f61bd5c64e4) (delete or rename) cells you've named.

> **Tip:** You can even give one cell multiple names, so you can refer to it in different ways!
{: .prompt-tip}

## 9. Pivot tables



## 10. Automation (VBA or Office Scripts)

## What did I miss?

Sound off in the comments if there's something I missed.

<hr>

*Disclaimer: at the time of this writing, I am employed by Microsoft, and have worked on Excel. These opinions are my own, and are not endorsed by my employer*