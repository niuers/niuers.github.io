---
title: "How to setup a blog using github"
date: 2020-07-21
categories:
  - blog
tags:
  - Jekyll
  - github
---

I want a blog to have following properties:
1. Developer friendly: Support code, math formula and jupyter notebook.
1. Can hook up with github so I can manage the contents with github.
1. Have control of the Ads.
1. Have the functionalities to classify posts by tags.
1. Be able to add static pages (non-blog)

The [github pages][github-pages] + [jekyll][jekyll] combination seems to satisfy all the above requirements. With a bit research, I found [Minimal Mistakes theme][mmistakes] just works for me.

Here are the steps I used to setup this blog:
1. Start with [Minimal Mistakes remote theme starter][mmistakes-starter] to create a repository. (Instead of starting from the [Minimal Mistakes Repository on GitHub][mmistakes], which is more complicate to follow)
  * Follow the instruction to create a repository from the starter template
  * Note, I don't suggest to use "username.github.io" as the repository name here, since it will always display "This is generated from template ...", which I don't like.
1. [Create your github pages][github-page-create] if you don't have one already.
1. On your local computer, clone both repositories into your local drive.
1. Copy everything from the repository of "minimal mistakes" to your empty github page repository.
1. Check-in your github page repository to github.com. Wait a few minutes, your webiste should be ready at: your-user-name.github.io.
1. Now you have a blog!


[github-pages]: https://pages.github.com/
[jekyll]: https://jekyllrb.com/
[mmistakes]: https://github.com/mmistakes/minimal-mistakes
[mmistakes-starter]: https://github.com/mmistakes/mm-github-pages-starter/generate
[github-page-create]: https://guides.github.com/features/pages/
