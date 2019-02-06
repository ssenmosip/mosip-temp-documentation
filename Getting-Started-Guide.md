# Content
1. [Getting the Source Code](#1-getting-the-source-code- )
2. [Setup and Configure Jenkins](#2-setup-and-configure-jenkins- )
3. [Setup and Configure Jfrog](#3-setup-and-configure-jfrog- )
4. [Setup and Configure SonarQube](#4-setup-and-configure-sonarqube- )
5. [Setup and Configure Docker Registry](#5-setup-and-configure-docker-registry- )
6. [Installing External Dependencies](#6-installing-external-dependencies- )
7. [Configuring MOSIP](#7-configuring-mosip- )
8. [MOSIP Deployment](#8-mosip-deployment- )

***
## 1. Getting the Source Code [**[↑]**](#content)
MOSIP source code can be obtained via creating a fork of MOSIP Github repository from the URL [https://github.com/mosip/mosip/](https://github.com/mosip/mosip/). To know more about how to fork code from Github follow this <a href="https://help.github.com/articles/fork-a-repo/" target="_blank">guide</a>.
Once Forked, start the process of setting up your CI/CD tools to build and run MOSIP.

***
## 2. Setup and Configure Jenkins [**[↑]**](#content)
In this step, we will setup jenkins and configure it. Configuration contains steps like creating credentials, creating pipelines using xml files present in MOSIP source code, connecting Jenkins to recently forked repository and creating webhooks. Lets look at these steps one by one - 

### A. Installing Jenkins
Jenkins installation is pretty standard one(see [How to install Jenkins](https://jenkins.io/doc/book/installing/)), but to use MOSIP supported build pipelines you have to install Jenkins in an Redhat 7.5 environment. Also you have to install following list of plugins - 
* [Github Plugin](https://wiki.jenkins.io/display/JENKINS/GitHub+Plugin)
* Others

### B. Create Pipelines
### C. Setting Up Github with Jenkins

***
## 3. Setup and Configure Jfrog [**[↑]**](#content)

***
## 4. Setup and Configure SonarQube [**[↑]**](#content)

***
## 5. Setup and Configure Docker Registry [**[↑]**](#content)

***
## 6. Installing External Dependencies [**[↑]**](#content)

***
## 7. Configuring MOSIP [**[↑]**](#content)

***
## 8. MOSIP Deployment [**[↑]**](#content)

***