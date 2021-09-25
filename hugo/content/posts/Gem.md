---
title: "Gem"
date: 2021-09-25T16:27:13+01:00
draft: false
---

# What I Used
Finally finished setting up my Website and Gemini Capsule. I thought I should document what i used to create it

## Converting from GMI to HTML
I wanted to ensure that my site wasn't only limited to gemini, but I really didn't want to write HTML for everything. I was originally going to try to regex it all out, as I noticed HexDSL and Uoou doing, but this was cumbersome and i couldn't be bothered. After a bit of digging around, I found "gmi-to-html" on github, which served exactly as I needed. I wrote a small bash script to automate setting everything up and it worked well, after a little bit of faffing around. My main problem was my monkey brain not noticing that "sugar" in the arch repos wasn't the same as the one linked on the site... yeah, that took too much of my time :v

## Making new blog posts
Again, I didn't want to manually deal with blog posts like this one, so i wrote another tiny little script to automate it, from making the file and adding in basic template-y stuff, it worked well. My main problem here occured when trying to add a link to the main page for the blog post automatically, but I ended up bodgeing it by using line numbers (I had originally wanted to search for a specific string in the file). In the future, I am wondering if I might have to figure out how to limit the number of blog posts, but for now I dont see it being particuarly necessary, as I dont anticipate writing much here, and I don't really want to have a blog homepage as well as the main one.

## Hosting
I put it onto my Vultr VPS, and setup the server using Agate, a tiny little gemini server that does everything I need.


