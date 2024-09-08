---
url: https://istio.io/latest/docs/overview/
---
## What is Istio?

- https://istio.io/latest/docs/overview/what-is-istio/

> [!NOTE] What is Istio?
> Istio is an open source service mesh that layers transparently onto existing distributed applications.

Istio 는 아래와 기능을 제공함

- `secure communication` - 클러스터 내의 service-to-service 통신을 secure 한다.
- `automatic loadbalancing` - HTTP, gRPC, WebSocket, TCP traffic
- Fine-grained control of traffic behavior with
	- rouching rules
	- retries
	- failovers
	- and fault injection
- Access controls, Rate Limits and quotas
- Observation - metric, logs, traces

### How it works

- Istio 는 모든 네트워크 트래픽을 intercept 하는 proxy 레이어를 통해 동작
- **`Control Plane`** 은 설정/환경/룰 이 변함에 따라 동적으로 proxy servers 를 제어
- **`Data plane`** 은 service 간의 통신

## Why choose Istio?

- https://istio.io/latest/docs/overview/why-choose-istio/

Istio 는 2017년 런칭하여 `sidecar-based service mesh` 라는 개념을 주도하였음.
프로젝트는 시작과 동시에, Service-Mesh 라는 개념을 정의하는것을 하였습니다. 이 개념
- Standards-based mutual TLS for zero-trust networking
- smark traffic routing
- oberservability - metrics,logs and tracing
을 포함

그 이후로, 이 프로젝트는 
- 멀티 클러스터 및 멀티 네트워크 토폴로지, 
- WebAssembly를 통한 확장성, 
- Kubernetes Gateway API 개발, 
- 그리고 애플리케이션 개발자들로부터 메시 인프라를 분리하는 앰비언트 모드 등 
메시 분야에서의 발전을 이끌어 옴

### Istio 👍 

1. Simple and powerful
2. The Envoy proxy
3. Community
4. Packages

## Dataplane modes - Sidecar or ambient?

- https://istio.io/latest/docs/overview/dataplane-modes/

Istio service mesh 는 논리적으로 `data plane`과 `control plane` 으로 나뉨

![[istio-service-mesh.excalidraw|800]]

`data plane` - proxies 의 집합
`control plane` - data plane 의 proxies 를 제어하고 관리한다.

Istio 는 두가지 모드의 data plane 을 제공합니다.

**Sidecar mode** - 클러스터내의 모든 파드에 Envoy Proxy 를 배포하는 방식
**Ambient mode** - 노드 별 `Layer 4 Proxy`/ 선택적으로 Layer 7 기능을 위해 `ns 별 envoy proxy` 를 이용하는 방식

두 모드는 서로 호환 가능하고, 특정 네임스페이스나 워크로드를 각 모드에 선택적으로 넣을 수 있음.

### Sidecar mode (stable)

- 2017 첫 릴리즈 부터 존재했으며 다양한 환경에서 동작이 증명됨
- 직관적으로 이해됨. 하지만 비용이 꽤나 필요함
	- 배포되는 모든 애플리케이션은 sidecar 로써 Envoy proxy 를 주입해야함.
	- L4, L7 모두 proxy 할 수 있음

### Ambient mode (beta)

- 2022 년에 런칭되었으며, sidecar mode 의 단점을 극복하기 위해 도입됨.
- Istio 1.22 에 와서는 단일 클러스터 사용환견에서 production-ready 라고 평가됨 현시점 가장 최신버전 (1.22.4)

모든 트래픽은 레이어 4 전용 노드 프록시를 통해 프록시됨. 
애플리케이션은 레이어 7 기능을 얻기 위해 Envoy 프록시를 통한 라우팅을 선택할 수 있음


