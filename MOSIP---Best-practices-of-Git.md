# MOSIP - Best practices of Git 

## 1. Introduction
  ### 1.1 Context

MOSIP is developed as an open source framework project. Git is used as the source code repository. There should a standard set of steps which should be followed to maintain the consistency of the code commits.

 ### 1.2 Purpose of this document

This document gives the steps that a MOSIP developer should do during the development of the project.

  ### 1.3 Scope of this document

This document covers the steps that the Developers and the Tech leads should do during the development activities.

## 2. Git entries

Following are the teams who will be using the Git,

1. Java team
2. Testing team
3. Database team
4. UI team

## 3. Git activities

Do all the Git activities using the following tools,

Eclipse

- Do the Git activities via eclipse only.

Gitbash

- Team members are using IDE other than Eclipse can use Git bash.
- UI team and Database team can use the Gitbash to push their details to Git.
- The advance commands are needed only for the Tech Leads on few occasions.

## 4. Initial setup

Developer and Tech Leads:

1. Clone the Git repository, [**Git**](/mosip/mosip.git)

2. Give your username and password.

## 5. Basic flow

Following are the typical steps which will be done by the people.

Developer:

1. Developer checkout the branch from DEV and creates the feature branch.
  1. git checkout
2. The naming convention for the feature branch is as follows,
  1. DEV\_\&lt;_sprint number_\&gt;\_\&lt;_developer name_\&gt;\_\&lt;JIRA id\&gt;
  2. For example, _DEV\_SPRINT3\_URVIL\_MOS-424_
3. Developer develops the code in the newly created branch.
4. Daily morning, the developer have to **pull** from the Git or whenever possibile.
5. Whenever needed, the developer can **push** their feature branch to Git.
6. Developer can do multiple **commit** s in between.

Tech Lead:

1. Once the developer is done with the development, requests for review from the reviewer. Mostly, this will be the Tech Lead.
2. The Tech Lead pulls the code from Git, reviews the code and gives the review comment.
3. Once the developer done with the review comment implementation, **commit** s and **push** es the code to the feature branch.
4. Once the review is over, Tech Lead **merge** s the code to the DEV branch.
5. Then the Tech Lead sends a mail to the other Tech Leads about the commit.
6. Once the **merge** happens to the DEV branch, the Jenkins Pipeline will start building all the modules and will restart the applications. NOTE: Every application have to have a place to display the build time.

## 6. Types of branches
### 6.1 DEV branch

This is the branch used for the development purpose.

### 6.2 Feature branches

This is the branch created by each developer for a specific feature. The branch name should comply the naming standard. There can be &#39;n&#39; number of branches.

## 6.3 Release branches

This branch will handle the releases.

## 6.4 Master branch

This is a stable branch. Only the tested code should be pushed to this branch.

## 7. Feature branches
  ### 7.1 Naming standard

While naming the feature branches, make sure to follow the standard.

The naming convention for the feature branch is as follows, 
  1. DEV\_&lt;_sprint number_&gt;_&lt;_developer name_&gt;_&lt;JIRA id&gt;
  2. For example, _DEV\_SPRINT3\_URVIL\_MOS-424_

### 7.2 House keeping

Please delete the feature branches when it is not absolutely necessary. As a thumb rule, you can delete the feature branch after n+1 sprints. For example, you can delete the feature branch of sprint 3 in sprint 5.

## 8. Checklists

### 8.1 DEV branch

There is a DEV branch already available on the Git. Lead should follow the below steps to do the initial commit,

1. Make sure the project structure complies to the MOSIP standards.
2. Make sure the code had the appropriate unit testing coverage.
3. The Java code should comply to the MOSIP standards.
4. The Java code should comply to the MOSIP quality standards.
5. The intended Maven targets should succeed.

Once the above criteria are met, the code should be pushed to DEV branch by the Tech lead.

## 9. Roles and Permissions

Following are the roles and permissions given in Git,

1. Developer
  1. DEV branch
    1. Can _checkout_ a new feature branch from DEV branch.
    2. Can _push_ his newly created feature branches to the Git.
  2. Feature branches
    1. Cannot _push_ any code to DEV branch.
2. Tech Lead
  1. DEV branch
    1. Can _checkout_ a new feature branch from DEV branch.
    2. Can _push_ his newly created feature branches to the Git.


## 10. Contact

Shravan Poorigali `shravan.poorigali@mindtree.com`

Karthik Ramanan `Karthik.Ramanan@mindtree.com`

Rudra Prasad Tripathy `Rudra.Tripathy@mindtree.com`

John David `John.Panneerselvam@mindtree.com`