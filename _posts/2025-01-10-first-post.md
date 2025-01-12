---
title: "First Post"
date: 2025-01-10
layout: post
---

This blog uses GitHub Pages and a Jekyll theme.  I've outlined what I've done to get the blog up and running here for future reference.  

### Advantages of using GitHub Pages:
- Using GitHub, local repos, etc. which I need more experience using.
- Simple content management with a simple collection of "post" files and assets like images.
- Easy editing of posts using Markdown files. These can be previewed in the web based editor on GitHub.
- It's free for personal use.

Thanks to Jorge Sanz for his helpful example pages:  
&nbsp;&nbsp;&nbsp;&nbsp;<https://github.com/jsanz/gh-pages-minima-starter>

### Set up a GitHub account and create a repo to hold the blog.
- The repo name should be \<user\>.github.io.
- See the quick start for more details:\
  <https://docs.github.com/en/pages/quickstart>

### Add a few required files to start
- README.md, _config.yml, Gemfile
- More files and sub-directories are added later for posts and customization. For details, see:
  <https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/adding-content-to-your-github-pages-site-using-jekyll#about-content-in-jekyll-sites>
- Other notes: 
  - As an alternative it should be possible to clone a working repo for an example blog..
  - Note: I'm not 100% certain a Gemfile is required for a GitHub Action based deployment.

### Set up the Source and Actions 
I'm using the GitHub Actions presently.
- Settings/Pages/Code and Deployment: Source:
  - Deploy from a branch, e.g. main, to require a push.
  - GitHub Actions to auto trigger builds and push to GitHub Pages.
- Actions/General:
  - Allow \<user\>, and select non-\<user\>, actions and reusable workflows
  - Allow actions created by GitHub
  - Allow actions by Marketplace verified creators

### Add local modifications to layouts, footer, etc.
- All that is required for modifications is to create the local dir/file and edit it.
- The full Jekyll theme does not need to be in the repo, just the local customized files.
  - Example: _layouts/base.html, _includes/footer.html
- Update _config.yml for the theme, header and footer fields.
  - This blog uses the jekyll/minima repo, rather than the built in version in GitHub:
    `remote_theme: jekyll/minima`
  - Read through the jekyll/minima/_config.yaml file for additional options.

### Add a first post
- Create post files under _posts, e.g. _posts/\<date\>-\<short-description\>.md
- The date format is yyyy-mm-dd.  Example, _posts/2025-01-10-first-post.md.

### Build and debug
- The build actions are set up to be triggered automatically on file updates or checkins.
- The only required steps are to monitor the build under Actions, and debug and errors.
- For example, an incorrect date format in a post file name will cause the build to fail.

### Check your deployed site at \<user>.github.io

### Install Ruby and Jekyll to preview pages locally
- Initial instructions are at the github pages site:  
  <https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/testing-your-github-pages-site-locally-with-jekyll>
- Further instructions for Ubuntu:  
`sudo apt-get install ruby-dev ruby-bundler`
- Run bundle install once in the local repo.  Then start a local server with:  
`bundle exec jekyll serve --baseurl=""`

### Other modifications and options
- Created a Personal Access Token (PAT) to allow git pushes from a local repo.
- Note: Checkouts are done using the PAT in the URL. See:  
  <https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens>
- Added and modified the Gemfile to use ubuntu-22.04 specifically, after build errors.
- Using the jekyll/minima remote theme instead of the GitHub built-in older version.
- Add the `jekyll-seo-tag` plugin to add SEO metadata to the generated html pages.
- Use ghostwriter to edit and preview Markdown locally even before a jekyll build. (Includes spell checking!) Available here:  
  <https://ghostwriter.kde.org/>

### Additional References
Markdown
- <https://www.markdownguide.org/cheat-sheet/>
- <https://www.markdownguide.org/basic-syntax>
