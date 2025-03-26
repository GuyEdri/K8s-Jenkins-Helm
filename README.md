#K8s-Jenkins-Helm

The K8s-Jenkins-Helm project provides a framework for deploying Jenkins on a Kubernetes cluster using Helm charts. This setup enables scalable and efficient continuous integration and continuous deployment (CI/CD) pipelines within a Kubernetes environment.

#Features

Kubernetes Deployment: Utilizes Kubernetes manifests (cluster.yaml) to define and manage the deployment of Jenkins and related services within the cluster.

Helm Integration: Leverages Helm charts for streamlined installation and management of Jenkins, simplifying the deployment process.

AWS Integration: Includes scripts (awsalb.sh) and IAM policies (iam_policy.json) to facilitate integration with AWS services, such as setting up an Application Load Balancer for managing external access to Jenkins.

Sample Applications: Contains example applications (my-apps/weather-app) with corresponding Jenkinsfile configurations to demonstrate CI/CD pipelines.

#Repository Structure

my-apps/weather-app/: Sample application demonstrating CI/CD pipeline integration.

Jenkinsfile: Defines the CI/CD pipeline stages for Jenkins.

awsalb.sh: Shell script for setting up AWS Application Load Balancer.

cluster.yaml: Kubernetes manifest for deploying Jenkins and related services.

iam_policy.json: AWS IAM policy definitions for necessary permissions.


#Explanation

Developers interact with the Jenkins Master to initiate CI/CD pipelines.

Jenkins Agents are dynamically provisioned within the Kubernetes cluster to execute build and deployment tasks.

Sample applications, like the Weather App, are deployed and managed within the cluster.

AWS services, such as IAM and ALB, are utilized for authentication, authorization, and external access management.

#Getting Started

1. Set Up Kubernetes Cluster

Ensure you have a running Kubernetes cluster. Tools like Minikube or Kind can be used for local setups.

2. Install Helm

Helm is a package manager for Kubernetes. Install it by following the official Helm installation guide.

3. Deploy Jenkins Using Helm

##Add the Jenkins Helm repository:

helm repo add jenkins https://charts.jenkins.io
helm repo update

##Create a namespace for Jenkins:

kubectl create namespace jenkins

##Install Jenkins:

helm install jenkins jenkins/jenkins --namespace jenkins

For detailed instructions, refer to the Jenkins Helm Chart documentation.

4. Configure AWS Integration

Use the awsalb.sh script to set up the AWS Application Load Balancer. Ensure you have the AWS CLI installed and configured.

Apply the IAM policies defined in iam_policy.json to grant necessary permissions.

5. Deploy Sample Application

Navigate to the my-apps/weather-app directory.

Review and customize the Jenkinsfile to suit your pipeline requirements.

Commit your changes and push to your repository to trigger the Jenkins pipeline.
