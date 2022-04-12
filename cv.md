---
layout: post
title: CURRICULUM VITAE
image: assets/images/pic00.jpg
description: Resume rendered from markdown to pdf via github actions
nav-menu: true
---

* [PDF][2]
* [MD][1]

[1]:{{ aricg.github.io }}/Pandoc/resume.md
[2]:{{ aricg.github.io }}/Pandoc/resume.pdf

Resume rendered from markdown to pdf via [github actions](https://github.com/Aricg/aricg.github.io/blob/gh-pages/.github/workflows/pandoc.yml)


Docker makes using Pandoc in your builds easy, try it out:
{% highlight shell %}
#Pandoc interactive:
docker run -it --volume "$(pwd):/data" --entrypoint "/bin/sh" pandoc/latex

#Pandoc simple:
docker run -it --volume "$(pwd):/data" pandoc/latex input.md -o output.pdf
{% endhighlight %}



