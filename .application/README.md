# LLaMA Stack Operator Deployment

This repository contains the necessary Kubernetes/OpenShift manifests to deploy and manage the LLaMA Stack Operator and its components.

## Prerequisites

- OpenShift or Kubernetes cluster
- `oc` or `kubectl` CLI tool
- Cluster admin privileges
- A project named `llama-serve`

## Installation

1. First, deploy the Llama Stack Operator:

   ```bash
   oc apply -f llama-stack-operator.yaml
   ```

2. Deploy the Llama distribution:

   ```bash
   oc apply -f llama-distribution.yaml
   ```

3. (Optional) Generate test traffic:

   ```bash
   oc apply -f create-data-for-llama-job.yaml
   ```

   This creates a job that sends 50 requests to the Llama stack to generate sample traffic.

## Components

- `llama-stack-operator.yaml`: Contains the operator deployment and necessary RBAC rules
- `llama-distribution.yaml`: Defines the Llama stack distribution and configuration
- `create-data-for-llama-job.yaml`: Optional job to generate test traffic

## Verification

To verify the installation, check that all pods are running:

```bash
oc get pods -n <namespace>
```

## Cleanup

To remove all components:

```bash
oc delete -f llama-distribution.yaml
oc delete -f llama-stack-operator.yaml
```