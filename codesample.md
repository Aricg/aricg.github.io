---
#layout: page
layout: post
title: Specimen
description: Code Contributions
image: assets/images/pic01.jpg
nav-menu: true
---


<!-- Main
<div id="main" class="alt">
<section id="one">
	<div class="inner">
<p>Here are some code snippits with links to their souce on github</p>
-->


<header class="major">
  <h1>Work Specimines</h1>
</header>

LFTOOLS/GLOBAL-JJB
-------

* LFtools is a CLI script that acts as the glue between components in LF's CI infrastructure
* Global-jjb is a common jenkins job builder base for LF projects
* Examples of my authored code can be provided as these softwares are open-source
* Featured work culminated jenkins driven automation:
  * committer promotion
  * artifact release
  * new project creation
  * doc builds<br>

[A recent change set that creates a project](https://gerrit.linuxfoundation.org/infra/c/releng/info-master/+/69945)<br>
[Read the docs shell script](https://github.com/lfit/releng-global-jjb/blob/master/shell/rtdv3.sh)<br>
[Read the docs example build](https://gerrit.onap.org/r/c/policy/parent/+/128484)<br>
[Release jobs initial commit](https://github.com/lfit/releng-global-jjb/commit/d473edacae5c8da2b4da50e6d41b2a1c52316813)<br>
[Example release job](https://gerrit.onap.org/r/c/policy/models/+/128499)<br>
[Example committer promotion](https://gerrit.onap.org/r/c/cps/ncmp-dmi-plugin/+/128368)<br>






{% highlight none %}
Usage: lftools gerrit [OPTIONS] COMMAND [ARGS]...

  GERRIT TOOLS.

Options:
  --help  Show this message and exit.

Commands:
  abandonchanges              Abandon all OPEN changes for a gerrit project.
  addfile                     Add a file for review to a Project.
  addgithubrights             Grant Github read for a project.
  addgitreview                Add git review to a project.
  addinfojob                  Add an INFO job for a new Project.
  addmavenconfig              Add maven config file for JCasC.
  create-saml-group           Create saml group based on ldap group.
  createproject               Create a project via the gerrit API.
  list-project-inherits-from  List who a project inherits from.
  list-project-permissions    List Owners of a Project.

{% endhighlight %}
[link to lftools gerrit docs](https://docs.releng.linuxfoundation.org/projects/lftools/en/latest/commands/gerrit.html)

<details>
<summary> gerrit.py </summary>

{% highlight python %}
#!/usr/bin/env python3
# SPDX-License-Identifier: EPL-1.0
##############################################################################
# Copyright (c) 2018 The Linux Foundation and others.
#
# All rights reserved. This program and the accompanying materials
# are made available under the terms of the Eclipse Public License v1.0
# which accompanies this distribution, and is available at
# http://www.eclipse.org/legal/epl-v10.html
##############################################################################
"""Create a gerrit project."""

from __future__ import print_function

import logging
from pprint import pformat

import click

from lftools.api.endpoints import gerrit
from lftools.git.gerrit import Gerrit as git_gerrit

log = logging.getLogger(__name__)


@click.group()
@click.pass_context
def gerrit_cli(ctx):
    """GERRIT TOOLS."""
    pass


@click.command(name="addfile")
@click.argument("gerrit_fqdn")
@click.argument("gerrit_project")
@click.argument("filename")
@click.option("--issue_id", type=str, required=False, help="For projects that enforce an issue id for changesets")
@click.option("--file_location", type=str, required=False, help="File path within the repository")
@click.pass_context
def addfile(ctx, gerrit_fqdn, gerrit_project, filename, issue_id, file_location):
    """Add a file for review to a Project.

    Requires gerrit directory.

    Example:

    gerrit_url gerrit.o-ran-sc.org/r
    gerrit_project test/test1
    """
    g = gerrit.Gerrit(fqdn=gerrit_fqdn)
    data = g.add_file(gerrit_fqdn, gerrit_project, filename, issue_id, file_location)
    log.info(pformat(data))


@click.command(name="addinfojob")
@click.argument("gerrit_fqdn")
@click.argument("gerrit_project")
@click.argument("jjbrepo")
@click.option("--issue_id", type=str, required=False, help="For projects that enforce an issue id for changesets")
@click.option("--agent", type=str, required=False, help="Specify the Jenkins agent label to run the job on")
@click.pass_context
def addinfojob(ctx, gerrit_fqdn, gerrit_project, jjbrepo, issue_id, agent):
    """Add an INFO job for a new Project.

    Adds info verify jenkins job for project.
    result['id'] can be used to ammend a review
    so that multiple projects can have info jobs added
    in a single review

    Example:

    gerrit_url gerrit.o-ran-sc.org/r
    gerrit_project test/test1
    jjbrepo ci-mangement
    """
    git = git_gerrit(fqdn=gerrit_fqdn, project=jjbrepo)
    git.add_info_job(gerrit_fqdn, gerrit_project, issue_id, agent)


@click.command(name="addgitreview")
@click.argument("gerrit_fqdn")
@click.argument("gerrit_project")
@click.option("--issue_id", type=str, required=False, help="For projects that enforce an issue id for changesets")
@click.pass_context
def addgitreview(ctx, gerrit_fqdn, gerrit_project, issue_id):
    """Add git review to a project.

    Example:
    gerrit_url gerrit.o-ran-sc.org
    gerrit_project test/test1
    """
    git = git_gerrit(fqdn=gerrit_fqdn, project=gerrit_project)
    git.add_git_review(gerrit_fqdn, gerrit_project, issue_id)


@click.command(name="addgithubrights")
@click.argument("gerrit_fqdn")
@click.argument("gerrit_project")
@click.pass_context
def addgithubrights(ctx, gerrit_fqdn, gerrit_project):
    """Grant Github read for a project.

    gerrit_url gerrit.o-ran-sc.org
    gerrit_project test/test1
    """
    g = gerrit.Gerrit(fqdn=gerrit_fqdn)
    data = g.add_github_rights(gerrit_fqdn, gerrit_project)
    log.info(pformat(data))


@click.command(name="abandonchanges")
@click.argument("gerrit_fqdn")
@click.argument("gerrit_project")
@click.pass_context
def abandonchanges(ctx, gerrit_fqdn, gerrit_project):
    """Abandon all OPEN changes for a gerrit project.

    gerrit_url gerrit.o-ran-sc.org
    gerrit_project test/test1
    """
    g = gerrit.Gerrit(fqdn=gerrit_fqdn)
    data = g.abandon_changes(gerrit_fqdn, gerrit_project)
    log.info(pformat(data))


# Creates a gerrit project if project does not exist and adds ldap group as owner.
# Limits: does not support inherited permissions from other than All-Projects.
@click.command(name="createproject")
@click.argument("gerrit_fqdn")
@click.argument("gerrit_project")
@click.argument("ldap_group")
@click.option("--description", type=str, required=True, help="Project Description")
@click.option("--check", is_flag=True, help="just check if the project exists")
@click.pass_context
def createproject(ctx, gerrit_fqdn, gerrit_project, ldap_group, description, check):
    """Create a project via the gerrit API.

    Creates a gerrit project.
    Sets ldap group as owner.

    Example:

    gerrit_url gerrit.o-ran-sc.org/r
    gerrit_project test/test1
    ldap_group oran-gerrit-test-test1-committers

    """
    g = gerrit.Gerrit(fqdn=gerrit_fqdn)
    data = g.create_project(gerrit_fqdn, gerrit_project, ldap_group, description, check)
    log.info(pformat(data))


@click.command(name="create-saml-group")
@click.argument("gerrit_fqdn")
@click.argument("ldap_group")
@click.pass_context
def create_saml_group(ctx, gerrit_fqdn, ldap_group):
    """Create saml group based on ldap group."""
    g = gerrit.Gerrit(fqdn=gerrit_fqdn)
    data = g.create_saml_group(gerrit_fqdn, ldap_group)
    log.info(pformat(data))


@click.command(name="list-project-permissions")
@click.argument("gerrit_fqdn")
@click.argument("project")
@click.pass_context
def list_project_permissions(ctx, gerrit_fqdn, project):
    """List Owners of a Project."""
    g = gerrit.Gerrit(fqdn=gerrit_fqdn)
    data = g.list_project_permissions(project)
    for ldap_group in data:
        log.info(pformat(ldap_group))


@click.command(name="list-project-inherits-from")
@click.argument("gerrit_fqdn")
@click.argument("gerrit_project")
@click.pass_context
def list_project_inherits_from(ctx, gerrit_fqdn, gerrit_project):
    """List who a project inherits from."""
    g = gerrit.Gerrit(fqdn=gerrit_fqdn)
    data = g.list_project_inherits_from(gerrit_project)
    log.info(data)


@click.command(name="addmavenconfig")
@click.argument("gerrit_fqdn")
@click.argument("gerrit_project")
@click.argument("jjbrepo")
@click.option("--issue_id", type=str, required=False, help="For projects that enforce an issue id for changesets")
@click.option("--nexus3", type=str, required=False, help="Specify a Nexus 3 server, e.g. nexus3.example.org")
@click.option(
    "--nexus3_ports",
    type=str,
    required=False,
    help="Comma-separated list of ports supported by the Nexus 3 server specified",
)
@click.pass_context
def addmavenconfig(ctx, gerrit_fqdn, gerrit_project, jjbrepo, issue_id, nexus3, nexus3_ports):
    """Add maven config file for JCasC.

    \b
    The following options can be set in the gerrit server's entry in lftools.ini:
      * default_servers: Comma-separated list of servers using the <projectname>
        credential. Default: releases,snapshots,staging,site
      * additional_credentials: JSON-formatted string containing
        servername:credentialname pairings. This should be on a single line,
        without quotes surrounding the string.
      * nexus3: The nexus3 server url for a given project.
      * nexus3_ports: Comma-separated list of ports used by Nexus3.
        Default: 10001,10002,10003,10004

    \f
    The 'b' escape character above disables auto-formatting, so that the help
    text will follow the exact formatting used here. The 'f' escape is to keep
    this from appearing in the --help text.
    https://click.palletsprojects.com/en/latest/documentation/
    """
    git = git_gerrit(fqdn=gerrit_fqdn, project=jjbrepo)
    git.add_maven_config(gerrit_fqdn, gerrit_project, issue_id, nexus3, nexus3_ports)


gerrit_cli.add_command(addinfojob)
gerrit_cli.add_command(addfile)
gerrit_cli.add_command(addgitreview)
gerrit_cli.add_command(addgithubrights)
gerrit_cli.add_command(createproject)
gerrit_cli.add_command(abandonchanges)
gerrit_cli.add_command(create_saml_group)
gerrit_cli.add_command(list_project_permissions)
gerrit_cli.add_command(list_project_inherits_from)
gerrit_cli.add_command(addmavenconfig)
{% endhighlight %}
</details>

[link to gerrit.py](https://github.com/lfit/releng-lftools/blob/master/lftools/cli/gerrit.py)

<details>
<summary>
api/gerrit.py
</summary>
{% highlight python %}

# SPDX-License-Identifier: EPL-1.0
##############################################################################
# Copyright (c) 2019 The Linux Foundation and others.
#
# All rights reserved. This program and the accompanying materials
# are made available under the terms of the Eclipse Public License v1.0
# which accompanies this distribution, and is available at
# http://www.eclipse.org/legal/epl-v10.html
##############################################################################

"""Gerrit REST API interface."""

import json
import logging
import os
import time
import urllib

import lftools.api.client as client
from lftools import config

log = logging.getLogger(__name__)


class Gerrit(client.RestApi):
    """API endpoint wrapper for Gerrit.

    Be sure to always include the trailing "/" when adding
    new methods.
    """

    def __init__(self, **params):
        """Initialize the class."""
        self.params = params
        self.fqdn = self.params["fqdn"]
        if "creds" not in self.params:
            creds = {
                "authtype": "basic",
                "username": config.get_setting(self.fqdn, "username"),
                "password": config.get_setting(self.fqdn, "password"),
                "endpoint": config.get_setting(self.fqdn, "endpoint"),
            }
            params["creds"] = creds

        super(Gerrit, self).__init__(**params)

    def add_file(self, fqdn, gerrit_project, filename, issue_id, file_location, **kwargs):
        """Add a file for review to a Project.

        File can be sourced from any location
        but only lands in the root of the repo.
        unless file_location is specified
        Example:

        gerrit_url gerrit.o-ran-sc.org
        gerrit_project test/test1
        filename /tmp/INFO.yaml
        file_location="somedir/example-INFO.yaml"
        """
        signed_off_by = config.get_setting(fqdn, "sob")
        basename = os.path.basename(filename)
        payload = self.create_change(basename, gerrit_project, issue_id, signed_off_by)

        if file_location:
            file_location = urllib.parse.quote(file_location, safe="", encoding=None, errors=None)
            basename = file_location
        log.info(payload)

        access_str = "changes/"
        result = self.post(access_str, data=payload)[1]
        log.info(result["id"])
        changeid = result["id"]

        my_file = open(filename)
        my_file_size = os.stat(filename)
        headers = {"Content-Type": "text/plain", "Content-length": "{}".format(my_file_size)}
        self.r.headers.update(headers)
        access_str = "changes/{}/edit/{}".format(changeid, basename)
        payload = my_file
        result = self.put(access_str, data=payload)
        log.info(result)

        access_str = "changes/{}/edit:publish".format(changeid)
        headers = {"Content-Type": "application/json; charset=UTF-8"}
        self.r.headers.update(headers)
        payload = json.dumps(
            {
                "notify": "NONE",
            }
        )
        result = self.post(access_str, data=payload)
        return result
        ##############################################################

    def add_info_job(self, fqdn, gerrit_project, jjbrepo, reviewid, issue_id, **kwargs):
        """Add an INFO job for a new Project.

        Adds info verify jenkins job for project.
        result['id'] can be used to ammend a review
        so that multiple projects can have info jobs added
        in a single review

        Example:

        fqdn gerrit.o-ran-sc.org
        gerrit_project test/test1
        jjbrepo ci-mangement
        """
        ###############################################################
        # Setup
        signed_off_by = config.get_setting(fqdn, "sob")
        gerrit_project_dashed = gerrit_project.replace("/", "-")
        filename = "{}.yaml".format(gerrit_project_dashed)

        if not reviewid:
            payload = self.create_change(filename, jjbrepo, issue_id, signed_off_by)
            log.info(payload)
            access_str = "changes/"
            result = self.post(access_str, data=payload)[1]
            log.info(result)
            log.info(result["id"])
            changeid = result["id"]
        else:
            changeid = reviewid

        if fqdn == "gerrit.o-ran-sc.org":
            buildnode = "centos7-builder-1c-1g"
        else:
            buildnode = "centos7-builder-2c-1g"

        my_inline_file = """---
- project:
    name: {0}-project-view
    project-name: {0}
    views:
      - project-view\n
- project:
    name: {0}-info
    project: {1}
    project-name: {0}
    build-node: {2}
    jobs:
      - gerrit-info-yaml-verify\n""".format(
            gerrit_project_dashed, gerrit_project, buildnode
        )
        my_inline_file_size = len(my_inline_file.encode("utf-8"))
        headers = {"Content-Type": "text/plain", "Content-length": "{}".format(my_inline_file_size)}
        self.r.headers.update(headers)
        access_str = "changes/{0}/edit/jjb%2F{1}%2F{1}.yaml".format(changeid, gerrit_project_dashed)
        payload = my_inline_file
        log.info(access_str)
        result = self.put(access_str, data=payload)
        log.info(result)

        access_str = "changes/{}/edit:publish".format(changeid)
        headers = {"Content-Type": "application/json; charset=UTF-8"}
        self.r.headers.update(headers)
        payload = json.dumps(
            {
                "notify": "NONE",
            }
        )
        result = self.post(access_str, data=payload)
        log.info(result)
        return result

    def vote_on_change(self, fqdn, gerrit_project, changeid, **kwargs):
        """Helper that votes on a change.

        POST /changes/{change-id}/revisions/{revision-id}/review
        """
        log.info(fqdn, gerrit_project, changeid)
        access_str = "changes/{}/revisions/2/review".format(changeid)
        headers = {"Content-Type": "application/json; charset=UTF-8"}
        self.r.headers.update(headers)
        payload = json.dumps(
            {
                "tag": "automation",
                "message": "Vote on file",
                "labels": {
                    "Verified": +1,
                    "Code-Review": +2,
                },
            }
        )

        result = self.post(access_str, data=payload)
        # Code for projects that don't allow self merge.
        if config.get_setting(self.fqdn + ".second"):
            second_username = config.get_setting(self.fqdn + ".second", "username")
            second_password = config.get_setting(self.fqdn + ".second", "password")
            self.r.auth = (second_username, second_password)
            result = self.post(access_str, data=payload)
            self.r.auth = (self.username, self.password)
        return result

    def submit_change(self, fqdn, gerrit_project, changeid, payload, **kwargs):
        """Method so submit a change."""
        # submit a change id
        access_str = "changes/{}/submit".format(changeid)
        log.info(access_str)
        headers = {"Content-Type": "application/json; charset=UTF-8"}
        self.r.headers.update(headers)
        result = self.post(access_str, data=payload)
        return result

    def abandon_changes(self, fqdn, gerrit_project, **kwargs):
        """."""
        gerrit_project_encoded = urllib.parse.quote(gerrit_project, safe="", encoding=None, errors=None)
        access_str = "changes/?q=project:{}".format(gerrit_project_encoded)
        log.info(access_str)
        headers = {"Content-Type": "application/json; charset=UTF-8"}
        self.r.headers.update(headers)
        result = self.get(access_str)[1]
        payload = {"message": "Abandoned by automation"}
        for id in result:
            if (id["status"]) == "NEW":
                id = id["id"]
                access_str = "changes/{}/abandon".format(id)
                log.info(access_str)
                result = self.post(access_str, data=payload)[1]
                return result

    def create_change(self, filename, gerrit_project, issue_id, signed_off_by, **kwargs):
        """Method to create a gerrit change."""
        if issue_id:
            subject = "Automation adds {0}\n\nIssue-ID: {1}\n\nSigned-off-by: {2}".format(
                filename, issue_id, signed_off_by
            )
        else:
            subject = "Automation adds {0}\n\nSigned-off-by: {1}".format(filename, signed_off_by)
        payload = json.dumps(
            {
                "project": "{}".format(gerrit_project),
                "subject": "{}".format(subject),
                "branch": "master",
            }
        )
        return payload

    def sanity_check(self, fqdn, gerrit_project, **kwargs):
        """Perform a sanity check."""
        # Sanity check
        gerrit_project_encoded = urllib.parse.quote(gerrit_project, safe="", encoding=None, errors=None)
        mylist = ["projects/", "projects/{}".format(gerrit_project_encoded)]
        for access_str in mylist:
            log.info(access_str)
            try:
                result = self.get(access_str)[1]
            except Exception:
                log.info("Not found {}".format(access_str))
                exit(1)
            log.info("found {} {}".format(access_str, mylist))
        return result

    def add_git_review(self, fqdn, gerrit_project, issue_id, **kwargs):
        """Add and Submit a .gitreview for a project.

        Example:

        fqdn gerrit.o-ran-sc.org
        gerrit_project test/test1
        issue_id: CIMAN-33
        """
        signed_off_by = config.get_setting(fqdn, "sob")
        self.sanity_check(fqdn, gerrit_project)

        ###############################################################
        # Create A change set.
        filename = ".gitreview"
        payload = self.create_change(filename, gerrit_project, issue_id, signed_off_by)
        log.info(payload)

        access_str = "changes/"
        result = self.post(access_str, data=payload)[1]
        log.info(result)
        changeid = result["id"]

        ###############################################################
        # Add a file to a change set.
        my_inline_file = """
        [gerrit]
        host={0}
        port=29418
        project={1}
        defaultbranch=master
        """.format(
            fqdn, gerrit_project
        )
        my_inline_file_size = len(my_inline_file.encode("utf-8"))
        headers = {"Content-Type": "text/plain", "Content-length": "{}".format(my_inline_file_size)}
        self.r.headers.update(headers)
        access_str = "changes/{}/edit/{}".format(changeid, filename)
        payload = my_inline_file
        result = self.put(access_str, data=payload)

        if result.status_code == 409:
            log.info(result)
            log.info("Conflict detected exiting")
            exit(0)

        else:
            access_str = "changes/{}/edit:publish".format(changeid)
            headers = {"Content-Type": "application/json; charset=UTF-8"}
            self.r.headers.update(headers)
            payload = json.dumps(
                {
                    "notify": "NONE",
                }
            )
            result = self.post(access_str, data=payload)
            log.info(result)

            result = self.vote_on_change(fqdn, gerrit_project, changeid)
            log.info(result)

            time.sleep(5)
            result = self.submit_change(fqdn, gerrit_project, changeid, payload)
            log.info(result)

    def create_saml_group(self, fqdn, ldap_group, **kwargs):
        """Create saml group from ldap group."""
        ###############################################################
        payload = json.dumps({"visible_to_all": "false"})
        saml_group = "saml/{}".format(ldap_group)
        saml_group_encoded = urllib.parse.quote(saml_group, safe="", encoding=None, errors=None)
        access_str = "groups/{}".format(saml_group_encoded)
        log.info("Encoded SAML group name: {}".format(saml_group_encoded))
        result = self.put(access_str, data=payload)
        return result

    def add_github_rights(self, fqdn, gerrit_project, **kwargs):
        """Grant github read to a project."""
        ###############################################################
        # Github Rights

        gerrit_project_encoded = urllib.parse.quote(gerrit_project, safe="", encoding=None, errors=None)
        # GET /groups/?m=test%2F HTTP/1.0
        access_str = "groups/?m=GitHub%20Replication"
        log.info(access_str)
        result = self.get(access_str)[1]
        time.sleep(5)
        githubid = result["GitHub Replication"]["id"]
        log.info(githubid)

        # POST /projects/MyProject/access HTTP/1.0
        if githubid:
            payload = json.dumps(
                {
                    "add": {
                        "refs/*": {
                            "permissions": {
                                "read": {"rules": {"{}".format(githubid): {"action": "{}".format("ALLOW")}}}
                            }
                        }
                    }
                }
            )
            access_str = "projects/{}/access".format(gerrit_project_encoded)
            result = self.post(access_str, data=payload)[1]
            pretty = json.dumps(result, indent=4, sort_keys=True)
            log.info(pretty)
        else:
            log.info("Error no githubid found")

    def create_project(self, fqdn, gerrit_project, ldap_group, description, check):
        """Create a project via the gerrit API.

        Creates a gerrit project.
        Converts ldap group to saml group and sets as owner.

        Example:

        gerrit_url gerrit.o-ran-sc.org/r
        gerrit_project test/test1
        ldap_group oran-gerrit-test-test1-committers
        --description="This is a demo project"

        """
        gerrit_project = urllib.parse.quote(gerrit_project, safe="", encoding=None, errors=None)

        access_str = "projects/{}".format(gerrit_project)

        result = self.get(access_str)[0]
        if result.status_code == 404:
            log.info(result)
            log.info("Project not found.")
            projectexists = False

        elif result.status_code == 401:
            log.info(result)
            log.info("Unauthorized.")
            exit(1)

        else:
            log.info("found {}".format(access_str))
            log.info(result)
            projectexists = True

        if projectexists:
            log.info("Project already exists")
            exit(1)
        if check:
            exit(0)

        saml_group = "saml/{}".format(ldap_group)
        log.info("SAML group name: {}".format(saml_group))

        access_str = "projects/{}".format(gerrit_project)
        payload = json.dumps(
            {
                "description": "{}".format(description),
                "submit_type": "INHERIT",
                "create_empty_commit": "True",
                "owners": ["{}".format(saml_group)],
            }
        )

        log.info(payload)
        result = self.put(access_str, data=payload)
        return result

    def list_project_permissions(self, project):
        """List a projects owners."""
        result = self.get("access/?project={}".format(project))[1][project]["local"]
        group_list = []
        for k, v in result.items():
            for kk, vv in result[k]["permissions"]["owner"]["rules"].items():
                group_list.append(kk.replace("ldap:cn=", "").replace(",ou=Groups,dc=freestandards,dc=org", ""))
        return group_list

    def list_project_inherits_from(self, gerrit_project):
        """List who a project inherits from."""
        gerrit_project = urllib.parse.quote(gerrit_project, safe="", encoding=None, errors=None)
        result = self.get("projects/{}/access".format(gerrit_project))[1]
        inherits = result["inherits_from"]["id"]
        return inherits

{% endhighlight %}
</details>

[link to api/gerrit.py](https://github.com/lfit/releng-lftools/blob/master/lftools/api/endpoints/gerrit.py)

The above api interface was written to replace my earlier work done in bash:<br>
[shell/gerrit_create](https://github.com/lfit/releng-lftools/blob/master/shell/gerrit_create)<br>
[shell/inactivecommitters](https://github.com/lfit/releng-lftools/blob/master/shell/inactivecommitters)


{% highlight none %}
Usage: lftools github [OPTIONS] COMMAND [ARGS]...

  GITHUB TOOLS.

Options:
  --help  Show this message and exit.

Commands:
  create-repo  Create a Github repo within an Organization.
  create-team  Create a Github team within an Organization.
  list         List options for github org repos.
  submit-pr    Submit a pr if mergeable.
  update-repo  Update a Github repo within an Organization.
  user         Add and Remove users from an org team.
  votes        Helper for votes.
{% endhighlight %}

[lftools github documentation](https://docs.releng.linuxfoundation.org/projects/lftools/en/latest/commands/github.html)<br>

[cli/github_cli.py](https://github.com/lfit/releng-lftools/blob/master/lftools/cli/github_cli.py)<br>
[github_helper.py](https://github.com/lfit/releng-lftools/blob/master/lftools/github_helper.py)<br>

Info File:<br>
[link to documentation](https://docs.releng.linuxfoundation.org/projects/lftools/en/latest/commands/infofile.html)<br>
[link to ldap_cli](https://github.com/lfit/releng-lftools/blob/master/lftools/cli/ldap_cli.py)<br>
[link to ldap](https://github.com/lfit/releng-lftools/blob/master/lftools/ldap_cli.py)<br>
[link to yaml4info](https://github.com/lfit/releng-lftools/blob/master/shell/yaml4info)<br>
[link to infofile](https://github.com/lfit/releng-lftools/blob/master/lftools/cli/infofile.py)<br>
[link to autocorrectinfofile](https://github.com/lfit/releng-lftools/blob/master/shell/autocorrectinfofile)<br>


LFID api (internal identity provider)<br>
[link to documentation](https://docs.releng.linuxfoundation.org/projects/lftools/en/latest/commands/lfidapi.html)<br>
[link to lfid_cli](https://github.com/lfit/releng-lftools/blob/master/lftools/cli/lfidapi.py)<br>
[link to lfidapi](https://github.com/lfit/releng-lftools/blob/master/lftools/lfidapi.py)<br>
[link to oauth2_helper](https://github.com/lfit/releng-lftools/blob/master/lftools/oauth2_helper.py)<br>

JcasC
-----

* Jenkins admin configuration via code reivew:
  * Code written for JcasC allows config files in repo to manage jenkins<br>

[Example JcasC change](https://gerrit.onap.org/r/c/ci-management/+/127823)

JcasC:<br>
[link to parser](https://github.com/lfit/releng-global-jjb/blob/master/jenkins-admin/create_jenkins_global_env_vars.py)<br>
[Jinja rendering](https://github.com/lfit/releng-global-jjb/blob/master/jenkins-admin/create_jenkins_clouds_openstack_yaml.py)<br>

<details>
<summary>
JcasC Updater (Bash)
</summary>
{% highlight python %}
#!/bin/bash
# SPDX-License-Identifier: EPL-1.0
##############################################################################
# Copyright (c) 2020 The Linux Foundation and others.
#
# All rights reserved. This program and the accompanying materials
# are made available under the terms of the Eclipse Public License v1.0
# which accompanies this distribution, and is available at
# http://www.eclipse.org/legal/epl-v10.html
##############################################################################
set -euo pipefail

casc_d_dir="/var/lib/jenkins/casc.d/community.d/"
ci_man="/opt/ci-man-repo"

main() {
  cd "$1" || exit
  check_for_updates #Are there updates to the ci-man repo
  mktmpdir
  lf_venv
  global_env_vars
  detect_clouds
  if [[ "${#clouds[@]}" -gt 1 ]]; then
    merge_clouds "${clouds[@]%/*}"
  fi
  cp "$tmpdir"/*.yaml "$casc_d_dir"/
  echo "$casc_d_dir"
  create_groovy
  reload_casc
  echo "Cleaning up"
  rm "$groovyfile"
  rm -rf "$tmpdir"
  rm -rf "$tmpdirnomadyaml"
  rm -rf "$lf_venv"
  echo "INFO: Jcasc updated"
}

check_for_updates(){
  OLD_GIT_COMMIT=$(git rev-parse HEAD)
  git pull --quiet --recurse-submodules
  NEW_GIT_COMMIT=$(git rev-parse HEAD)
  if [[ "$OLD_GIT_COMMIT" != "$NEW_GIT_COMMIT" ]]; then

  jenkins_config_files=$(git diff-tree \
  -m --no-commit-id \
  -r "$NEW_GIT_COMMIT" "$OLD_GIT_COMMIT" \
  --name-only -- "jenkins-config/")

    if (( $(grep -c . <<<"$jenkins_config_files") > 0 )); then
      echo "INFO: Modified config files found: $jenkins_config_files"
    else
      exit 0 #No updates
    fi
  else
    exit 0 #No updates
  fi
}


lf_venv(){
  source global-jjb/jenkins-init-scripts/lf-env.sh
  lf-activate-venv lftools jinja2 ruamel.yaml
}

reload_casc() {
  lftools jenkins -s <%= @casc_jenkins_url_stripped %> groovy "$groovyfile"
}

merge_clouds(){
  yq3 m -a append "$tmpdir"/"$1".yaml "$tmpdir"/"$2".yaml > "$tmpdir"/clouds.yaml
  rm -f "$tmpdir"/"$1".yaml "$tmpdir"/"$2".yaml
}

mktmpdir(){
  tmpdir=$(mktemp -d)
  tmpdirnomadyaml=$(mktemp -d)
}

create_groovy() {
  groovyfile="$(mktemp)"
cat <<EOF > "$groovyfile"
import io.jenkins.plugins.casc.ConfigurationAsCode;
ConfigurationAsCode.get().configure()
EOF
}

global_env_vars() {
  if ! [[ -d $casc_d_dir ]]; then
    echo "casc.d dir '$casc_d_dir' not found."
    exit 1
  fi
  python global-jjb/jenkins-admin/create_jenkins_global_env_vars.py \
    --path=jenkins-config/ <% if @casc_jenkins_url_stripped.include? "sandbox" %>--sandbox<% end %>
}

nomad() {
  echo "$2 detected with name $1"
  ls "$cloud_path/$2/$1/"
  cloudcfg="$cloud_path/$2/$1/cloud.yaml"
  cloud_cfg_check "$cloudcfg"
  files=()
  cd "$cloud_path/$2/$1/" || exit
  while read -d $'\n'; do
     if [[ $REPLY =~ main.yaml ]];then
       cloudfile=$REPLY
     elif [[ $REPLY =~ sandbox.yaml ]];then
       sandboxfile=$REPLY
     elif [[ $REPLY =~ defaults.yaml ]];then
       defaultsfile=$REPLY
     else
       files+=("$REPLY")
     fi
  done < <(find . -name "*.yaml" )


  cp "${files[@]}" "$tmpdirnomadyaml"
  <% if @casc_jenkins_url_stripped.include? "sandbox" %>cloudfile="$sandboxfile"<% end %>
  cp $cloudfile "$tmpdirnomadyaml"
  cp $defaultsfile "$tmpdirnomadyaml"

  cd "$tmpdirnomadyaml" || exit

  for file in ${files[@]}; do
      yq3 merge "$file" "$defaultsfile" > tmpfile
      cp tmpfile "$file"
  done

  yq3 merge --arrays append "${files[@]}" > umerged.yaml
  yq3 p -- umerged.yaml  "jenkins.clouds[+] nomad" > nmerged.yaml
  yq3 m --arrays update "$cloudfile" nmerged.yaml > "$tmpdir/nomad.yaml"
  yq3 w --inplace -d'*' "$tmpdir/nomad.yaml" 'jenkins.clouds[0].nomad.templates[*].password' '<%= @nomad_dockerhub_password %>'
  cd -
  echo "Nomad jcasc updated"
}

openstack() {
  echo "$2 detected with name $1"
  ls "$cloud_path/$2/$1/"
  cloudcfg="$cloud_path/$2/$1/cloud.cfg"
  cloud_cfg_check "$cloudcfg"
  python global-jjb/jenkins-admin/create_jenkins_clouds_openstack_yaml.py \
    --path=jenkins-config/ <% if @casc_jenkins_url_stripped.include? "sandbox" %>--sandbox<% end %> \
    --name "$1" > "$tmpdir/openstack.yaml"

}

cloud_cfg_check(){
  if ! [[ -f $cloudcfg ]]; then
    echo "No cloud config found"
    exit 1
  fi
  echo "$cloudcfg cloud config found"
}

detect_clouds(){
  cloud_path="jenkins-config/clouds"
  if [[ -d "$cloud_path" ]]; then
    clouds=()
    while read -d $'\n'; do
      clouds+=("$REPLY")
    done < <(find "$cloud_path" -type d  | awk -F"/clouds/" '{ print $2 } ' | grep "/")
  fi

  #run functions based on cloud name
  for cloud in "${clouds[@]}"; do
    "${cloud%/*}" "${cloud##*/}" "${cloud%/*}"
  done
}

main $ci_man
{% endhighlight %}
</details>

