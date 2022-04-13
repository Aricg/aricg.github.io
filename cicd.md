---
layout: post
title: CI/CD
description: Empty Section
image: assets/images/pic55.jpg
nav-menu: true
---

Pre-commit: catch common errors and enforce standards before engaging your pipeline.
{% highlight shell %}

$ git commit -m "Add super awesome feature"
black....................................................................Passed
blacken-docs.........................................(no files to check)Skipped
Trim Trailing Whitespace.................................................Passed
Fix End of Files.........................................................Passed
Check Yaml...........................................(no files to check)Skipped
Debug Statements (Python)................................................Passed
Flake8...................................................................Passed
Reorder python imports...................................................Passed
pyupgrade................................................................Passed
rst ``code`` is two backticks........................(no files to check)Skipped
rst..................................................(no files to check)Skipped
changelog filenames..................................(no files to check)Skipped


Commit early and often
----------------------
Good CI feedback encourages developers to merge their local changes with the main branch.

Communicate
-----------
What local tests do your developers run to smoke test their code? We want this in CI

Enforce
-------
Enforce documentation on new features, docstrings on functions, release notes on releases.

Code-review
-----------
You CI is only as good as your review, smaller diffs are easier to review, but changes languish

Developers have to write their own tests
-----------------------------------------
Make it dead simple for them to add and tweak tests, put up the scafolding and document it well.

Only alert on failure
----------------------
No news is good news, don't ping for zero exits.

