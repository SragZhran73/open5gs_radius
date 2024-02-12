# OLB README

## Overview

In this README you will find how to deal with this *OLB/open5gs* project.

 2 special branches are yet available:

* *src* which is a fork of [*open5gs project*](https://github.com/open5gs/open5gs)
* *main* which is based on one version of open5gs project and gathers all internal features added to open5gs project

## Work with the *src* branch

### Synchronise fork

when needed, you can update the fork to align the *src* branch whith current open5gs project main branch.

To do so, you can use the following commands:

```console
  git clone git@gitlab.tech.orange:olb/open5gs.git
  cd open5gs
  git checkout src
  git fetch upstream
  git merge upstream/main
```

## Work with the *main* branch

Please keep in mind those rules:

* Never commit directly on Main.
* Code review is a best practice to adopt.
* Commit messages must be explicit. Generic messages must be avoided.
* Squash before merge, 1 commit message is prefered, but more are acceptable if clearer.

### Add a feature

A feature is added using the following feature branch workflow:

* Clone the project if you haven’t already:

```console
  git clone git@gitlab.tech.orange:olb/open5gs.git
  cd open5gs
```

* Create a branch for your feature:

```console
  git checkout -b feature_name
```

* Write code for the feature.
  Add the code to the staging area and add a commit message for your changes:

```console
  git commit -am "feat: brief description of the feature
  
  Detailed description of your feature."
```

* Push your branch to GitLab:

```console
  git push origin feature_name
```

* Review your code: On the left sidebar, go to Code > Commits.
* If needed amend your commit or create a new one.
* Create a merge request.
  The previous push command return a link to create this MR, you can use it or create it from the gitlab GUI.
* After validation of this MR, the feature will be merged to the main branch.


### Update of open5gs version 

In that case, we will also use a feature branch.
To initiate it you may have to synchronize the open5gs src branch as described above.

Then checkout the wanted version in this example the v2.7.0 version:

```console
  git checkout v2.7.0
```

and create a branch based on this version.

```console
  git checkout --orphan ogs-v2.7.0
  git commit -m"open5gs v2.7.0"
```

Finally apply all features (ie commits) available in the main branch:

```console
  git cherry-pick $(git rev-list --reverse main | head -2 | tail -1)..$(git rev-list -1 main)
```

When all conflicts are solved this branch will become the main branch (creation of release branch may be needed)

This way of working may be very complex and contibute to open5gs project, to propose our changes could simplify
the maintenance of our internal changes.
