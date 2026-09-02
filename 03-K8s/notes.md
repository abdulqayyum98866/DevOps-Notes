# Kubernetes Architecture — Notes & Diagrams

A concise reference on how Kubernetes is structured, what each component does, and how a request flows through the system.

## Overview

Kubernetes clusters are split into two halves:

- **Control Plane** — the brain. Makes global decisions (scheduling, scaling, healing) and keeps track of the cluster's desired state.
- **Worker Nodes** — the muscle. Run your actual application containers.

![Kubernetes Architecture]()

## Control Plane Components

| Component | Definition |
|---|---|
| **API Server** | The single entry point into the cluster. Every command — from `kubectl`, controllers, or other components — goes through it. It validates requests and exposes the Kubernetes API. |
| **etcd** | A distributed key-value store that holds the entire cluster's state — what should exist, and the current configuration of every object. The single source of truth. |
| **Scheduler** | Watches for newly created pods with no node assigned, and decides which worker node they should run on, based on resource availability and constraints. |
| **Controller Manager** | Runs controller processes that continuously watch the cluster's actual state and reconcile it toward the desired state (e.g. replacing a pod that crashed). |

## Worker Node Components

| Component | Definition |
|---|---|
| **Kubelet** | An agent running on every node. It receives instructions from the control plane and ensures the containers described in a pod spec are running and healthy. |
| **Kube-proxy** | Maintains network rules on each node, enabling network communication to pods from inside or outside the cluster. |
| **Container Runtime** | The software that actually runs containers (e.g. containerd, CRI-O). Kubelet talks to it to start/stop containers. |
| **Pod** | The smallest deployable unit in Kubernetes. Wraps one or more containers that share the same network namespace (IP address) and storage volumes. |

## Networking Flow

![Kubernetes Networking](./k8s-networking.svg)

| Concept | Definition |
|---|---|
| **Pod IP** | Every pod gets its own cluster-internal IP address. Pods can communicate directly using these IPs. |
| **Ephemeral IPs** | Pods are disposable — when one restarts or is rescheduled, it gets a *new* IP. Nothing should hard-code a pod IP. |
| **Service** | A stable virtual IP and DNS name sitting in front of a group of pods (matched via label selectors). It load balances traffic across whichever pods are currently healthy. |
| **kube-proxy routing** | Implements the actual routing rules on each node so traffic sent to a Service IP is forwarded to a live, matching pod IP. |

## End-to-End Flow: `kubectl apply`

1. You run `kubectl apply -f deployment.yaml`.
2. The request hits the **API server**, which validates and stores the desired state in **etcd**.
3. The **Scheduler** notices new, unscheduled pods and assigns each one to a suitable **worker node**.
4. The **kubelet** on that node pulls the container image and starts the containers via the **container runtime**.
5. The **Controller Manager** continuously checks that the actual number of running pods matches what was requested — recreating any that fail.
6. A **Service** in front of these pods gives external traffic a stable way to reach them, with **kube-proxy** handling the routing to healthy pod IPs.

## Quick Glossary

- **Cluster** — the full set of control plane + worker node machines Kubernetes manages.
- **Deployment** — a higher-level object that manages a set of identical pods (handles scaling, rolling updates).
- **Node** — a single machine (VM or physical) that's part of the cluster.
- **Namespace** — a way to logically divide a cluster (e.g. `dev`, `staging`, `prod`).

---
*Diagrams generated for personal study notes.*



