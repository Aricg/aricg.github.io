---
layout: post
title: CI/CD
description: Infrastructure as Code
image: assets/images/pic55.jpg
nav-menu: true
---

Pre-commit
----------
catch common errors and enforce standards before engaging your pipeline.
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
{% endhighlight %}


Commit early and often
----------------------
Good CI feedback encourages developers to merge their local changes with the main branch.

Communicate
-----------
What local tests do your developers run to smoke test their code? We want this in CI.

Enforce
-------
Enforce documentation on new features, docstrings on functions, release notes on releases.

Code-review
-----------
Your CI is only as good as your review, smaller diffs are easier to review, big changes languish.

Developers write their own tests
-----------------------------------------
Make it dead simple for them to add and tweak tests, put up the scaffolding and document it well.

Only alert on failure
----------------------
No news is good news, don't ping when we exit zero.

Infrastructure as code
----------------------
Everything needs to be code, everything needs machine and human review.

Gitops helpers
--------------
Provide your developers a way to trigger specific parts of the pipline with arguments
in their commit message.<br>
Put all triggers in the template by default, devs can delete the lines they don't need.
{% highlight shell %}
git config --global commit.template
git config --global commit.cleanup strip
{% endhighlight %}
[Rebase with comment](https://github.com/cirrus-actions/rebase)<br>
[Revert with a comment](https://github.com/marketplace/actions/automatic-revert)

Logging as feedback
-------------------
Alerts are only as observed as their signal to noise ratio.
Anomalies in logs, failures, Et al. should be treated as feedback.
For example, let the machine post to the conversational review of the merged patch set.
Now when you look back at the most recently merged code, you have context in the right place.

4am retrograde
---------------
It's free* to have a patchset proposing a revert of the most recent production change.
Stakeholders of the latest change and CI can provide proactive post-feedback as a matter of course:
  * Is this change safe to revert?
  * How does production look after the change? Anything potential concerns?
  * Anomaly monitoring can comment directly to this patchset.
Merge an already verified proposal if things went south.

