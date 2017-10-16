You've just put your own CI process in place to automatically build and validate whatever code is checked in by your team.

### Alternative packaging

You produced a zip archive in your CI process. This is convenient if you plan to deploy the app to an Azure web app or to an IIS server. However, if your goal is to deploy the app to a Linux machine, then you can publish the build as a simple folder. To do this, simply remove the **Archive files** task from your build definition or YAML file.

If your goal is to deploy the app to Azure web apps for containers or a Kubernetes cluster, then you can publish the app as a container. To learn more, see this topic:

* [Build a container](../containers/build-container.md)

### Extend to other Git workflows

Now that you have a CI process for your master branch, you can extend the CI process to work with other branches in your repository, or to validate all pull requests. For more information, see one of these topics:

* [CI builds for Git in VSTS](../../actions/ci-build-git.md)

* [CI builds for GitHub](../../actions/ci-build-github.md)

### Deploy your app

You can also automatically deploy your app. To learn more, see one of these topics:

* [Deploy to Azure Web App](../cd/deploy-webdeploy-webapps.md)

* [Deploy to a Windows VM](../cd/deploy-webdeploy-iis-deploygroups.md)
