---
layout: post
title: Approach
description: Insights on my approach
image: assets/images/pic33.jpg
nav-menu: true
---


### I craft tightly connected pipelines for Code, builds, tests, releases, deployments and monitoring.

> I would like to look over your current pipelines and talk together about them. Your hopes, your dreams..

1) Identify and itemize workflows
-------------------------------
* Ticket to merged
* Alert to revert
* Collect pain points
* Pick operators to sit down with after meetings:
  * learn their systems, their workflows, itemize what takes up their time

>My friend and co-worker Jessica had an unreasonable workload during release time.
We analyzed her tickets and found that with projects under her purview growing past 100,
the ticketing system the developers had been using to request promotion of their maven artifacts had buckled.
To address this, I devised and implemented a release.yaml. Developers could now flag for promotion a specified historical build on the artifact server.
With some Nexus api integration, we were soon able to programmatically verify and provide feedback.
Now that the verify job could vote and comment on developer submitted release.yaml patchsets both they and Jessica now had timely feedback during the busy release cycle.
After these changes, Jessica could simply review and approve 100 or so patchsets, reducing the back and forth inherit in a ticketing system.
This automation was soon expanded to include container releases as well.

2) Create work from problem discovery
-----------------------------------
* What is our delta from best practices, best in class
* Light research, deep thinking: divine the winds of tomorrow and weave them into your dreams
* Initial proposal writing

>The most time consuming daily task at the Linux Foundation was new project creation.
Each project needed a gerrit repo mirrored to github, a jira project, maven repositories
and an ldap group populated with committers. My idea was to create a yaml file per project in a central repository.
A jenkins job verified it's correctness and on merge all of the various pieces would be created.
This took writing various APIs into lftools and some build logic. After the assets were created the info file was pushed into said newly created repo
and used henceforth for self-management of committers in that repository.


3) Proposal, sharing
------------------

* Meet together and review proposals
* Move forward with the ones you like

> Daily tasks aside, I really enjoy creating work for myself and collaborating with co-workers.
That said, the entire team needs breathing room for this work model to track.

4) Iterate, double-check
----------------------

* Itemize pros and cons (they must exist)
* Visit alternative approaches
* Present these and discuss

>In the beginning, there was a separate repository for all documentation,
which meant that at release time we were constantly chasing after teams to submit their work in the docs repository.
Moving docs/ into each repo and including them in the master index with intersphinx linking (not submodules please)
really helped everyone reach their milestones and put the onus to submit documentation where it belonged.


5) Sprint Planning
----------------

* Spec out Epic and its tasks.
* Ensure the end-to-end workflow has been adequately described
* Consider writing 'end user' documentation as a starting point:
  * This can help eliminate hand waving

### Organizing documentation can be a simple task if we have strong guiding principles and a flushed out index to guide developers.

>There isn’t one thing called documentation, there are four.\
Tutorials:\
Learning precipitates from the concrete to the abstract, you don't want explanations in your tutorials. you want the user 'to do'.
Don't give the user options, you are creating a service for them. Concrete actions that build confidence, a tutorial will turn your learner into a user.\
How to guides:\
problem oriented, ie: take the user through the steps to solve common problems. Analogy: a recipie\
Reference guides:\
Code determined, these only have one job. Technical description of the machinery and how to operate it.
With guiding principles of structure, consistency, description and accuracy, this is often the only type of documentation a developer can imagine writing.\
Explanation/background/discussion:\
This is understanding oriented. Explains why things are they way they are. Can discuss multiple options: (eg for a deployment)\
Above all do not mix these catagories in your documentation or the overall quality will fall.
Be mindful: They represent four different purposes or functions, and require different approaches to their creation.



6) Sprint Review
-------------

* Review Epics, tasks and documentation as end goal
* Shake out any remaining hand waving

>My manager Andy had great ideas but very little time.
He saw that a git-ops JcasC implementation would eliminate an entire class of tickets from our helpdesk and tasked me with bringing his idea to life.
Andy could clearly disseminate his ideas and would succinctly review my epics ensuring their end to end consistency.
Because his ideas were flushed out from the outset, I was able to complete the task to his specifications without blocking issues arising.
