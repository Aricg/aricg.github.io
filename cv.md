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
<details>
<summary> pandoc.yml </summary>
{% highlight yaml%}
name: Pandoc
on:
  push:
    paths:
      - "Pandoc/**"
    branches:
      - gh-pages

jobs:
  convert_via_pandoc:
    runs-on: ubuntu-18.04
    steps:
      - name: Set up Git repository
        uses: actions/checkout@v3
      - name: Convert with Pandoc
        uses: docker://pandoc/latex
        with:
          args: >-
            -o Pandoc/resume.pdf
            Pandoc/resume.md
      - name: Commit PDF
        run: |
          git config user.name github-actions
          git config user.email github-actions@github.com
          git add Pandoc/resume.pdf
          git commit -m "Push resume.pdf"
          git push
      - uses: actions/upload-artifact@master
        with:
          name: resume.pdf
          path: Pandoc/resume.pdf

{% endhighlight %}
</details>

<br>
Docker makes using Pandoc in your builds easy, try it out:
{% highlight shell %}
#Pandoc interactive:
docker run -it --volume "$(pwd):/data" --entrypoint "/bin/sh" pandoc/latex

#Pandoc simple:
docker run -it --volume "$(pwd):/data" pandoc/latex input.md -o output.pdf
{% endhighlight %}



