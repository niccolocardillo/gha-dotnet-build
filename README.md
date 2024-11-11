# .NET Build

Uses the .NET CLI `dotnet build` [command](https://learn.microsoft.com/en-us/dotnet/core/tools/dotnet-build) that builds specified projects or the solution itself including all of its dependencies.

Supports `projects` input we learned to appreciate from [AzDO DotNetCoreCLI](https://learn.microsoft.com/en-us/azure/devops/pipelines/tasks/reference/dotnet-core-cli-v2?view=azure-pipelines).

## Usage

To use this action in your GitHub repository, you can follow these steps:

```yaml
uses: maurosoft1973/dotnet-build@v1
```

### Inputs

```yaml
with:
  # Optional path to the project(s) file to restore. Pass empty to have MSBuild use the default behavior.
  # Supports globbing.
  projects: 'src/**/*.csproj'
  # Defines the build configuration.
  configuration: 'Release'
  # Compiles for a specific framework. The framework must be defined in the project file.
  framework: 'net8.0'
  # Sets the verbosity level of the command.
  # Allowed values are q[uiet], m[inimal], n[ormal], d[etailed], and diag[nostic]. 
  # The default is quiet.
  level: 'quiet'
  # Provides a way to fully customize the build. See https://learn.microsoft.com/en-us/visualstudio/msbuild/msbuild-command-line-reference?view=vs-2022#switches for more information.
  buildSwitches: ''
  # Upload the generated build artifact. The artifact name is: "framework.configuration" (Ex: framework: net8.0, configuration: Release, the name of artifact is : net8.0-Release)
  uploadBuildArtifact: 'true'
  # When set, current workspace will be overwritten with the content of the restore cache.
  restoreCacheKey: ''
```

### Outputs

This action has no outputs.

## Examples

### Build all project into src/**/ *.csproj with configuration Release

```yaml
- name: Build for Release
  uses: maurosoft1973/dotnet-build@v1
  with:
    configuration: Release
```

### Build specified project with configuration Release

```yaml
- name: Build for Release
  uses: maurosoft1973/dotnet-build@v1
  with:
    configuration: Release
    projects: 'src/ProjectExample/*.csproj'
```

### Build all project into src/**/*.csproj with configuration Debug without upload artifact

```yaml
- name: Build for Debug
  uses: maurosoft1973/dotnet-build@v1
  with:
    configuration: Debug
    uploadBuildArtifact: false
```

### Build all project into src/**/ with configuration Debug and use restore Cache.

```yaml
- name: Build
  uses: maurosoft1973/dotnet-build@v1
  with:
    configuration: Debug
    restoreCacheKey: dotnet-restore-sha256
```

## Contributing to .NET Build

Contributions are welcome! 
Feel free to submit issues, feature requests, or pull requests to help improve this action.

### License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
