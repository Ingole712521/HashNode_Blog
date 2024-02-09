---
title: "Jenkins and  Case Study"
seoTitle: "Jenkins and  Case Study"
datePublished: Mon Feb 05 2024 15:04:15 GMT+0000 (Coordinated Universal Time)
cuid: cls92brzv000409jqbt7u0lvk
slug: jenkins-and-case-study
tags: web-development, devops, jenkins, case-study

---

![](https://miro.medium.com/v2/resize:fit:700/0*8uSSylTmlpxwiHi0 align="left")

**Jenkins** is an open-source Continuous Integration server written in Java for orchestrating a chain of actions to achieve the Continuous Integration process in an automated fashion. Jenkins supports the complete development life cycle of software from building, testing, documenting the software, deploying, and other stages of the software development life cycle.

Jenkins is a widely used application around the world that has around 300k installations and growing day by day. By using Jenkins, software companies can accelerate their software development process, as Jenkins can automate build and test at a rapid rate.

It is a server-based application and requires a web server like Apache Tomcat. The reason Jenkins software became so popular is that of its monitoring of repeated tasks which arise during the development of a project. For example, if your team is developing a project, Jenkins will continuously test your project builds and show you the errors in early stages of your development.

# **What is Continuous Integration?**

**Continuous Integration** is a process of integrating code changes from multiple developers in a single project many times. The software is tested immediately after a code commit. With each code commit, code is built and tested. If the test is passed, the build is tested for deployment. If the deployment is successful, the code is pushed to production.

This commit, build, test, and deploy is a continuous process and hence the name continuous integration/deployment.

![](https://miro.medium.com/v2/resize:fit:700/0*dHPHaEA_pdiNHHw8.png align="left")

# **How does Jenkins work?**

Jenkins is a server-based application and requires a web server like Apache Tomcat to run on various platforms like Windows, Linux, macOS, Unix, etc. To use Jenkins, you need to create pipelines which are a series of steps that a Jenkins server will take. Jenkins Continuous Integration Pipeline is a powerful instrument that consists of a set of tools designed to **host**, **monitor**, **compile** and **test** code, or code changes, like:

* **Continuous Integration Server** (Jenkins, Bamboo, CruiseControl, TeamCity, and others)
    
* **Source Control Tool** (e.g., CVS, SVN, GIT, Mercurial, Perforce, ClearCase and others)
    
* **Build tool** (Make, ANT, Maven, Ivy, Gradle, and others)
    
* **Automation testing framework** (Selenium, Appium, TestComplete, UFT, and others)
    

# **Architecture Of Jenkins**

Before we dive into how does Jenkins work, we must understand the architecture of Jenkins. These are the series of steps that outlines the interaction between different elements in Jenkins:

* Developers do the necessary modifications in the source code and commit the changes to the repository. A new version of that file will be created in the version control system that is used for maintaining the repository of source code.
    
* The repository is continuously checked by Jenkins CI server for any changes (either in the form of code or libraries) and **changes are pulled by the server**.
    
* In the next step, we ensure that the build with the ‘pulled changes’ is going through or not. The Build server **performs a build with the code and an executable** is generated if the build process is successful. In case of a build failure, an automated email with a link to build logs and other build artifacts is sent to the developer.
    
* In case of a successful build, the built application (or executable) is deployed to the test server. This step helps in realizing **continuous testing where the newly built executable goes through a series of automated tests**. Developers are alerted in case the changes have caused any breakage in functionality.
    
* If there are no build, integration, and testing issues with the checked-in code, the changes and tested application are automatically **deployed to the Prod/Production server**.
    

![](https://miro.medium.com/v2/resize:fit:700/0*gIXCne_T2OYMiRSe.png align="center")

# **Android Developers using Jenkins**

Android projects are fundamentally no different from how other types of software development projects might make use of a CI/CD system such as Jenkins:

* Android developers will collaborate using a source control management system (SCM) such as Git.
    
* They will create Pull Requests, which should be automatically verified.
    
* They expect to get feedback on test failures and code quality (e.g. via email or Slack); and they should be able to easily deploy new versions of their app to beta testers or end-users.
    

![](https://miro.medium.com/v2/resize:fit:700/0*w4MEFL6Lz4_N0c9B.png align="center")

# **Building Android Apps**

To build an Android app, you need the Java development tools (JDK), which Jenkins can automatically install for you, plus the Android SDK, which you can also install on individual build agents using a tool installer, or you can use a Docker container with the Android SDK Tools preinstalled, for example.

Then, you can use your SCM plugin of choice to fetch your source code, and build the app using the Android Gradle Plugin via the Gradle Wrapper — in most cases this is as simple as running ./gradlew assemble Debug.

Once your app has been built and packaged into a .apk file, you can use the archive artefacts build step, storing the APK, enabling colleagues to download APKs directly from Jenkins, so that they can try out the latest build.

# **Testing Android Apps**

The Android SDK supports two types of test: unit tests, which run on the JVM, and instrumentation tests, which have to run on an Android device or emulator. Both types of test can be executed using Jenkins and, since the Android Gradle Plugin writes the test results to disk in JUnit XML format, the JUnit Plugin for Jenkins can be used to parse the results, enabling you to see a test report, and to be notified of test failures.

Compiling and executing the unit tests for your app is as simple as adding another build step which runs ./gradlew test Debug Unit Test.

Thanks you !!