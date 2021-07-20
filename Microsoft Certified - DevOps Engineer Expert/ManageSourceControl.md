## Develop a modern source control strategy

### Integrate/migrate disparate source control systems (e.g., GitHub, Azure Repos)

### Design authentication strategies

### Design approach for managing large binary files (e.g., Git LFS)

#### Git Large File Storage

Git Large File Storage (LFS) replaces large files such as audio samples, videos, datasets, and graphics with text pointers inside Git, while storing the file contents on a remote server like GitHub.com or GitHub Enterprise.

### Design approach for cross repository sharing (e.g., Git sub-modules, packages)

#### Submodules

It often happens that while working on one project, you need to use another project from within it. Perhaps it’s a library that a third party developed or that you’re developing separately and using in multiple parent projects.

Submodules allow you to keep a Git repository as a subdirectory of another Git repository.

```git
$ git submodule add https://github.com/chaconinc/DbConnector
Cloning into 'DbConnector'...
remote: Counting objects: 11, done.
remote: Compressing objects: 100% (10/10), done.
remote: Total 11 (delta 0), reused 11 (delta 0)
Unpacking objects: 100% (11/11), done.
Checking connectivity... done.

$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

  new file:   .gitmodules
  new file:   DbConnector
```

First you should notice the new .gitmodules file. This is a configuration file that stores the mapping between the project’s URL and the local subdirectory you’ve pulled it into:

```ini
[submodule "DbConnector"]
  path = DbConnector
  url = https://github.com/chaconinc/DbConnector
```

### Implement workflow hooks

You can configure your workflows to run:

- When specific activity on GitHub happens
- At a scheduled time
- When an event outside of GitHub occurs

```yaml
# Triggered when code is pushed to any branch in a repository
on: push
# Triggers the workflow on push or pull request events
on: [push, pull_request]
```

The following steps occur to trigger a workflow run:

1. An event occurs on your repository, and the resulting event has an **associated commit SHA and Git ref.**
2. The ```.github/workflows``` directory in your repository is searched for workflow files at the associated commit SHA or Git ref
3. The workflow files for that commit SHA and Git ref are inspected, and a new workflow run is triggered for any workflows that have ```on:``` values that match the triggering event.

### Design approach for efficient code reviews (e.g., GitHub code review assignments, schedule reminders, Pull Analytics)

#### GitHub Code Review Assignements

Code review assignments clearly indicate **which members of a team are expected to submit a review for a pull request**.

Code review assignments automatically choose and assign reviewers based on one of two possible algorithms:

- The round robin algorithm chooses reviewers based on who's received the least recent review request, focusing on alternating between all members of the team regardless of the number of outstanding reviews they currently have.
- The load balance algorithm chooses reviewers based on each member's total number of recent review requests and considers the number of outstanding reviews for each member.

#### Scheduled reminders

Scheduled reminders help teams focus on the most important review requests that require their attention.
Scheduled reminders for pull requests will send a message to your team in Slack with **all open pull requests** that you or your team have been asked to review, at a specified time.

## Plan and implement branching strategies for the source code

### Define Pull Requests (PR) guidelines to enforce work item correlation

Here are some common guidelines for pull request:

- **Make A Branch**:
  - Create a separate branch for each issue that you're working on. Do not make changes to the default branch (e.g. master, develop) of your fork.
- **Push Your Code ASAP**:
  - Push your code as soon as you can. Follow the "early and often*" rule.
- **Request Review**:
- **Describe Your Pull Request**:
  - Tasks should be divided into subtasks that can be handled in **uninterrupted stretches of work**. *(30-60 minutes on average, and no more than 4 hours)*
- **Incorporating feedback**:

#### Commit Early, Push Often

Whatever your methodology, whatever the granularity of tasks in your project management tools:

- **Keep your commits small**
  - **Avoid ever leaving uncommitted work**
  - Each commit should try to represent one single step forward of work
  - Smaller commits result in a more interesting and readable commit log
  - Big commit == big risk
  - Big commits are harder for others to review.

- **Perform Frequent Pushes**
  - Never have only a single copy of your work.
  - Provide transparency about your ongoing work to your team.

### Implement branch merging restrictions (e.g., branch policies, branch protections, manual, etc.)

### Define branch strategy (e.g., trunk based, feature branch, release branch, GitHub flow)

#### Feature Branching Strategy *(Task Branching)*

- **Description**: Using a feature branching strategy allows developers to create a branch for a **specific feature** or **task**.
These are often referred to as user stories. This **branch-per-issue workflow allows** developers to work separately.
- **Pros**:
  - Allowing developers to experiment and work independently from the core product can keep your codebase stable.
  - Gives your team’s the freedom to innovate, plus you can implement workflows for CI/CD.
  - Helps developers easily segment their work.
  - Each team or sub-team could maintain their own branch for development.
  By integrating all changes earlier in the development cycle, you can prevent costly conflicts that could take a long time to sort out.
- **Cons**:
  - Long-lived feature branches are a nightmare to merge.
  - Featuring branching only works if developers (and teams) branch and merge often.
  - It is recommended to merge **at least once a day**

> *Note that when using the feature branching strategy for a large enterprise/codebase, it is important to integrate changes across teams frequently.*

#### Release Branching Strategy

- **Description**: A release branching strategy involves creating a branch for a potential release that includes all applicable stories. When a team starts working on a new release, the branch is created.
- **Pros**:
  - Product that needs to support multiple versions in parallel or needs to handle customization for a specific customer, **release branching is a requirement**.
- **Cons**:
  - Working with a lot of release branches can be difficult to maintain.
  - With a lot of a of changes and contributors, the codebase can quickly become unstable.
  - It also can potentially create more work for teams. If they need to maintain multiple releases, changes would need to be applied into several versions.

### Design and implement a PR workflow (code reviews, approvals)

### Enforce static code analysis for code-quality consistency on PR

## Configure repositories

### Configure permissions in the source control repository

### Organize the repository with git-tags

Git has the ability to tag specific points in a repository’s history as being important. Typically, people use this functionality to mark release points (v1.0, v2.0 and so on).

```git
# Listing your tags
$ git tag
v1.0
v2.0

# Listing your tags that match a particular pattern.
$ git tag -l "v1.8.5*"
v1.8.5
v1.8.5-rc0
v1.8.5-rc1
v1.8.5-rc2
v1.8.5-rc3
```

Git supports two types of tags:

- **lightweight**: very much like a branch that doesn’t change - it’s just a pointer to a specific commit.
- **annotated**: are stored as full objects in the Git database. They’re checksummed; contain the tagger name, email, and date; have a tagging message; and can be signed and verified with GNU Privacy Guard (GPG).

```git
# Creating an annoted tag
$ git tag -a v1.4 -m "my version 1.4"

$ git show v1.4
tag v1.4
Tagger: Ben Straub <ben@straub.cc>
Date:   Sat May 3 20:19:12 2014 -0700

my version 1.4

commit ca82a6dff817ec66f44342007202690a93763949
Author: Scott Chacon <schacon@gee-mail.com>
Date:   Mon Mar 17 21:52:11 2008 -0700

# Creating a lightweight tag
$ git tag v1.4-lw
$ git show v1.4-lw
commit ca82a6dff817ec66f44342007202690a93763949
Author: Scott Chacon <schacon@gee-mail.com>
Date:   Mon Mar 17 21:52:11 2008 -0700
```

Here is how to delete a tag

```git
$ git tag -d v1.4-lw
# Note that this does not remove the tag from any remote servers.
# There are two common variations for deleting a tag from a remote server.
# 1. git push <remote> :refs/tags/<tagname>:
$ git push origin :refs/tags/v1.4-lw
To /git@github.com:schacon/simplegit.git
 - [deleted]         v1.4-lw

# 2. The second (and more intuitive) way to delete a remote tag is with git push origin --delete <tagname>
$ git push origin --delete <tagname>
```

### Plan for handling oversized repositories

There are broadly two major reasons for repositories growing massive:

- They accumulate a very very long history
- They include huge binary assets that need to be tracked and paired together with code

#### Cloning repositories with a very long history

Either you will have to perform ```git shallow clone```
**Git shallow clone** lets you pull down **just the latest commits**, not the entire repo history.

```git
$git clone -–depth [depth] [remote-url]
```

You can also use git shallow clone to access a single branch

```git
$git clone [remote-url] --branch [name] --single-branch [folder]
```

You can also use ```git filter branch``` which lets you walk through the entire history of the project filtering out, modifying, and skipping files according to predefined patterns.

```git
$git filter-branch --tree-filter 'rm -rf [/path/to/spurious/asset/folder]'
```

Note that git filter-branch has a minor drawback, though: once you use _filter-branch_, you effectively rewrite the entire history of your project. That is, all commit ids change. This requires every developer to re-clone the updated repository.

#### Managing repositories with huge binary assets

By default, Git will compress and store all subsequent full versions of the binary assets, which is obviously not optimal if you have many.

It is important to reflect on the nature of your project’s binary assets, as that will help you determine the winning approach.

Here are some points to consider:

- Use ‘delta off’ for binary files that change significantly to avoid the unnecessary delta compression work as part of the repack.
- If you have multiple binary files, turn compression off with ‘core.compression 0’ or ‘core.loosecompression 0’.
- Explore the tuning of ‘core.bigFileThreshold’ in order to disable delta compression for files that are bigger than X MiB

> *Please note that some repositories have to be kept in tact for legal or regulatory reasons.*

### Plan for content recovery in all repository states

### Purge data from source control

## Integrate source control with tools

### Integrate GitHub with DevOps pipelines

#### Task 1: Forking a GitHub repo and installing Azure Pipelines

The **GitHub Marketplace** provides a variety of tools from Microsoft and 3rd parties that help you extend your project workflows. Click **Marketplace** from the top navigation to visit it.
The **Azure Pipelines offering is free** for anyone to use **for public repositories**, and free for a single build queue if you’re using a private repository.

#### Task 2: Configuring your Azure Pipelines project

Select (or create) the **Azure DevOps organization** you would like to perform these builds under, as well as the Azure DevOps **project** from that organization you would like to use

Azure Pipelines will analyze your project in an attempt to determine if any existing templates would be a good fit.

The build pipeline is defined as **YAML**, a markup syntax well-suited to defining processes like this because it allows you to manage the configuration of the pipeline like any other file in the repo.

### Integrate GitHub with identity management solutions (Azure AD)

### Design for GitOps

GitOps is a way of implementing Continuous Deployment for **cloud native applications**.
It focuses on a developer-centric experience when operating infrastructure, by using tools developers are already familiar with, including Git and Continuous Deployment tools.

The core idea of GitOps is having a Git repository that always contains **declarative descriptions** of the infrastructure currently desired in the production environment and an automated process to make the production environment match the described state in the repository.

If you want to deploy a new application or update an existing one, **you only need to update the repository** - the automated process handles everything else.

![GitOps Architecture Azure](../Images/GitOpsArchitectureAzure.png)

#### Why should I use GitOps?

- **Deploy Faster More Often**:
  - You don’t have to switch tools for deploying your application.
  - Everything happens in the version control system you use for developing the application anyways.
- **Easy and Fast Error Recovery**:
  - You have a complete history of how your environment changed over time.
  - Recovery is as easy as issuing a ```git revert``` and watching your environment being restored.
- **Easier Credential Management**: Your environment only needs access to your repository and image registry
- **Self-documenting Deployments**: Every change to any environment must happen through the repository. You can always check out the master branch and get a complete description of what is deployed where plus the complete history of every change ever made to the system.
- **Shared Knowledge in Teams**:
  - Using Git to store complete descriptions of your deployed infrastructure allows everybody in your team to check out its evolution over time.
  - With great commit messages everybody can reproduce the thought process of changing infrastructure and also easily find examples of how to set up new systems.

#### How does GitOps work?

GitOps organizes the deployment process around code repositories as the central element. There are at least two repositories:

- **The application repository**: contains the source code of the application and the deployment manifests to deploy the application
- **The environment configuration repository**: contains all deployment manifests of the currently desired infrastructure of an deployment environment.

##### Push-based vs. Pull-based Deployments

When possible, the Pull-based approach should be preferred as it is considered the more secure and thus better practice to implement GitOps.

###### Push-based Deployments

The Push-based deployment strategy is implemented by popular CI/CD tools such as Jenkins, CircleCI, or Travis CI.
The source code of the application lives inside the application repository along with the Kubernetes YAMLs needed to deploy the app.

Whenever the application code **is updated**, the build pipeline is triggered, which builds the container images and finally **the environment configuration repository is updated with new deployment descriptors**.

![GitOps Push Deployments](../Images/GitOpsPushDeployments.png)

##### Pull-based Deployments

With the pull-based deployment approach, the operator is introduced. It takes over the role of the pipeline by continuously comparing the desired state in the environment repository with the actual state in the deployed infrastructure. Whenever differences are noticed, the operator updates the infrastructure to match the environment repository.

![GitOps Pull Deployments](../Images/GitOpsPullDeployments.png)

### Design for ChatOps

ChatOps, a term widely credited to GitHub, is all about conversation-driven development.

While in a chat room, team members type commands that the chatbot is configured to execute through custom scripts and plugins.

These can range from code deployments, to security event responses, to team member notifications.

ChatOps integrates development tools, operations tools, and processes into a collaboration platform so that teams can efficiently communicate and manage the flow of their work.

### Integrate source control artifacts for human consumption (e.g., Git changelog)

### Integrate GitHub Codespaces
