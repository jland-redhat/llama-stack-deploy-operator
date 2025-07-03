# Llama Stack Distribution Operator

A Kubernetes operator for deploying and managing Llama Stack distributions on OpenShift with observability integration.

## Overview

This Helm chart provides a Kubernetes operator that manages the deployment and configuration of Llama Stack distributions, specifically designed to work with OpenShift. It includes integration with OpenTelemetry for observability and supports remote vLLM inference.

## Prerequisites

- OpenShift 4.10 or later
- Helm 3.0 or later
- OpenTelemetry Collector (for metrics and tracing)
- vLLM inference service

## Installation

1. Clone this repository:

   ```bash
   git clone <repository-url>
   cd llama-stack-deploy-operator
   ```

2. Install the chart directly from the local directory:

   ```bash
   helm install my-llama-stack . -n your-namespace
   ```

   Or to install in a specific namespace:

   ```bash
   helm install my-llama-stack . -n your-namespace --create-namespace
   ```

## Configuration

The following table lists the configurable parameters and their default values.

| Parameter | Description | Default |
|-----------|-------------|---------|
| `playground.image` | Container image for the playground UI | `quay.io/jland/llama-stack-playground:v0.2.12` |
| `llamastackdistribution.vllm.url` | vLLM service endpoint | `http://granite-33-2b-instruct-predictor.model-as-a-service.svc.cluster.local:8080/v1` |
| `llamastackdistribution.vllm.model` | Default inference model | `granite-33-2b-instruct` |
| `llamastackdistribution.otel_trace_endpoint` | OpenTelemetry trace endpoint | `http://otel-collector-collector.redhat-ods-monitoring.svc.cluster.local:4318/v1/traces` |
| `llamastackdistribution.otel_metric_endpoint` | OpenTelemetry metrics endpoint | `http://otel-collector-collector.redhat-ods-monitoring.svc.cluster.local:4318/v1/metrics` |

## Customizing the Deployment

You can customize the deployment by creating a `values.yaml` file and overriding the default values:

```yaml
playground:
  image: your-registry/llama-stack-playground:your-tag

llamastackdistribution:
  vllm:
    url: "http://your-vllm-service:8080/v1"
    model: "your-model-name"
  otel_trace_endpoint: "http://your-otel-collector:4318/v1/traces"
  otel_metric_endpoint: "http://your-otel-collector:4318/v1/metrics"
```

Then install with your custom values:

```bash
helm install my-llama-stack llama-stack/llama-stack-distribution -f values.yaml -n your-namespace
```

## Customizing Llama Stack Configuration

You can customize the Llama Stack configuration by modifying the `files/run.yaml` file before installation. This file contains the main configuration for the Llama Stack deployment.

For a complete reference of available configuration options, please refer to the [Llama Stack Documentation](https://llama-stack.readthedocs.io/en/latest/distributions/configuration.html#runtime-override).

## Components

- **LlamaStackDistribution CRD**: Custom Resource Definition for managing Llama Stack deployments
- **Playground UI**: Web interface for interacting with the deployed models
- **OpenTelemetry Integration**: Built-in support for metrics and tracing
- **vLLM Integration**: Support for remote vLLM inference
