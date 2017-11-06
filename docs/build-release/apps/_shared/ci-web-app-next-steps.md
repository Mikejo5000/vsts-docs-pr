You've just put your own CI process in place to automatically build and validate whatever code is checked in by your team.

### Alternative packaging

You produced a zip archive in the above CI process. This is convenient if you plan to deploy the app to an Azure web app or to an IIS server. Here are a few more options for how you may package your artifact.

* Deploy to Linux VMs: If your goal is to deploy the app to a Linux machine, then publish the build as a simple folder. To do this, simply remove the **Archive files** task from your build definition.

* Deploy to a container service: If your goal is to deploy the app to Azure web apps for containers or a Kubernetes cluster, then publish the app as a container. To learn more, see [Build and push a container for your app](../containers/build-container.md).

### Extend to other Git workflows

Now that you have a CI process for your master branch, you can extend the CI process to work with other branches in your repository, or to validate all pull requests. For more information, see one of these topics:

* [CI builds for Git in VSTS](../../actions/ci-build-git.md)

* [CI builds for GitHub](../../actions/ci-build-github.md)

### Deploy your app

You can also automatically deploy your app. To learn more, see one of these topics:

* [Deploy to Azure Web App](../cd/deploy-webdeploy-webapps.md)

* [Deploy to a Windows VM](../cd/deploy-webdeploy-iis-deploygroups.md)
