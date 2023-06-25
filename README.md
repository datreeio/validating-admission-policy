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
### install minikube (version 1.27)
### Download example:
  * VAP
  * VAPB
  * example yaml
### explain each part and show command to apply it
### expected result img

## Useful links


