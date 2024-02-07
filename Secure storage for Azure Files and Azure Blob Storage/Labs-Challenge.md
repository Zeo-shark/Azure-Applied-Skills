# Secure storage for Azure Files and Azure Blob Storage

## Tasks performed
- Create and configure a storage account
- Create and configure Blob Storage
- Create and configure Azure Files
- Configure encryption
- Configure networking for storage

## Core Topics: 
Azure Storage Accounts, Azure Blob, Azure Files

1. As part of our IT modernization initiative, we will be transitioning our on-premises applications to the AKS platform. Some of the initial prerequisites have already been implemented, including an Azure virtual network environment named VNET1.

This is your task:

Ensure that the AKS cluster can host deployments of containerized Windows applications.
Ensure that the AKS cluster has the fewest nodes possible, is scaled manually, and uses the B2ms virtual machine size.
Integrate the AKS cluster with a new container registry by using the managed identity of the cluster. The container registry must be named acr37718875.
Ensure that all the AKS nodes are connected to the VNET1 virtual network.
Ensure that the AKS cluster can scale out by using Azure Container Instances.

2. Our developers have built some Docker files for a project named Beehive. They want you to build and upload images for the project. Beehive consists of two images named app1 and db1. The developers also want you to deploy a pod to the dev and uat namespaces using a command line. If the namespaces do not exist, please create them.

This is your task:

You need to build the images and upload them to the repository. The Dockerfiles are located in C:\labtest\dockerfiles. The deployment must meet the following requirements:

The images must have a tag of v0.0.1.
The image for db1 must be named db1.
The image for app1 must be named app1.
The pod must be deployed to the dev and uat namespaces. The deployment YAML file is located in C:\labtest\dockerfiles\lab1\deployment.

3. We are concerned with the security of our AKS implementation; we want to ensure that all communication in transit is encrypted, and a central logging repository is implemented. We need your help to identify resources that fail to meet our security policy.

This is your task:

You need to configure the security of our AKS deployment to meet the following requirements:

All AKS clusters in the subscription must meet the Kubernetes clusters should be accessible only over HTTPS policy. Use Azure Policy to detect the AKS clusters in the subscription that do NOT.
Use Azure Policy to assign the Deploy - Configure diagnostic settings for Azure Kubernetes Service to Log Analytics workspace policy. The policy must ensure that all the AKS clusters use AKSLogAnalyticsWorkspace as the Log Analytics workspace.
Thanks,

Project Management Team

**Solution** 
- To ensure that all AKS clusters in the subscription are accessible only over HTTPS, you need to use Azure Policy to audit the clusters that do not meet this requirement. You can use the built-in policy definition named Kubernetes clusters should be accessible only over HTTPS1 to do this. To assign this policy, follow these steps2:
- In the Azure portal, search for and select Policy.
On the Policy page, select Assignments under Authoring.
On the Assignments page, select + Assign policy.
On the Assign policy page, enter or select the following information:
Scope: Select your subscription or resource group that contains the AKS clusters.
Policy definition: Select Kubernetes clusters should be accessible only over HTTPS from the list.
Assignment name: Enter a name for the assignment, such as AKS-HTTPS-Audit.
Assignment description: Enter an optional description for the assignment.
Parameters: Leave the default values.
Remediation: Leave the default values.
Compliance: Leave the default values.
Select Review + create and then select Create.
- After the policy is assigned, it will take some time to evaluate the compliance state of your AKS clusters. You can view the compliance details on the Policy page under Compliance. You can also use the Azure CLI or PowerShell to get the compliance data3. The policy will report non-compliant if any of the following conditions are true4:
The AKS cluster has a public IP address and a fully qualified domain name (FQDN) for the API server endpoint.
The AKS cluster has authorized IP ranges disabled.
The AKS cluster has private cluster disabled.
To fix the non-compliance, you need to either enable authorized IP ranges or private cluster for your AKS clusters. You can use the Azure portal, the Azure CLI, or PowerShell to do this5 .
- To ensure that all AKS clusters use AKSLogAnalyticsWorkspace as the Log Analytics workspace, you need to use Azure Policy to deploy the diagnostic settings for the clusters. You can use the built-in policy definition named Deploy - Configure diagnostic settings for Azure Kubernetes Service to Log Analytics workspace to do this. To assign this policy, follow these steps:
In the Azure portal, search for and select Policy.
On the Policy page, select Assignments under Authoring.
On the Assignments page, select + Assign policy.
On the Assign policy page, enter or select the following information:
Scope: Select your subscription or resource group that contains the AKS clusters.
Policy definition: Select Deploy - Configure diagnostic settings for Azure Kubernetes Service to Log Analytics workspace from the list.
Assignment name: Enter a name for the assignment, such as AKS-Diag-Deploy.
Assignment description: Enter an optional description for the assignment.
Parameters: Select AKSLogAnalyticsWorkspace as the Log Analytics workspace name and resource ID. You can also customize the diagnostic settings categories and retention days as needed.
Remediation: Leave the default values.
Compliance: Leave the default values.
- Select Review + create and then select Create.
After the policy is assigned, it will take some time to deploy the diagnostic settings to your AKS clusters. You can view the deployment details on the Policy page under Remediation tasks. You can also use the Azure CLI or PowerShell to get the deployment data. The policy will report compliant if the diagnostic settings are successfully deployed and configured for your AKS clusters.