# Kubernetes Troubleshooting Guide

While working with Kubernetes on OKE (Oracle Kubernets Engine), I encountered many issues, so I decided to create a troubleshooting guide to help identify and resolve common problems in Kubernetes deployments. 🌟🌟🌟

- Pod issues (e.g., CrashLoopBackOff, ImagePullBackOff)
- Service misconfigurations
- Ingress connectivity problems

## Introduction
Kubernetes deployments can encounter various issues ranging from pod scheduling problems to service misconfigurations. This guide provides a systematic approach to: 🌐🌐🌐
- Identify the root cause of issues.
- Apply appropriate fixes.
- Ensure a smooth deployment process.

## Features

- **Step-by-Step Troubleshooting Instructions**: Navigate problems systematically.
- **Flowcharts**: Visualize solutions with embedded diagrams.
- **Command Examples**: Useful Kubernetes CLI commands.

## Table of Contents

1. [Introduction](#introduction)
2. [Troubleshooting Pods](#troubleshooting-pods)
3. [Troubleshooting Services](#troubleshooting-services)
4. [Troubleshooting Ingress](#troubleshooting-ingress)
5. [General Debugging Commands](#general-debugging-commands)

 
### Pods Troubleshooting Flowchart
#### Step 1: Check Pod Status

1. Run: 🐳🐳🐳

```kubectl get pods```

2. Observe the pod's status:

* **PENDING**: Move to Step 2.
* **CrashLoopBackOff**: See Step 3.
* **ImagePullBackOff**: Refer to Step 4.

#### Step 2: Check Resource Availability
* verify if the cluster has sufficient resources: ⚙️⚙️⚙️

   ```kubectl describe pod <pod-name>```

* If resources are insufficient:
  * Scale up the cluster.
  * Relax ResourceQuota limits if applicable.

####  Step 3: Inspect CrashLoopBackOff

1. Check logs: 🛠️🛠️🛠️

   ```kubectl logs <pod-name> --previous```

2. Common fixes:
   * Update Dockerfile to include CMD if missing.
   * Fix readiness or liveness probes if they are failing.

####  Step 4: Fix ImagePullBackOff

1. Verify the image name and tag: 🖼️🖼️🖼️

   ```kubectl describe pod <pod-name>```

2. Common solutions:
   * Correct image name/tag.
   * Configure access to private registries if required.

### Services Troubleshooting Flowchart

#### Step 1: Verify Service Configuration
 
1. Check if the service exposes the correct port: 🧩🧩🧩
   
   ```kubectl describe service <service-name>```
   
3. Ensure targetPort matches the container's containerPort.

#### Step 2: Debug Endpoint Connectivity

1. Verify endpoints: 📡📡📡
   ```kubectl get endpoints``
2. If no endpoints are listed:
3. Check if the service selector matches pod labels.
4. Inspect pod readiness.

#### Step 3: Test Port Forwarding

1. Forward a service port to localhost: 🌐🌐🌐

```kubectl port-forward service/<service-name> 8080:<service-port>```

2. Verify the app's accessibility at http://localhost:8080.

### Ingress Troubleshooting Flowchart

#### Step 1: Inspect Ingress Configuration

1. Describe ingress: 🛣️🛣️🛣️

``` kubectl describe ingress <ingress-name>```

2. Check serviceName and servicePort mappings.

#### Step 2: Verify Backend Status

1. Ensure backends are listed: 🎯🎯🎯

```kubectl get endpoints```

2. If backends are missing:
3. Fix service configuration.
4. Verify pod readiness and labels.

#### Step 3: Debug Ingress Connectivity

1. Forward ingress port to localhost: 🚀🚀🚀

```kubectl port-forward <ingress-pod-name> 8080:<ingress-port>```

2. Test access at http://localhost:8080.

## Contributions

We welcome contributions! Please open an issue or submit a pull request to help improve this guide.

## References

- [Kubernetes Documentation](https://kubernetes.io/docs/)
- [LearnK8s Troubleshooting Guide](https://learnk8s.io/troubleshooting-deployments)
