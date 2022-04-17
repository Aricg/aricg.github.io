---
layout: post
title: The Plan
description: Integrate ideas
image: assets/images/pic33.jpg
nav-menu: true
---


### I aim to tightly connect: Coding, building, testing, releasing, deploying and monitoring.

> I'd like to look over your current pipelines and talk together about them. Your hopes, your dreams, et al.

Part 1
------

Identify and itemize workflows:
* Ticket to Merged
* Alert to Revert
* Pick operators to sit down with after meetings and pair work for a span.
  * learn their systems, their workflows, itemize what takes up their time.

>My friend and co-worker Jessica had an unreasonable work load during release time, we analyzed her tickets.
With projects under her purveor growing past 100, promoting maven artifacts via a ticketing system had buckled.
I devised and implemented a release.yaml. Developers flag for promotion their own maven artifacts.
With some Nexus api integration we were soon able to programmatically verify and provide feedback, via gerrit comments and votes on the release.yaml patchsets.
Now Jessica simply had to review and approve 100 or so patches in gerrit during a release cycle.


Part 2
------

Creative work and deep thinking:
* Search for best practices, divine the winds of tomorrow and weave them into your dreams.
* Light research
* Proposal writing
* Iterate ideations

>The most time consuming daily task at the Linux Foundation was new project creation.
Each project needed a gerrit repo, mirrored to github, a jira project, maven repositories
and a group of committers backed by ldap. My idea was to create a yaml file per project in a central repository.
A jenkins job verified it's correctness and on merge all of the various pieces would be created.
This took writing various APIs into lftools and some build logic. At the end the info file was pushed into the newly created repo
and used henseforth to manage committers on the repo.


Part 3
------

Sprint Planning:

* Meet together and review proposals, create epics for the ones that pass review

> Daily tasks aside I really enjoy creating work for myself.
That said you need breathing room for this work model to pan out.

Part 4
------

Epic iteration:

* pros and cons to the proposed approach (they must exist)
* alternative approaches
* Write 'end user' documentation as a starting point:
  * Ensure that the entire workflow has been described
  * Identify and eliminate any remaining hand waving

>In the beginning there was a separate repository for all the documentation.
At release time there was endless chasing of teams to include their work in the docs repository.
Moving docs/ into each repo and including them in the master index with intersphinx linking (not submodules please)
really helped everyone reach their milestones, and put the onus where it belonged.

Part 5
------

Second sprint:

* Review the documentation as end goal
* Shake out any remaining hand waving
* Spec out tasks for epic

>Organizing documentation is not a simple task, common templates and guidielines can go a long way to helping encourage
developers to document their code, a flushed out index with stubs can help with this.

Part 6
------

Sprint as usual.

>I traveled to many events at my last job, it was great to see people in person.
Many ideas that would have not otherwise been were shared and acted on.

