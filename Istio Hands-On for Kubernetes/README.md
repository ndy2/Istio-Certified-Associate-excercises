---
site: udemy
url: https://www.udemy.com/course/istio-hands-on-for-kubernetes
tags:
  - kubernetes
  - devops
  - istio
---
- 1.Introduction
	- [x] Introduction

- 2.Getting Started
	- [x] What is Istio

- 4.Hands on Demo 
	- [x] Getting Istio Running
	- [x] Enabling Sidecar Injection
	- [x] Visualizing the System with Kiali
	- [x] Finding Perfoermance Problems

- 5.Introducing Envoy
	- [x] Introducing Envoy - The Data Plane
	- [x] Going Depper into Envoy

- 6. Telemetry
- [x] Starting the Demo System
- [x] Kiali Deeper Dive
- [x] Kiali Dynamic Traffic Routing
- [x] Distributed Tracing Overview
- [x] Using Jaeger UI
- [x] Why you need to "Propagete Headers"
- [x] What happens if you don't propagate headers?
- [x] Metrics with Grafana

```bash
# fix jaeger

k apply -f https://raw.githubusercontent.com/istio/istio/master/samples/addons/jaeger.yaml



```

```bash
# fix kiali
k delete deploy kiali -n istio-system
k delete sa kiali -n istio-system
k delete cm kiali -n istio-system
k delete service kiali -n istio-system

k delete clusterrole kiali-viewer
k delete clusterrole kiali
k delete clusterrolebindings.rbac.authorization.k8s.io kiali

helm install kiali-server kiali/kiali-server --namespace istio-system --set auth.strategy="anonymous" --version 1.40.0
kubectl patch service kiali -n istio-system -p '{"spec": {"type": "NodePort", "ports": [{"port": 80, "targetPort": 80, "nodePort": 31000, "name": "http"}]}}'
```

  