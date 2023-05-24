---
layout: post
title: Approach
description: Insights on my approach
image: assets/images/pic33.jpg
nav-menu: true
---


### I craft tightly connected pipelines for code, builds, tests, releases, deployments, and monitoring, leveraging AI, Kubernetes, and Containers.

> Let's discuss your current pipelines, your aspirations, and your challenges.

1) Identify and itemize workflows
-------------------------------
* Ticket to merged
* Alert to revert
* Collect pain points
* Pick operators to sit down with after meetings:
  * learn their systems, their workflows, itemize what takes up their time

>My colleague Jessica was overwhelmed during release time due to the sheer number of projects under her purview. To alleviate this, I implemented a release.yaml that allowed developers to flag a specific historical build for promotion on the artifact server. With Nexus API integration, we could programmatically verify and provide feedback, reducing the back and forth inherent in a ticketing system. This automation was later expanded to include container releases as well.

2) Create work from problem discovery
-----------------------------------
* Identify gaps from best practices and industry standards
* Conduct research, think deeply, and anticipate future trends
* Draft initial proposals


>The most time-consuming daily task at the Linux Foundation was new project creation. To streamline this, I created a yaml file per project in a central repository. Upon merging, all the necessary assets were created. This required writing various APIs into lftools and additional build logic.


3) Proposal, sharing
------------------

* Review proposals together
* Proceed with the ones that resonate


>I enjoy creating work for myself and collaborating with co-workers. However, it's essential that the entire team has breathing room for this work model to be effective.


4) Iterate, double-check
----------------------

* List pros and cons
* Explore alternative approaches
* Discuss these alternatives


>Initially, documentation was in a separate repository, which led to a scramble at release time to get teams to submit their work. Moving docs/ into each repo and linking them with intersphinx (not submodules, please) helped everyone reach their milestones.


5) Sprint Planning
----------------

* Detail the Epic and its tasks
* Ensure the end-to-end workflow is adequately described
* Consider writing 'end user' documentation as a starting point


### Organizing documentation can be a simple task if we have strong guiding principles and a well-structured index to guide developers.


>Documentation is multifaceted. It includes tutorials, how-to guides, reference guides, and explanations or discussions. Each serves a different purpose and requires a different approach. Mixing these categories can lead to a decline in overall quality.


6) Sprint Review
-------------

* Review Epics, tasks and documentation as end goal
* Eliminate any remaining ambiguities

>My manager Andy had great ideas but very little time. He envisioned a git-ops JCasC implementation that would eliminate an entire class of tickets from our helpdesk. Andy could clearly disseminate his ideas and would succinctly review my epics, ensuring their end-to-end consistency. Because his ideas were well thought out from the outset, I was able to complete the task to his specifications without encountering blocking issues.
