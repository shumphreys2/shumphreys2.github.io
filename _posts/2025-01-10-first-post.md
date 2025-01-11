---
title: "First Post"
date: 2025-01-10
layout: post
---

This blog uses GitHub Pages and a Jekyll theme.  I'll outline what I've done here for future reference.  

### Advantages of using GitHub Pages for me are:
- Using GitHub, which I need more experience using.
- Simple content management by having a collection of post files and assets.
- It's free for personal use.
- Easy editing of posts using Markdown files. These can be previewed in the web based editor on GitHub.
- Markdown reference: https://www.markdownguide.org/cheat-sheet/

First, thanks to Jorge Sanz for his helpful example pages:\
https://github.com/jsanz/gh-pages-minima-starter/tree/master

### Set up a GitHub account and create a repo to hold the blog.
- The repo name should be <user>.github.io.
- See the quick start for more details:\
  https://docs.github.com/en/pages/quickstart

### Add a README.md and _config.yml file to start.
- More files and sub-directories are added later
- https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/adding-content-to-your-github-pages-site-using-jekyll#about-content-in-jekyll-sites
- NOTE: As an alternative it should be possible to clone a working repo for an example blog.

### Set up the Source and Actions 
I'm using the GitHub Actions presently.
- Settings/Pages/Code and Deployment: Source:
-- Deploy from a branch, e.g. main, to require a push.
-- GitHub Actions to auto trigger builds and push to GitHub Pages.
- Actions/General:
-- Allow <user>, and select non-<user>, actions and reusable workflows
-- Allow actions created by GitHub
-- Allow actions by Marketplace verified creators

### Add local modifications to layouts, footer, etc.
- All that is required for modifications is to create the local dir/file and edit it.
- The full Jekyll theme does not need to be in the repo, just the local customized files.
- Example: _layouts/base.html, _includes/footer.html

### Add a first post
- Create post files under _posts, e.g. _posts/<date>-<short-description>.md
- The date format is yyyy-mm-dd.  Example, _posts/2025-01-10-first-post.md.

### Build and debug
- The build actions are set up to be triggered automatically on file updates or checkins.
- The only required steps are to monitor the build under Actions, and debug and errors.
- For example, an incorrect date format in a post file name will cause the build to fail.

### Check your deployed page(s) at <user>.github.io

