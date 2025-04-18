# Istio-Certified-Associate-excercises

see https://training.linuxfoundation.org/certification/istio-certified-associate-ica/

## Logistics

- Duration: 2hrs/ Cost: $250/ Passing Score : 75%/ Get a free retake

## Curriculums

see https://github.com/cncf/curriculum/blob/master/ICA_Curriculum.pdf

A. Istio Installation, Upgrade & Configuration (7%)
- Using the Istio CLI to install a basic cluster
- Customizing the Istio installation with the IstioOperator API
- Using overlays to manage Istio component settings

B. Traffic Management(40%)
- Controlling network traffic flows within a service mesh
- Configuring sidecar injection
- Using the Gateway resource to configure ingress and egress traffic
- Understanding how to use ServiceEntry resources for adding entries to internal service registry
- Define traffic policies using DestinationRule
- Configure traffic mirroring capabilities

C. Resilience and Fault Injection (20%)
- Configuring circuit breakers(with or without outlier detection)
- Using resilience features
- Creating fault injection

D. Securing Workloads(20%)
- Understand Istio security features
- Set up Istio authorization for HTTP/TCP traffic in the mesh
- Configure mutual TLS at mesh, namespace, and workload levels

E. Advanced Scenarios (13%)
- Understand how to onboard non-kubernetes workloads to the mesh
- Troubleshoot configuration issues

Topics not covered:
- Istio Ambient Mode
- Observability tools integrated with Istio such as Kiali, Grafana, and Prometheus

## How to study?

documentation
- istio.io/latest/docs

slack
- cloud-native.slack.com > istio-exam-study-group
- istio.slack.com

some resources
- https://www.udemy.com/course/pe-lf-ica
- https://github.com/isaac88/istio-certified-associate-ica-exam
- https://killercoda.com/ica

## References

- https://www.udemy.com/course/istio-hands-on-for-kubernetes/
- https://www.youtube.com/watch?v=m0GjtrCVSdI
- https://docs.linuxfoundation.org/tc-docs/certification/frequently-asked-questions-ica
- https://medium.com/@arivermar/exploring-the-basics-of-istio-traffic-management-cee13f0817c2
- https://medium.com/@arivermar/demistifying-istio-gateways-762d37070431

---

### tips

#### 1. ⏱️ Time Management
- For parts that require searching, **prepare keywords or references** in advance to find things quickly.
- Bookmark frequently used **Istio documentation** and use `Ctrl + F` to locate sections quickly.
- e.g.) **VirtualService Reference**  
  https://istio.io/latest/docs/reference/config/networking/virtual-service/  
  → Use `Ctrl + F` to search for keywords like `version: v1`

#### 2. 🛠️ kubectl Usage Tips
- Always create resources by **writing YAML manifests and applying them**.
- Use **VS Code** for easier YAML editing and validation.

#### 3. 📦 Istio Resource Versions and Specs

- Current Istio version: **1.18.2**
- It's generally fine to refer to the **latest** documentation for `spec` fields.
- However, note that `apiVersion` often differs:
  - Latest Documentation may use: `networking.istio.io/v1`
  - In practice: you often need to use **`networking.istio.io/v1beta1`** depending on the problem requirements.

#### 4. ⚠️ Easy-to-Miss Resources
Make sure you're familiar with the concept of:

- `Sidecar`
- `WorkloadGroup`
- `WorkloadEntry`

#### 5. 🌐 Cluster Context & Namespace Switching
- Each problem might involve **switching Kubernetes cluster context**, so don't overlook this.
- Namespace may vary between problems — **always double-check the namespace** before applying or analyzing resources.

#### 6. 🧠 Use Fully Qualified Domain Names (FQDN)
- When writing the `host` field, **use full Kubernetes DNS-based FQDN** whenever possible.
- ❌ `sleep.default` ✅ `sleep.default.svc.cluster.local`

#### 7. Useful commands

##### ✔️ Analyze Istio config in a namespace
```bash
istioctl analyze -n default
```

##### ✔️ Validate resource syntax
```bash
istioctl validate -f a.yaml
```

#### 8. 📸 Exam Environment Setup
- Prepare a high-quality webcam, neat workspace, and valid passport or ID.
- Proctors can be strict, so test your exam environment ahead of time if possible.
