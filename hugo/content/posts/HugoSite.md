---
title: "Making a completely free website"
date: 2021-09-25T17:13:46+01:00
draft: false
---

I embarked on trying to create a public website today, and, evidently, have suceeded. I currently cannot afford another domain, nor hosting for the website, so this is the story of how I made a, fully functional, free website.

# Hosting
My personal site is currently hosted on my VPS, but it is often a hassle to deal with. I am happy with that, for that site, as I feel it provides a good learning experience, but for this site I just wanted something that would work.
I looked for some way to host a website that was free, but also provided support for custom domains. Thankfully, I only wanted this site to be static, which made it all a lot easier. I settled on [https://pages.github.com](github-pages)

# Domain
I wanted to have a proper domain for this site, not some subdomain provided to me by github or whatever. I found [https://freenom.com](freenom), which - although seeming a little bit sketchy - seemed to have good reviews and, well, it worked... ish.
For whatever reason, the ".tk" domain endings just refused to work for me. Github pages just didn't see it existed. When I made one with ".ml", and exactly the same configuration, it worked almost instantly.
The freenom DNS servers are fairly slow (not unusabale, just not particuarly snappy), which is understandable for a free service. I tried to hook it up to Cloudflare, but it complained and gave errors about not being able to find the domain. Would potentially like to come back to this but it doesn't really matter enough.
All in all, for a free domain it works... good. Not great, but fine.

# Content
I ended up using [https://gohugo.io](Hugo) to put make this website - potential post about that coming soon - but it wasn't flawless with Github Pages. The first minor problem was trying to get it to like not being the parent git directory (the real one being the one for my website, including things like the CNAME file etc). Second was how it stored the static content it generated compared to how Github Pages wanted it. Pages could only read from either `/` or `/docs` as the static content, whereas hugo put any static content into a folder called `public` in it's root directory. I ended up just putting all the hugo stuff in a folder and manually copying it to the `docs` folder. It's annoying and nowhere near perfect, but it works, and isn't _too_ bad.
```
.
├── CNAME
├── docs
├── hugo
│   └── public
└── README.md
```

All in all, I think that it is definitely a feasable way to host a website for anyone interested. If you're willing to jump through a few minor hurdles (and probably a lot easier if I didn't spend time trying to deal with cloudflare). It seems good for a beginner website, or people such as myself on a budget.
May make a custom site later 😀
