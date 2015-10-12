---
layout: post
title:  "Create a job"
date:   2015-10-07 12:28:00
categories: jenkins-create-job
topic: jenkins
---

## Cretea a Job

<hr>

Click on **Create jobs** to get started

<hr>

Enter the job name and select the Freestyle project

<hr>

Select **Git** under the Source code management options

<hr>

Build Triggers specify or trigger the build on a particular action or period of time.

Build after other projects are built
Build periodically
Build when a change is pushed to GitHub
Poll SCM

Jenkins can poll your Revision Control System for changes. You can specify how often Jenkins polls your revision control system using the same syntax as crontab on Unix/Linux.



<hr>

Add a Build-Step

Select **Execute shell** to do your build using a shell script

When a Jenkins job executes, it sets some environment variables that you may use in your shell script or batch command. The following table contains a list of all of these environment variables.

| ENVIRONMENT VARIABLES |                                                MEANING                                                                                                                                                                               |
|-----------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| BUILD_NUMBER          | The current build number, such as "153"                                                                                                                                                                                              |
|-----------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| BUILD_ID              | The current build id, such as "2005-08-22_23-59-59" (YYYY-MM-DD_hh-mm-ss)                                                                                                                                                            |
|-----------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| BUILD_URL             | The URL where the results of this build can be found (e.g. http://buildserver/jenkins/job/MyJobName/666/)                                                                                                                            |
|-----------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| NODE_NAME             | The name of the node the current build is running on. Equals 'master' for master node.                                                                                                                                               |
|-----------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| JOB_NAME              | Name of the project of this build. This is the name you gave your job when you first set it up. It's the third column of the Jenkins Dashboard main page.                                                                            |
|-----------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| BUILD_TAG             | String of jenkins-${JOB_NAME}-${BUILD_NUMBER}. Convenient to put into a resource file, a jar file, etc for easier identification.                                                                                                    |
|-----------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| JENKINS_URL           | Set to the URL of the Jenkins master that's running the build. This value is used by Jenkins CLI for example                                                                                                                         |
|-----------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| EXECUTOR_NUMBER       | The unique number that identifies the current executor (among executors of the same machine) that's carrying out this build. This is the number you see in the "build executor status", except that the number starts from 0, not 1. |
|-----------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| WORKSPACE             | The absolute path of the workspace.                                                                                                                                                                                                  |
|-----------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| GIT_COMMIT            | For Git-based projects, this variable contains the Git hash of the commit checked out for the build (like ce9a3c1404e8c91be604088670e93434c4253f03),(all the GIT_* variables require git plugin)                                     |
|-----------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| GIT_URL               | For Git-based projects, this variable contains the Git url (like git@github.com:user/repo.git or [https://github.com/user/repo.git)]                                                                                                 |
|-----------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|




<hr>

Add a Post-Build action to publish test reports in xml or send e-mails after the build is complete.

<hr>



