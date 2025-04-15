---
author: ckanyika
ms.author: ckanyika
ms.date: 3/20/2025
ms.topic: include
---

### Hosted image updates

We’re rolling out updates to keep Azure Pipelines’ hosted agents secure and current. These updates include adding support for Ubuntu-24.04, Windows 2025 images, and macOS-15 Sequoia, while deprecating older images like Ubuntu-20.04 and Windows Server 2019. 

For more details, please visit our [blog post](https://devblogs.microsoft.com/devops/upcoming-updates-for-azure-pipelines-agents-images/).

#### macOS-15 Sequoia is generally available

The `macOS-15` image will be available on Azure Pipelines hosted agents starting April 1. To use this image, update your YAML file to include `vmImage:'macos-15'`:  

```yaml
- job: macOS15
  pool:
    vmImage: 'macOS-15'
  steps:
  - bash: |
      echo Hello from macOS Sequoia
      sw_vers
```

For macOS-15 installed software, see [image configuration](https://github.com/actions/runner-images/blob/main/images/macos/macos-15-Readme.md).

The `macOS-14` image will still be used when specifying `macOS-latest`. We'll update `macOS-latest` to use `macOS-15` in April.

#### Windows-2025 image is available in preview

The `windows-2025` image is now available in preview for Azure Pipelines hosted agents. To use this image, update your YAML file to include `vmImage:'windows-2025'`:  

```yaml
- job: win2025
  pool:
    vmImage: 'windows-2025'
  steps:
  - pwsh: |
      Write-Host "(Get-ComputerInfo).WindowsProductName"
      Get-ComputerInfo | Select-Object WindowsProductName
      Write-Host "`$PSVersionTable.OS"
      $PSVersionTable.OS
```

For Window Server 2025 installed software, see [image configuration](https://github.com/actions/runner-images/blob/main/images/windows/Windows2025-Readme.md).


#### The ubuntu-latest pipeline image will start using ubuntu-24.04

In the coming weeks, pipeline jobs specifying `ubuntu-latest` will start using `ubuntu-24.04` instead of `ubuntu-22.04`.

For guidance on tasks that use tools that are no longer on the `ubuntu-24.04` image, see our [blog post](https://devblogs.microsoft.com/devops/upcoming-updates-for-azure-pipelines-agents-images/). To keep using Ubuntu 22.04, use the `ubuntu-22.04` image label:

```yaml
- job: ubuntu2404
  pool:
    vmImage: 'ubuntu-24.04'
  steps:
  - bash: |
      echo Hello from Ubuntu 24.04
      lsb_release -d
  - pwsh: |
      Write-Host "`$PSVersionTable.OS"
      $PSVersionTable.OS
```


#### The ubuntu-20.04 pipeline image is deprecated and will be retired April 1

We're deprecating support for the Ubuntu 20.04 image in Azure Pipelines because it will reach its end of support soon. Find the deprecation plan with brownout schedule in our [blog post](https://devblogs.microsoft.com/devops/upcoming-updates-for-azure-pipelines-agents-images/#ubuntu).


### Workload identity federation uses Entra issuer

Just over a year ago, we made [Workload identity federation generally available](https://devblogs.microsoft.com/devops/workload-identity-federation-for-azure-deployments-is-now-generally-available/). Workload identity federation allows you to configure a service connection without a secret. The identity (App registration, Managed Identity) underpinning the service connection can only be used for the intended purpose: the service connection configured in the identity's federated credential.

We're now changing the format of the federated credential for new Azure and Docker service connections. Existing service connections will work as before.

|    &nbsp;     | Azure DevOps issuer                                                 | Entra issuer (new service connections)                        |
|---------|---------------------------------------------------------------------|---------------------------------------------------------------|
| Issuer  | `https://vstoken.dev.azure.com/<organization id>`                   | `https://login.microsoftonline.com/<Entra tenant id>/v2.0`    |
| Subject | `sc://<organization name>/<project name>/<service connection name>` | `<entra prefix>/sc/<organization id>/<service connection id>` |

There's no change in configuration and the way tokens are obtained stays the same. Pipeline tasks don't need to be updated and work as before. 

The steps to create a service connection aren't changing and in most cases, the new issuer isn't visible. When [configuring an Azure service connection manually](/azure/devops/pipelines/release/configure-workload-identity), you'll see the new federated credentials displayed:

> [!div class="mx-imgBorder"]
> [![Screenshot of FIC example.](../../media/253-pipelines-01.png "Screenshot of FIC example")](../../media/253-pipelines-01.png#lightbox)

Copy these values as before when creating a federated credential for an App registration or Managed Identity.

#### Automation

When creating a service connection in automation with the [REST API](/rest/api/azure/devops/serviceendpoint/endpoints/create), use the federated credential returned by the API:

```json
authorization.parameters.workloadIdentityFederationIssuer
authorization.parameters.workloadIdentityFederationSubject
```

Likewise, when creating a service connection with the Terraform azuredevops provider, the [azuredevops_serviceendpoint_azurerm](https://registry.terraform.io/providers/microsoft/azuredevops/latest/docs/resources/serviceendpoint_azurerm#attributes-reference) resource returns `workload_identity_federation_issuer` and `workload_identity_federation_subject` attributes.

#### More information

- [Connect to Azure with an Azure Resource Manager service connection](/azure/devops/pipelines/library/connect-to-azure)
- [Troubleshoot an Azure Resource Manager workload identity service connection](/azure/devops/pipelines/release/troubleshoot-workload-identity)

###  Gradle@4 task

A new [Gradle@4](/azure/devops/pipelines/tasks/reference/gradle-v4) task has been created with support for [Gradle 8.0](https://docs.gradle.org/8.0/userguide/upgrading_version_7.html). The built-in code coverage option is removed from the `Gradle` task starting with `Gradle@4`. To use code coverage with Gradle in your pipeline:

- Specify code coverage plugins in your build.gradle file. For more information, see [Gradle code analysis options](https://docs.gradle.org/current/userguide/plugin_reference.html#code_analysis).
- Use the [PublishCodeCoverageResults@2](/azure/devops/pipelines/tasks/reference/publish-code-coverage-results-v2) task in your pipeline after the `Gradle@4` task.

Configuration of the SonarQube analysis was moved to the [SonarQube](https://marketplace.visualstudio.com/items?itemName=SonarSource.sonarqube) or [SonarCloud](https://marketplace.visualstudio.com/items?itemName=SonarSource.sonarcloud) extensions in the task `Prepare Analysis Configuration`.


### stringList parameter type

One of the top requested YAML pipelines features is to [define parameters that contain a list of items](https://developercommunity.visualstudio.com/t/parameters-that-support-multiselect/1224839).

With this sprint, we've added a new parameter type, named `stringList`, that provides this capability.

Say you want to allow those who queue pipeline runs to choose which regions they want to deploy a payload to. Now you can do this as shown in the example below.

```yaml
parameters:
- name: regions
  type: stringList
  displayName: Regions
  values:
    - WUS
    - CUS
    - EUS

stages:
- ${{ each stage in parameters.regions}}:
  - stage: ${{stage}}
    displayName: Deploy to ${{stage}}
    jobs:
    - job:
      steps:
      - script: ./deploy ${{stage}}
```

When queuing this pipeline, you'll now have the option of choosing multiple regions to deploy to, as shown in the following screenshot:

> [!div class="mx-imgBorder"]
> [![Screenshot of choosing multiple regions.](../../media/253-pipelines-02.png "Screenshot of choosing multiple regions")](../../media/253-pipelines-02.png#lightbox)

### Identity of user who requested a stage to run

To improve security of your YAML pipelines, you may wish to know who requested a stage to run. To address this need, were adding two new predefined variables, `Build.StageRequestedBy` and `Build.StageRequestedById`. These variables are similar to the `Build.RequestedFor` and `Build.RequestedForId` variables, but for a stage, not a run.

When a user explicitly triggers a user, for example, in case of a manually triggered stage or rerunning a stage, their identity is used to fill in the two variables.

