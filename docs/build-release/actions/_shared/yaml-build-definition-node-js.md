steps:
- task: Npm@1
  displayName: npm install

- task: Gulp@0
  inputs:
    publishJUnitResults: "true"
    displayName: Gulp

- task: ArchiveFiles@1
  inputs:
    rootFolder: "$(System.DefaultWorkingDirectory)"
    includeRootFolder: "false"
    displayName: Zip up the files

- task: PublishBuildArtifacts@1
  inputs:
    PathtoPublish: $(Build.ArtifactStagingDirectory)
    ArtifactName: "drop"
    ArtifactType: "Container"
    displayName: Publish the artifacts
