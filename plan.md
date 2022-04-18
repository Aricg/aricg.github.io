---
layout: post
title: Proposal
description: Insights on my approach
image: assets/images/pic33.jpg
nav-menu: true
---


### I aim to tightly connect: Coding, building, testing, releasing, deploying and monitoring.

> I'd like to look over your current pipelines and talk together about them. Your hopes, your dreams, et al.

Identify and itemize workflows:
-------------------------------
* Ticket to Merged
* Alert to Revert
* Collect pain points
* Pick operators to sit down with after meetings:
  * learn their systems, their workflows, itemize what takes up their time.

>My friend and co-worker Jessica had an unreasonable work load during release time, we analyzed her tickets.
With projects under her purveor growing past 100, promoting maven artifacts via a ticketing system had buckled.
I devised and implemented a release.yaml. Developers flag for promotion their own maven artifacts.
With some Nexus api integration we were soon able to programmatically verify and provide feedback, via gerrit comments and votes on the release.yaml patchsets.
Now Jessica simply had to review and approve 100 or so patches in gerrit during a release cycle.


Create work from problem discovery:
-----------------------------------
* What is our delta from best practices, best in class.
* Light research, deep thinking: divine the winds of tomorrow and weave them into your dreams.
* Initial proposal writing.

>The most time consuming daily task at the Linux Foundation was new project creation.
Each project needed a gerrit repo mirrored to github, a jira project, maven repositories
and an ldap group populated with committers. My idea was to create a yaml file per project in a central repository.
A jenkins job verified it's correctness and on merge all of the various pieces would be created.
This took writing various APIs into lftools and some build logic. After the assets were created the info file was pushed into said newly created repo
and used henceforth for self-management of committers in that repository.


Proposal, sharing:
------------------

* Meet together, review proposals.
* Move forward with the ones you like.

> Daily tasks aside I really enjoy creating work for myself.
That said you need breathing room for this work model.

Iterate, double-check:
----------------------

* Itemize pros and cons (they must exist)
* Visit alternative approaches.
* present these and discuss.

>In the beginning there was a separate repository for all documentation.
At release time there was endless chasing of teams to submit their work in the docs repository.
Moving docs/ into each repo and including them in the master index with intersphinx linking (not submodules please)
really helped everyone reach their milestones, and importantly put the onus where it belonged.

Sprint Planning:
----------------

* Spec out Epic and its tasks.
  * Ensure the end-to-end workflow has been adequately described
* Consider writing 'end user' documentation as a starting point:
  * This can help eliminate hand waving.

>Organizing documentation is not a simple task, common templates and guidielines can go a long way to helping encourage
developers to document their code, a flushed out index with stubs can help with this.\
If you can’t figure out how to organize your material, try this: Write down ideas in random order, then sort them.

Sprint Review
-------------

* Review Epics, tasks and documentation as end goal.
* Shake out any remaining hand waving.

>My manager Andy had great ideas and no time.
He saw that a git-ops JcasC implementation would eliminate an entire class of tickets from our helpdesk.
Andy could clearly disseminate his ideas and would succinctly review my epics ensuring their end to end consistency.
I was able to complete his assigned work without being blocked as his ideas were flushed out before he set them upon me.

