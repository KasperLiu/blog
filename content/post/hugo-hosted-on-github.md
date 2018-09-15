---
title: "Hugo Hosted on Github"
date: 2018-09-14T16:38:52+08:00
draft: false
lastmod: 2018-09-15T12:08:52+08:00
description: "a tutorial for hosting a home page on github with hugo"
tags: ["hugo", "github"]
categories: ["web"]

# You can also close(false) or open(true) something for this content.
# P.S. comment can only be closed
comment: false
toc: true
autoCollapseToc: false
postMetaInFooter: true
hiddenFromHomePage: false
# You can also define another contentCopyright. e.g. contentCopyright: "This is another copyright."
contentCopyright: false
reward: false
mathjax: false
# 即可進行inline latex渲染
mathjaxEnableSingleDollar: false
# 公式自动编号
mathjaxEnableAutoNumber: false

# You unlisted posts you might want not want the header or footer to show
hideHeaderAndFooter: false

# You can enable or disable out-of-date content warning for individual post.
# Comment this out to use the global config.
#enableOutdatedInfoWarning: false

# 流程图 
flowchartDiagrams:
  enable: false
  options: ""

# 序列图 see: https://blog.olowolo.com/example-site/post/js-sequence-diagrams/
sequenceDiagrams: 
  enable: false
  options: ""
---

____
# Prepare
before deploying Hugo as a personal home page hosted on Github, there are some basic steps to complete:

- a [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) version greater than v2.8 has been installed.  
- a [Github Pages](https://help.github.com/articles/user-organization-and-project-pages/), e.g. `<Username>.github.io`.
- [Hugo](https://gohugo.io/getting-started/installing/) installed.

____
# Deploying
step by step to deploy:

- create a new repository `e.g. blog` to maintain Hugo's content (personal blogs) and other source files.
- `git clone <new repository>` to your workspace and go into the path `e.g. ~/workspace/blog`.
- initiate a web site with command `hugo new site mysite` and copy all the contents of the project `mysite`, then delete the project `mysite`.
- now, run `hugo new posts/my-first-post.md` to create a content file and use `hugo server -D` to make website work locally on `http://localhost:1313`.
- stop the server with <kbd>Ctrl</kbd> + <kbd>C</kbd> and run `rm -rf public` to completely remove the `public` directory.
- now, make this new repository's `public` directory link to Github pages(`<Username>.github.io`) with the command `git submodule add -b master git@github.com:<USERNAME>/<USERNAME>.github.io.git public`. When running the `hugo` command to build the site to `public`, the created `public` directory will have a remote origin.
- run `hugo && cd public` and then **make a pull request to Github pages** and open browser to `https://<USERNAME>.github.io` to see the site.

Now, the above steps make hugo deployed on Github pages. It can automate some of these steps with the following script `deploy.sh`:

```bash
#!/bin/bash

echo -e "\033[0;32mDeploying updates to GitHub...\033[0m"

# Build the project.
# if using a theme, replace with `hugo -t <YOURTHEME>`
hugo --baseUrl="https://<USERNAME>.github.io/"

# Go To Public folder
cd public
# Add changes to git.
git add .

# Commit changes.
msg="rebuilding site `date`"
if [ $# -eq 1 ]
  then msg="$1"
fi
git commit -m "$msg"

# Push source and build repos.
git push origin master

# Come Back up to the Project Root
cd ..
```

so, integrate creating content and deploying script together:

```bash
#!/bin/bash
hugo new posts/new-post.md

# edit new post

# release post
./deploy.sh "Your optional commit message"
```

____
# Adding a theme
Consider about adding a theme for Hugo, go to [themes.gohugo.io](https://themes.gohugo.io/) for a beautiful one. Here uses [Even](https://github.com/olOwOlo/hugo-theme-even) for example.

- go back to the new repository directory. `e.g. ~/workspace/blog`.
- add a new theme as a submodule: `git submodule add https://github.com/olOwOlo/hugo-theme-even themes/even`
- To use the Even, copy and replace the `config.toml(themes/even/exampleSite/config.toml)` in the root folder of Hugo site `~/workspace/blog`.
- check the theme work successfully with `hugo server -D`.

Then, we can customize the theme as we want. But firstly we should take an overview of `config.toml` to know more about Hugo.
____
# Reference
1.[Hugo: Host on GitHub](https://gohugo.io/hosting-and-deployment/hosting-on-github/)  
2.[Hugo: Quick Start](https://gohugo.io/getting-started/quick-start/)  
3.[Hugo-Theme-Even](https://github.com/olOwOlo/hugo-theme-even)