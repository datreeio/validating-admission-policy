# Validating admission policy 
Kubernetes Validation Admission Policy - local testing guide and valuable resources
Disclaimer - supported from 1.26

## What is Validating admission policy (VAP)?
Starting with version `1.26`, Kubernetes provides a new resource kind named `ValidatingAdmissionPolicy`, which offers a declarative, in-process alternative to validating admission webhooks.  
Read more about it [here](https://datree.slack.com/archives/D02S4JK41QD/p1687703168120579).

## What is Common expression language (CEL)?
CEL is an an open-source language that implements common semantics for expression evaluation.
In the world of Kubernetes, CEL is used within VAPs to declare validation rules and enforce them on a cluster.

## Testing/playground local
### Prerequisites
#### Minikube
Install the latest version using `brew`:
```
brew install minikube
```
If Minikube is already installed, upgrade it to the latest version:
```
brew upgrade minikube
```
If you're not using `brew`, see the [Minikube docs](https://minikube.sigs.k8s.io/docs/start/) for other ways to install/upgrade.

### Instructions
#### Start up your VAP-supported cluster
Run the following command:
```
minikube start --kubernetes-version=1.27.0-rc.0 --extra-config=apiserver.runtime-config=admissionregistration.k8s.io/v1alpha1  --feature-gates='ValidatingAdmissionPolicy=true'
```
This command specifies and enables the necessary Kubernetes version and feature gate to use VAPs in your cluster 🥳

<br/>

#### Download example files:
To see some policy enforcement in action, there are 3 components we will need:
  * `ValidatingAdmissionPolicy` resource - this is where our rule logic will be defined.
  * `ValidatingAdmissionPolicyBinding` resource - this is where we specify where and on which resources to run the validation. 
  * A resource manifest - an example YAML that violates our rule.

We have created these components for you so you can quickly run it on your machine. Simply [download the latest release](https://github.com/datreeio/validating-admission-policy/releases/latest/download/exampleFiles.zip) from this repo.

<br/>

#### Step by step!
In your terminal, `cd` to the dir containing the example files, then:
1. Apply the `ValidatingAdmissionPolicy` containing the rule logic
```
kubectl apply -f ./vap.yaml
```
This rule validates that the resource has at least 2 replicas.

2. Apply the `ValidatingAdmissionPolicyBinding`
```
kubectl apply -f ./vapBinding.yaml
```
The binding specifies that all objects with the label `example: test` will be validated.

3. Apply the violating resource
```
kubectl apply -f ./exampleResource.yaml
```
This Deployment has only 1 replica, and since it has the `example: test` label, it will be validated and denied by the VAP. 

![deny-msg](/resources/images/example-deny-msg.png)



## Useful links

## Troubleshooting
