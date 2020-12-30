---
title: "Improving our Release Process"
published: true
---

When I started on the IMS SDK team we had multiple automated and manual steps in order to create a release. In this article I will discuss how things worked before and various improvements we made.

# The Old Way

 We had numerous Jenkins jobs to build our frameworks. These were automatically kicked off when new code got into develop. Each job would build the framework, run the unit tests, create the framework file and documentation. As a last step the framework and documentation were sent to a network location.

 When we were ready to do a release we would manually trigger another Jenkins job to download all the frameworks and documentation. The job would then create a Git commit on our private snapshot repository.

 When we ready to do a release we would manually copy the files from the snapshot repo to the public repository and create a new git release.

 As you can read by the description above this process is a mix of automated and manual steps. We wanted to move to a more automated process and our company was moving to Azure DevOps, so we decided it was a good time to further automate the release process.

 # The New Way

 After our code moved to Azure, we created a pipeline for each framework. This was basically doing the same steps as Jenkins. But now we had some new problems. Azure is in the cloud and the Jenkins box was local, so copying the files to the network location was trivial with Jenkins, but not realistically possible with Azure. We ended up creating a kitchen sink pipeline that did all the building in one step and would create a zip file of all the frameworks and documentation.

 The rest of the steps were still the same as before, but unfortunately more manual. You'd have to download the files from Azure and then create a Git commit yourself for the snapshot repo.

 For Android they had a very similar release process and had migrated to using Azure releases. There process was 100% automated, so the next for iOS is to Azure releases just like Android. But, other priorities came up and this work did not get done.

 # Conclusion

 Azure has been more stable then Jenkins in terms of building and performance. It's also been fantastic to choose a specific version of Xcode and build only against it. I'm hoping the rest of the release steps can get automated and that the team will be able have click button releases.
