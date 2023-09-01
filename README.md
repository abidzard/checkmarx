# Checkmarx

![CxLogo](img/CxLogo.png?raw=true)

Checkmarx is a comprehensive application security platform designed to identify, manage, and mitigate security risks within software applications. It offers a range of tools and solutions to help organizations enhance the security of their software development lifecycle.

## CheckmarxSAST

Checkmarx Static Application Security Testing (Checkmarx SAST) is a specific component of the Checkmarx platform. It focuses on performing static analysis of the source code and binaries of applications. By analyzing the codebase, Checkmarx SAST detects vulnerabilities, security weaknesses, and potential exploits that might exist within the application's source code. This process is performed without actually executing the application.

## CheckmarxSCA

Checkmarx Software Composition Analysis (Checkmarx SCA) is another component of the Checkmarx platform. It is designed to analyze third-party and open-source components used within an application. Checkmarx SCA scans these components for known vulnerabilities, license compliance issues, and any potential risks that might arise from using these components. This helps organizations ensure that their applications do not inherit security vulnerabilities from the components they utilize.

## GitLab Integration

GitLab is a web-based DevOps life cycle tool that provides a Git-repository manager providing wiki, issue-tracking and continuous integration/continuous deployment pipeline features. GitLab offers the ability to automate the entire DevOps life cycle from planning to creation, build, verify, security testing, deploying, and monitoring offering high availability and replication, and scalability and available for using on-prem or cloud storage. In this documentation we focused on GitLab on Premise.

## CxFlow Overview

CxFlow is a Spring Boot application written by Checkmarx that enables initiations of scans and result orchestration. It is the main automation driving the GitLab and Checkmarx integration. Some features of CxFlow include:

- Automated project creation
- Facilitates feedback channels in a closed loop nature.
    - Channels include GitLab Issues, GitLab Merge Requests, JIRA, Rally, and ServiceNow.
 - Enables customers to incorporate Checkmarx into their DevOps/Release pipelines as early as possible.
- Controls the “breaking” of builds.

CxFlow is an open-source project written and maintained by Checkmarx. For access to CxFlow’s Wiki, please refer to [CxFlow Wiki](https://github.com/checkmarx-ltd/cx-flow/wiki)

> This repository reference to Checkmarx [Documentation](https://checkmarx.com/resource/documents/en/34965-8218-gitlab-integration.html).

## Pre-requisites
- __GitLab on Premise__

    To install GitLab on Premise please refer to [GitLab Installation](https://about.gitlab.com/install/)

- __GitLab Runner__

    ![GitLabRunner](img/gitlab-runner.png?raw=true)

    Runners are processes that pick up and execute CI/CD jobs for GitLab. [What is GitLab Runner?](https://docs.gitlab.com/runner/)

    To install GitLab Runner please refer to [GitLab Runner Installation](https://docs.gitlab.com/runner/install/)

- __Java__

    Java and the JVM (Java’s virtual machine) are required for many kinds of software, including Tomcat, Jetty, Glassfish, Cassandra, and Jenkins. Java comes with two main components. The JDK provides essential software tools to develop in Java, such as a compiler and debugger. JRE is used to execute Java programs.

    - To install the OpenJDK version of Java, first update your `apt` package index

        ```
        sudo apt update
        sudo apt install default-jdk
        ```
    - Verify the installation this command
    
            java --version
            
        ![JavaVersion](img/java-v.png?raw=true)

## Requirements
- GitLab can access a running Checkmarx CxSAST Server with an up-to-date Checkmarx license.
- If performing CxSCA scans, you must have a valid CxSCA license and GitLab must be able to access the CxSCA tenant.
- To review scan results within GitLab’s Security Dashboard, you need the Gold/Ultimate tier or the GitLab project must be public.
    - To review results in the issue management of your choice (i.e., JIRA) extra configuration is needed, please refer to [CxFlow Bug Trackers](https://github.com/checkmarx-ltd/cx-flow/wiki/Bug-Trackers-and-Feedback-Channels)
- `/app/cx-flow.jar` directory and `cx-flow.jar` are required to start a scan using cx-flow, more detail about Cx-Flow [click here](https://github.com/checkmarx-ltd/cx-flow).
    
    - Create directory called app on GitLab Server use this command:
        
            sudo mkdir /app

    - Go to directory `/app`
            
            cd /app

    - Download the latest version of Cx-Flow from [here](https://github.com/checkmarx-ltd/cx-flow/releases) or use this command:
        
            sudo wget https://github.com/checkmarx-ltd/cx-flow/releases/download/1.6.41/cx-flow-1.6.41.jar

        ![CxFlowDownload](img/wget-cx-flow.png?raw=true)

    - Rename the file to `cx-flow.jar` use this command:
        
            sudo mv cx-flow-1.6.41.jar cx-flow.jar

## CI/CD Variables
To allow for easy configuration, it is necessary to create environment variables with GitLab to run the integration. For more information on GitLab CI/CD variables, visit here: GitLab: [CI/CD - Environment Variables](https://checkmarx.com/resource/documents/en/34965-8218-gitlab-integration.html).

Edit the CI/CD variables under `Settings` → `CI/CD` → `Variables` and add the following variables for a CxSAST and/or CxSCA scan: