  <table>
  <tr>
    <td>![icon](../../../steps/utility/_img/command-line.png)<br/>[Utility: Command Line](../../../steps/utility/command-line.md)</td>
    <td>
      <p>Restore NuGet packages.</p>
      <ul>
        <li>Tool: `dotnet`</li>
        <li>Arguments: `restore`</li>
        <li>Advanced, Working folder: Folder in which the project.json file (for projects created with VS 2015) or .csproj file (for projects created with VS 2017) exists.</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td>![icon](../../../steps/build/_img/visual-studio-build.png)<br>[Build: Visual Studio Build](../../../steps/build/visual-studio-build.md)</td>
    <td>
      <p>(Optional) Build any additional projects that are checked in.<p>
      <ul>
          <li>Solution: ` **\*.sln `</li>
          <li>Platform: `$(BuildPlatform)`</li>
          <li>Configuration: `$(BuildConfiguration)`</li>
          <li>Visual Studio Version: Select `Visual Studio 2015` if your project was created in VS 2015 Update 3. Select `Visual Studio 2017` is your project was created in VS 2017.</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td>![Command line](../../../steps/utility/_img/command-line.png)<br/>[Utility: Command Line](../../../steps/utility/command-line.md)</td>
    <td>
      <p>Build your ASP.NET Core project and publish the output to a folder.</p>
      <ul>
        <li>Tool: `dotnet`</li>
        <li>Arguments: `publish -c $(BuildConfiguration) -o $(Build.ArtifactStagingDirectory)`</li>
        <li>Advanced, Working folder: Folder in which the project.json file (for projects created with VS 2015) or .csproj file (for projects created with VS 2017) exists.</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td>![icon](../../../steps/test/_img/visual-studio-test-icon.png)<br/>[Test: Visual Studio Test](../../../steps/test/visual-studio-test.md)</td>
    <td>
    <p>(Optional) Run your tests. See</p>
   <ul>
   <li>[Getting started with continuous testing](../../../../test/continuous-testing/getting-started/getting-started-with-continuous-testing.md)</li>
    <li>[Continuous testing scenarios and capabilities](../../../../test/continuous-testing/index.md).</li>
    </ul>
    </td>
  </tr>
  <tr>
    <td>![icon](../../../steps/utility/_img/archive-files.png)<br>[Utility: Archive Files](../../../steps/utility/archive-files.md)</td>
    <td>
      <p>Archive the output into a web deploy package.</p>
      <ul>
        <li>Root folder to archive: `$(Build.ArtifactStagingDirectory)`</li>
        <li>Prefix root folder name to archive paths: Unchecked
        <li>Archive type: `zip`</li>
        <li>Artifact file to create: `$(Build.ArtifactStagingDirectory)/$(Build.BuildId).zip`</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td>![icon](../../../steps/utility/_img/publish-build-artifacts.png)<br>[Utility: Publish Build Artifacts](../../../steps/utility/publish-build-artifacts.md)</td>
    <td>
      <p>Publish the build artifacts to be consumed by a release definition.</p>
      <ul>
        <li>Path to publish: `$(Build.ArtifactStagingDirectory)/$(Build.BuildId).zip`</li>
        <li>Artifact name: `drop`</li>
        <li>Artifact type: Server</li>
      </ul>
    </td>
  </tr>
  </table>