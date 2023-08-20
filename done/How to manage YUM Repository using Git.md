#how-to, #yum , #git, #devOps, #repository, #linux 

### Introduction

A [[../todo/YUM]] repository is a collection of RPM packages that can be used to install, update, and remove software on a Linux system. **Managing a YUM repository using Git can provide a number of benefits, including version control, collaboration, and the ability to track changes over time**.

In this article, we will provide a step-by-step guide for setting up and managing a YUM repository using Git.

---
### How Creating Two Branches and Using a Git Worktree Can Help You Manage YUM Repositories

Below, I will explain why creating two branches and using a Git worktree are beneficial for managing YUM repositories:

* **Creating two branches** separates the development/staging area from the production area. This allows you to make changes and updates to the repository in the staging area without affecting the production environment until you're ready to deploy. **By doing so, you can reduce production deploy downtime**.

* **Creating a Git worktree** is another way to manage the production area separately from the staging area. It's important to note that this is just one method of managing the production environment, and **you could also use git clone to achieve a similar result**.

---
#### Initialization

To get started with managing a YUM repository using Git, you will need to create a new YUM repository and add packages to it. Once you have done this, you can follow these steps to set up Git for managing the repository:

1. Create a new YUM repository and add packages to it.
2. Initialize Git in the staging folder and create two branches: `develop` for the staging area and `release` for the production area.
3. Create a Git worktree for the production area using the ../release branch.
```bash
$ cd /path/to/staging # as develop branch / staging area
$ git init
$ git checkout -b develop
$ git branch release
$ git worktree add ../production release
```

---
##### Folder structure

After completing these steps, you will have a Git repository set up with two branches: `develop` for the staging area and `release` for the production area. You will also have a Git worktree set up in the `production` folder, which will allow you to manage the production area separately from the staging area.

Folder structure:
```bash
working folder/
├── staging/           # develop branch
│   ├── <packages>
│   ├── repodata/
│   └── .git/
└── production/     # release branch
    ├── <packages>
    ├── repodata/
    └── .git/
```

---
#### Development

Now that Git is set up, you can begin developing new packages in the staging area and using `createrepo` to update the repository metadata. Here are the steps to follow:

4. Develop new packages in the staging area by moving or copying them into the `staging` folder.
5. Use createrepo to update the repository metadata:
```bash
$ cd /path/to/staging
# Add new packages and update metadata
$ mv <new packages> /path/to/staging
$ createrepo .
```
6. Commit the changes and push them to the `develop` branch.
```bash
$ git add .
$ git commit -m "Add new packages"
$ git push origin develop
```
7. Once the staging area is verified, switch to the `release` branch in the staging area.
```bash
$ git checkout release
```
8. Merge the changes from the `develop` branch to the `release` branch in the staging area.
```bash
$ git merge develop
```
9. Create a Git tag for the new release and push it to the `release` branch in the staging area.
```bash
$ git tag -a v1.0 -m "Release version 1.0"
$ git push origin v1.0
```
10. Switch back to the `develop` branch in the staging area.
```bash
$ git checkout develop
```

---
#### Production
Now that the changes have been merged into the `release` branch in the staging area, you can update the production area with the new packages. Here are the steps to follow:
11. Go to the production area and pull the latest Git tag from the release branch.
12. check the production can be use

```bash
$ cd /path/to/production
$ git pull origin v1.0
```

Repeat steps 4 - 12 as needed.

### References
> [The CentOS documentation on YUM repositories](https://wiki.centos.org/HowTos/CreateLocalMirror)
> [The Git documentation on Git worktrees](https://git-scm.com/docs/git-worktree)