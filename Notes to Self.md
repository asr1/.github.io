### Making a new Draft

jekyll draft "My new draft"  
jekyll rename _drafts/my-new-draft.md "My Renamed Draft"

### Publishing the Draft
jekyll publish _drafts/my-new-draft.md

### Serving locally with drafts
bundle exec jekyll s --drafts  
http://localhost:4000/

### Linking to another post
[Session 3. Getting started with Roll20]({% link _posts/2022-12-24-building-a-roll20-character-sheet-3.md%}) 

And doing it with an anchor:

Before we jump in, I'm going to repeat my {% capture link_with_anchor %}{% link _posts/2022-12-22-building-a-roll20-character-sheet-0-md.md %}#technology{% endcapture %}
[earlier suggestion]({{ link_with_anchor }})

### Filename after code:
```html
<!-- blah blah -->
```
{: file="characterSheet.html"}

### Footnotes

If everything's important, nothing is[^1]. 

at the end of the file:

[^1]: That's the plot of The Incredibles.