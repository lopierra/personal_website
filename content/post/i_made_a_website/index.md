---
title: "I made a website!"
author: "Pierrette Lo"
date: 2020-05-03
categories: ["R"]
tags: ["R Markdown", "blogdown", "website"]
summary: Finally decided to see what this whole {blogdown} thing is about
---
 
## Hello, world!

There is a lot of great information out there about blogdown, Hugo, and the Academic theme that I chose for my site. I wanted to list my references here, as well as (mostly for my future self) the actual things I did to build this site.

Skip down for [references](#references).

## My process (a work in progress)

### 1. Create new Github repo for the site

### 2. Create new RStudio project from the Github repo

### 3. Install {blogdown} and {hugo}

```
devtools::install_github("rstudio/blogdown")

blogdown::install_hugo()
```

### 4. Edit `.gitignore`

```
.Rproj.user
.Rhistory
.RData
.Ruserdata
blogdown
Thumbs.db # if a Mac user, .DS_Store instead  
public/ # if using Netlify
```

### 5. Create example site with Academic theme

```
blogdown::new_site(theme = "gcushen/hugo-academic", 
                   theme_example = TRUE)
```

### 6. Personalize content

Add my author info:

* Change content > authors > rename folder "admin" to "pierrette"
* Then change user to display in content > home > `about.md`
* Fill in or comment out information in config > _default > `params.toml`

Site setup:

* Modify root > `config.toml` to change title & copyright
* Change theme, font size, etc. in config > _default > `params.toml`
* Modify navigation links in config > _default > `menus.toml`
* Add blogdown link to the site footer in themes > hugo-academic > layouts > partials > `site_footer.html`
  * Also comment out the "Privacy Policy/Terms" part of the footer

Content:

* Modify info in pages in the `home` folder
  * These can be "widgets" that appear on your home page, and/or separate pages with menu links
* Remove sections (eg. "Demo", "hero") without deleting the actual content by going to content > home > demo.md and changing `active = false`
* Or just delete the content and refer back to the [example site](https://github.com/gcushen/hugo-academic/tree/master/exampleSite) if needed

Add-ins:

* "Serve Site" to see it refresh live in the viewer as you work
  * See [this](https://github.com/rstudio/blogdown/issues/404) if it keeps opening new browser tabs every time you save
* "Insert Image" for blog posts/projects so you don't have to use the shameful Paint 3D cheat to resize the image
* "New Post" instead of manually creating a new post folder

Future directions:

* Figure out an efficient workflow for when I have 10 open files called `index.md` :thinking:

### 7. Commit changes and push to GitHub

* **PRO TIP:** Don't name any of your post folders "blogdown"! It will be .git-ignored, and you will waste 2 hours trying to figure out why your post isn't showing up on your deployed site. :facepalm:
* Also, there will be a large amount of files to commit the first time. RStudio kept hanging when I tried to use the Git pane to commit everything - next time use the shell instead.

### 8. Deploy!

* **PRO TIP:** Don't try to do this for the first time "on your way to bed" at 11 pm.
* Sign up for Netlify account (instructions [here](https://alison.rbind.io/post/2017-06-12-up-and-running-with-blogdown/#build-your-site-in-rstudio))
* Select `New site from Git -> Continuous Deployment: GitHub`
* Connect Netlify to GitHub and select repo
* Check Hugo version in RStudio console using `blogdown::hugo_version()` and add `HUGO_VERSION` variable in Advanced build settings (instructions [here](https://alison.rbind.io/post/2019-02-19-hugo-netlify-toml/))
* Create a new text file in project root directory called `netlify.toml`; specify your hugo version
* Change site name at Netlify dashboard -> Domain settings -> Options
* Update baseurl with new URL in `config.toml`
* Get an rbind.io domain name [here](https://github.com/rbind/support/issues)
* *Note:* The `public` folder is recreated every time you serve/build your site. If things get weird, try deleting the whole folder locally or on GitHub. I did this after noticing that the first time around, all of the example content I deleted was still in the `public` folder. 

---

## References

### Official documentation

* [blogdown: Creating Websites with R Markdown](https://bookdown.org/yihui/blogdown/), by Yihui Xie, Amber Thomas & Alison Presmanes Hill
* [Documentation for the Hugo Academic theme](https://sourcethemes.com/academic/docs/), by George Cushen
* [Academic theme example site](https://github.com/gcushen/hugo-academic/tree/master/exampleSite)

### Quicker-start guides

* [Up & running with blogdown](https://alison.rbind.io/post/2017-06-12-up-and-running-with-blogdown/), by Alison Hill
* [Creating a website with the academic theme in blogdown](https://www.kevinzolea.com/post/blogdown/creating-a-website-with-the-academic-theme-in-blogdown/), by Kevin Zolea
* [Overwhelmed by Hugo academic theme: a beginner's guide](https://andreaczhang.rbind.io/post/my-1st-blogpost/), by Chi Zhang

### Troubleshooting/tips

* [A spoonful of Hugo: The netlify.toml file](https://alison.rbind.io/post/2019-02-19-hugo-netlify-toml/), by Alison Hill
* [A spoonful of Hugo: Troubleshooting your build](https://alison.rbind.io/post/2019-03-04-hugo-troubleshooting/), by Alison Hill
* [A blogdown new post workflow with GitHub and Netlify](https://www.garrickadenbuie.com/blog/blogdown-netlify-new-post-workflow/), by Garrick Aden-Buie
* [Handy list of markdown emojis](https://gist.github.com/rxaviers/7360908)
* [blogdown:::serve_site() keeps opening new browser tabs](https://github.com/rstudio/blogdown/issues/404)

