---
layout: post
title:  "setting up the blog"
date:   2020-08-21 23:13:09 -0400
categories: blog
---

I found lots of tutorials on setting up a github pages blog with jekyll but none that had every step I did.  Here's every step I did.


*Disclaimer: This applies to jekyll v4*

## Installation of Repository/Ruby/Jekyll/Hydeout
1. Created new repo under my github account.  cloned repo locally and `cd` into that directory.
1.  Followed [these](https://jekyllrb.com/docs/installation/macos/) instructions to install ruby and jekyll

1. Created new site using `jekyll new blog`.  I then moved everything from the `/blog` folder back to root (not necessary, I just preferred it there).

1. Installed hydeout theme by adding `gem "jekyll-theme-hydeout", "~> 4.1"` to my Gemfile.  Ran `bundle install`.  (reference: https://github.com/fongandrew/hydeout)

## Configuring Jekyll 

1. Updates to _config.yml
```yml
title: kevin buckley
email: kbuckley17@gmail.com
description: >- 
  things I learn in tech
baseurl: "" # the subpath of your site, we are at root
url: "https://kevinbuckley.github.io" # the base hostname & protocol 

# Build settings
theme: jekyll-theme-hydeout # using the hydeout theme
plugins:
  - jekyll-feed  # adds the feed link to the sidebar
```
2. Added me.md page for contact info and such 

3. Removed post comments.  Did this by adding an empty file `_includes/comments.html`

4. Updated styles.  Added an `assets/css/main.scss` file.  Example here: 
```scss
---
# Jekyll needs front matter for SCSS files
---

$link-color: navy;
@import "hydeout";
```
5. Adding custom links to the sidebar by adding a `_includes/custom-icon-links.html` 
```html
<a id="github-link" class="icon" title="Github Project" aria-label="Github Project" href="{{ site.repo }}">
{% include svg/github.svg %}
</a>
```
6. Setting up a home page in `index.md` .  Show the last post I made.
```md
---
layout: post
title: ""
---
<h1>{{ site.posts.last.title }}</h1>
{{ site.posts.last.content }}

:point_right: please use the posts link to your left to see all posts :point_left:
```

## Time to add a post! 
1. Added my first post under `_posts/`.  Note the `yyyy-mm-dd-mytitle.md` name format.  Funnily enough, this is the first post! 

----
### resources: 
*  https://jekyllrb.com/docs/
* https://jekyllrb.com/docs/continuous-integration/github-actions/


