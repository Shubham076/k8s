
## Introduction

Helm is a package manager for Kubernetes, allowing you to define, install, and upgrade even the most complex Kubernetes applications. This README provides a basic guide on how to use Helm for creating Helm charts and lists some common Helm commands.

## Prerequisites

-   Kubernetes cluster
-   Helm installed on your machine
-   Basic understanding of Kubernetes objects and YAML

## Creating a Helm Chart

### Step 1: Install Helm

Ensure that Helm is installed on your machine. You can download it from the [Helm Releases](https://github.com/helm/helm/releases) page.

### Step 2: Create a New Chart

Run the following command to create a new chart:

bashCopy code

`helm create mychart` 

This command creates a new directory `mychart` with the structure of a Helm chart.

### Step 3: Understand Chart Structure

The basic structure of a Helm chart:

-   `Chart.yaml`: The main chart description file.
-   `values.yaml`: The default configuration values for the chart.
-   `templates/`: The directory where Kubernetes resources are defined as templates.
-   `charts/`: Optional directory for sub-charts.

### Step 4: Customize Your Chart

Edit the files in the `templates/` directory to define the Kubernetes resources you want to manage with your chart. Update `values.yaml` to reflect any default values you want your chart to use.

### Step 5: Package Your Chart

Package your chart into a chart archive file with:

`helm package mychart` 

## Common Helm Commands

-   **Install a Chart**
    `helm install [RELEASE_NAME] [CHART_NAME]` 
    
-   **List Releases**
    `helm list` 
    
-   **Upgrade a Release**
    `helm upgrade [RELEASE_NAME] [CHART_NAME]` 
    
-   **Rollback a Release**
    `helm rollback [RELEASE_NAME] [REVISION]` 
    
-   **Uninstall a Release**
    `helm uninstall [RELEASE_NAME]` 
    
-   **Fetch a Chart**
    `helm pull [REPO/CHART]` 
    
-   **View Chart Information**
    `helm show all [CHART]` 
    
-   **Lint a Chart**
    `helm lint [CHART_PATH]` 
    
-   **Debug a Release**
    `helm install --debug --dry-run [RELEASE_NAME] [CHART]` 
    
-   **Search for Charts**
    `helm search repo [KEYWORD]` 

-  **Values**
    To see the values for a specific Helm release, you can use the following command:
    `helm get values [RELEASE_NAME] [CHART]`
    

### Release
 "release" is an instance of a Helm chart running in a Kubernetes cluster.
 ```
helm install my-release-name stable/my-chart
```

### Revision
- Each time you update or modify a release, such as upgrading to a new version of the chart or updating the configuration, Helm increments the revision number.
- Purpose: This allows you to track changes over time and roll back to previous versions of a release if needed

#### Initial 
 ```
helm install my-release-name stable/my-chart
```

#### First Update
When you first install a release, it is at revision 1.
```
helm upgrade my-release-name stable/my-chart --set someParameter=someValue
```

### Helm install
When you run a helm install command with Helm, it initiates the deployment of the components defined in the Helm chart into your Kubernetes cluster. This includes creating Kubernetes resources like Pods, Deployments, Services, and any other resources specified in the chart's templates.

Here's a breakdown of what happens:

- Reads the Chart: Helm reads the chart (a collection of files that describe a related set of Kubernetes resources) and its values.yaml file to understand what resources need to be created or configured.

- Template Rendering: Helm processes the templates in the chart with the values provided either from the values.yaml file or from any overrides you provide at install time. This rendering step converts the Helm templates into valid Kubernetes manifest files.

- Resource Creation: Helm then sends these generated manifest files to the Kubernetes API server, instructing it to create the resources described in these manifests.

- Creating Pods and Other Resources: If the chart includes Deployments, StatefulSets, DaemonSets, etc., the Kubernetes API server processes these manifests and starts creating the resources. For example, if a Deployment is defined, the Kubernetes scheduler starts creating the required Pods.

- Resource Management: Helm tracks the resources it creates as a release. This allows Helm to manage the lifecycle of these resources, including upgrading, rolling back, or deleting them.

- Feedback to User: Helm provides feedback about the status of the installation, including any errors encountered during the deployment process.

## Conclusion

Helm is a powerful tool for managing Kubernetes applications. By creating Helm charts, you can simplify the deployment and management of complex applications. The commands listed above are a starting point for interacting with Helm and managing your charts.