---
title: "How we Setup our iOS Project in Azure DevOps"
published: true
---

When we transitioned from building on Jenkins to Azure DevOps we unfortunately didn't have any expertise on the team or even at the company for how to setup a pipeline on Azure to build our iOS Apps. I am very passionate about having an app I'm working on in a buildable state on every pull request. Also I have spent time in previous roles using Jenkins, CircleCI, and BuddyBuild. So I was the logical choice in order to setup the pipeline in Azure.

First important question we had to answer was what is a pipeline? From what we've figured it's very similar to a Circle CI yaml configuration file which has a set of predefined steps you can choose to execute. This file lives in your project and controls how your build(s) are ran. You can have multiple configuration files if you have multiple projects in your repository and/or for different steps on different branches. Then you have to dig through configuration settings in Azure to point to the configuration file and tell it when and for what branches to build. For branches we choose pull request, develop, and main. Since we use Git Flow as our development process this seemed to target the most obvious build points.

We now had the file, but had to fill it up with the steps needed to build our project.

## Step 1: Developer Certs - InstallAppleCertificate

A really helpful feature of Azure DevOps is there is a secure file storage area. In this area I uploaded an Apple Development Certificate in the Personal Information Exchange (p12) format. Then in the configuration file the [InstallAppleCertificate](https://docs.microsoft.com/en-us/azure/devops/pipelines/tasks/utility/install-apple-certificate?view=azure-devops) step was added to install the cert to the keychain on the machine.

## Step 2: Provisioning Profile - InstallAppleProvisioningProfile

Similar to the Apple Development Certificate the provisioning profile for the app was stored in the secure file storage area and installed using [InstallAppleProvisioningProfile](https://docs.microsoft.com/en-us/azure/devops/pipelines/tasks/utility/install-apple-provisioning-profile?view=azure-devops) into the keychain on the machine.

## Step 3: Build - Xcode@5

Originally I wanted Azure DevOps to call through to [fastlane](https://fastlane.tools) and have fastlane take care of all the build steps but this proved to be too problematic so I went with the suggested [Xcode@5](https://docs.microsoft.com/en-us/azure/devops/pipelines/tasks/build/xcode?view=azure-devops) task. This was pretty straight forward to plunk in the various needed inputs. The biggest hassle was getting the provisioning profile and developer certs correctly referenced by this step.

## Step 4: Copy & Archive - CopyFile@2 & ArchiveFiles@2

In order to keep files around after you build has completed they have to be put in a very specific location. The [CopyFile@2](https://docs.microsoft.com/en-us/azure/devops/pipelines/tasks/utility/copy-files?view=azure-devops&tabs=yaml) command does that. Then the [ArchiveFiles@2](https://docs.microsoft.com/en-us/azure/devops/pipelines/tasks/utility/archive-files?view=azure-devops) command copies those file to a network location so they can be accessed after the build.

# Conclusion

The configuration file was successfully used when building on pull requests and in develop. A slightly different version was used in main which had additional steps. This greatly helped our team know the build status of the app and made it super easier to test as we stored the ipa for access after the build had completed. I ended up adding different configuration files for each of the frameworks we author. The steps were very similar to the above, but also incorporated running unit tests and publishing those results.

Overall, our transition to Azure has been smooth and we no longer need the Jenkins machine for any step in our build process. I'm hoping going forward we'll be able to better use the power of Azure DevOps to assist with release automation.
