# Kubernetes Lab

A hands-on learning lab built while working through Kubernetes fundamentals from scratch.

## What this is

This repo contains the YAML files from my first real Kubernetes session — creating Pods, Deployments, and Services on a local cluster using kind (Kubernetes IN Docker). Every file here was written, applied, broken, and understood before it was committed.

## What I built

- A bare Pod running nginx — to understand the smallest unit K8s knows about
- A Deployment with 3 replicas — to prove self-healing (kill a Pod, watch K8s replace it)
- A Service — to give the Deployment a stable address that survives Pod restarts

## Key concepts learned

**Pod** — the thing that actually holds your container inside K8s. Mortal on its own.

**Deployment** — the contract with K8s: "keep N copies of this running at all times." Self-healing. Scalable with one command.

**Service** — the permanent reception desk in front of your Pods. Pods die and get new IPs; the Service address never changes. Routes by label, not by IP.

**Why this matters** — Docker runs containers. It doesn't ask what *should* be running and enforce it. Kubernetes does. The Service + Deployment combination is what makes an app genuinely resilient.

## Stack

- kind v0.23.0 — local K8s cluster running inside Docker
- kubectl v1.36.2 — CLI to talk to the cluster
- WSL2 Ubuntu on Windows

## How to recreate this

```bash
kind create cluster --name my-cluster
kubectl apply -f deployment/my-deployment.yaml
kubectl apply -f service/my-service.yaml
kubectl port-forward service/nginx-service 8080:80
# visit http://localhost:8080
```

## Structure

```
kubernetes-lab/
├── pod/
│   └── my-pod.yaml           # bare Pod — learning exercise only
├── deployment/
│   └── my-deployment.yaml    # 3-replica nginx Deployment
└── service/
    └── my-service.yaml       # NodePort Service exposing the Deployment
```# Kubernetes-Lab
