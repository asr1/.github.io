---
layout: post
title: 'Road to Glory: what''s in a name?'
categories:
- Road to Glory
tags:
- code
- game-design
- rpg
- glorydays
img_path: "../../assets/img/"
image:
  path: templateHeaders/glorydays.png
  alt: Glorydays
date: 2025-08-06 14:30 -0700
---
*This is part of a series about Glorydays*, my upcoming roleplaying game where you create a teenage soap opera tv about aliens pretending to be high schoolers.*

Two facts: 

1. Glorydays takes place in 2003. 
2. The single most useful tool as a GM is a list of names.

I needed to create a list of names that would be appropriate for high schoolers in 2003. How do I do that?

First, I need a list of names. Easy enough, the [Social Security Administration](https://www.ssa.gov/oact/babynames/) provides a convenient list of baby names per year in the US. You can even get it as a CSV (comma separated value) file. Great!

This file goes back to 1880 and includes each name as a percent for how popular it was that year, as a portion of all registered names.

```csv
"year","name","percent","sex"
1880,"John",0.081541,"boy"
1880,"William",0.080511,"boy"
1880,"James",0.050057,"boy"
```

Time to write sme code. I decided to use Python for this, since it's pretty good for quick data manipulation.

The first thing I did was iterate through each row of the file, splitting on commas, and getting the name, the year, and the percent.

Then I wanted to sort these names by year. I created a simple map where for a given year, I can get every name and how common the name was that year. If I type in 2001, I'll get "Jacob",0.015734 (and a whole bunch of other names). I don't care about the sex column, so I'm ignoring it.

The game takes place in 2003, so we're looking for kids born between 1985 and 1990. These are going to be high schoolers in 2003, we we're only looking for names in that time period. Easy enough to add a filter.

Finally, there's WAY too many names here, including ones where only a single person had that name[^1]. So we want to have a cutoff, only showing names where at least 0.01% of people had that name that year.

And viola! That gives us a list that isn't too long of popular names in that period.

## Names

I took this list, and added some names from other countries as well, using similar methods. The default setting for Glorydays is Apple Grove, New Mexico, so I wanted to keep the focus American, but not strictly so — especially if your alien is going to pass as a foreign exchange student (one option of many)!

This list will be published as part of Appendix II: Resources in Glorydays.

Nicole, Colin, Asher, Cole, Megan, Tanya, Mathiu, Ellie, Grace, Dylan, Ian, Emily, Dominic, Joshua, Blaise, Isabel, Zane, Amaya, Aidan, Myla, Holiday, Atlas, Mayo, Nile, Forest, Shipley, Arch, Lynn, Alexis, Joaquim, Chad, Madhi, Wharton, Amos, Langley, Milligan, Shannon, Hannah, Angel, Caldwell, Ishita, Mac, Ashley, Xyla, Allison, Wei, Leslie, Tucker, Grey, Winter, Andrea, Miguel, Bird, Anna, Flavio, Klara, Bailey, Russel, Francesca, Ryan, Amanda, Sarah, Stephanie, Jennifer, Michelle, Justin, Andy, Kep, James, Kevin, Lisa, Natasha, Verica, Versey, Benoit, Tiffany, Vani, Julian, Mauricio, Aaron, Bilal, Gill, Deven, Chrissy, Cat, Reid, Zane, Robin, Brittany, Bishop, Santiago, Heather, Mila, Savannah, Diego, Luis, Alicia, Kelly, Angela, Isobel, Shawn, Amber, Tara, Crystal, Sabrina, Joel, Sara, Iris, Mitchel, Jet, Dustin, Evan, Bruce, Jenna, Diana, Justine, Raoul, Jessica, Mehda, Maria, Jillian, Carly, Krista, Sofia, Paul, Jamie, Lucia, Vincent, Luka, Darren, Jared, Riley, Graham, Geoffrey, Annamaria, Jaclyn, Jeff, Monica, Chantal, Dana, Lindsey, Wesley, Simon, Kit, Christian, Leah, Anibal, Florence, Alonso, Victor, Abdul, Ofelia, Caleb, Marcos, Yav, Duane, Salvador, Felipe, Rohit, Gonzalo, Sybil, Varsha, Lucia, Sofia, Martina, Natalie, Valeria, Julia, Paula, Meredith, Kristoff, Pryanka, Emma, Meadow, Melissa, Petra, Christy, Cameron, Hailie, Jaiden, Tyshawn, Jahir, Gavin, Balaji, Alana, Rebecca, Erica, Jade, Kiara, Kendra, Thalia, Kelsey, Red, Lyla, Katelyn, Skylar, Stella, Shaylee, Shawnee, Shale, Kade, Rick, Corbin, Taylor, Luca, Kenzie, Dakota, Adam, Andrew, Anthony, Brandon, Brian, Christopher, Daniel, David, Elizabeth, Eric, Jason, John, Jonathan, Joseph, Kyle, Lauren, Matthew, Michael, Nicholas, Robert, Samantha, William, Luis

## Code

If you care, the code used is reproduced below. I don't use Python often, and have no formal training in it. This code is "correct" in that it gave me a useful answer. No part of it should be treated as a best practice.

```python
import string 
  
names = []
yearDict = {}
title = True

with open('baby-names.csv') as f:
  for row in f:
    name = row.split(',')[1]
    name = name.replace('"','')
    year = row.split(',')[0]
    percent = row.split(',')[2]
    if title:
      title = False # There is almost certainly a better way to ignore the first column!
      continue

    if year not in yearDict:
      yearDict[year] = []
    yearDict[year].append((name, percent))
    names.append(name)
  
result = set() # A set ensures that each name will only be added once.

for year in range(1985, 1990):
  for name, percent in yearDict[str(year)]:
    if float(percent) >= 0.01: # We could lower this if we want more names, or raise it if we want fewer.
      result.add(name)
      
result_list = sorted(result)
print(result_list)
  
alphabet = string.ascii_lowercase
```

## Name coverage

As an aside, I used the same data to answer the question "What is the smallest set of names that can be used to have every letter of the alphabet represented". My naive solution was Jacqueline, Evan, Timothy, Alex, Wade, Zane, Frank, Gus, Pablo. I eventually used code to solve the same (you can find the whole [saga on Bluesky](https://bsky.app/profile/alexrinehart.bsky.social/post/3lo4rsce4e22h)). I was able to tweak weights for my definition of common, but it's inital set was:
Squire Alexander Fitzhugh Joseph Keyshawn Maverick Robert.

## Conclusion

1. Glorydays is being built.
2. Playing around with names is fun.
3. GM tools are useful, and there was almost certainly a better way to come up with this list!


[^1]: Impossible to tell directly from this data, as low results appear as a percentage, often in scientific notation, like 2000,"Dillion",7.1e-05,"boy".