### Making a new Draft
jekyll draft "My new draft"
jekyll rename _drafts/my-new-draft.md "My Renamed Draft"

### Publishing the Draft
jekyll publish _drafts/my-new-draft.md

### Serving locally with drafts
bundle exec jekyll s --drafts


### Linking to another post
[Session 3. Getting started with Roll20]({% link _posts/2022-12-24-building-a-roll20-character-sheet-3.md%}) 

### Filename after code:
```html
<!-- blah blah -->
```
{: file="characterSheet.html"}