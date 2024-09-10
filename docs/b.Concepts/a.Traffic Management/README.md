---
url: https://istio.io/latest/docs/concepts/traffic-management/
---
Istio 의 traffic routing rule 은 
- 서비스간의 traffic/API 호출을 쉽게 제어할 수 있도록 합니다.  
	- Istio 는 Circuit breakers, timeouts, and retries 
- A/B testing, canary rollouts, and staged rollout
- out-of-box reliability features


## Introducing Istio traffic management

Istio 가 traffic 을 제어하기 위해서, Istio 는 모든 endpoints 가 어떤 IP 를 가지는 지, 각각 무슨 services 에 속하는지 알아야 합니다. 즉, service registry 를 가져야 합니다. Istio 를 K8s 에서 활용하면 자동으로 istio 는 k8s 의 service 와 endpoint 를 등록합니다.

기본적으로 Istio 가 활용하는 Envoy Proxies 는 Least-requests model 에 기반한 load balancing 을 제공합니다. 램덤으로 두 개의 hosts 를 선택하여 그 중에 더 적은 요청을 받은 hosts 를 선택합니다. 

더 정교한 traffic 제어를 위해서는 Istio’s traffic management API 를 이용해 custom traffic configuration 을 적용할 수 있습니다. 다른 Istio 설정들과 동일하게 api 는 k8s 의 crd 로 관리됩니다.

- virtualservices.networking.istio.io
- destinationrules.networking.istio.io
- gateways.networking.istio.io
- serviceentries.networking.istio.io
- sidecars.networking.istio.io

### Virtual services

- Without virtual services, Envoy distributes traffic using least requests load balancing between all service instances
- With a virtual service, you can specify traffic behavior for one or more hostnames.

```yaml
apiVersion: networking.istio.io/v1
kind: VirtualService
metadata:
  name: reviews
spec:
  ### The hosts field
  ### 이 객체가 “reviews”라는 서비스를 대상으로 트래픽을 제어한다는 뜻
  hosts:
  - reviews
  
  ### Routing rules
  http:
  - match:
    - headers:
        end-user:
          exact: jason
    route:
    - destination:
        host: reviews
        subset: v2
  - route:
    - destination:
        host: reviews
        subset: v3
```


요약:
- end-user 헤더가 jason일 때는 reviews 서비스의 v2로 라우팅됨.
- 그 외의 모든 경우에는 reviews 서비스의 v3로 라우팅됨.

> [!NOTE] Routing rule precedence
> Routing rules are **evaluated in sequential order from top to bottom**

### Destination rules

- https://istio.io/latest/docs/reference/config/networking/destination-rule/

```yaml
apiVersion: networking.istio.io/v1
kind: DestinationRule
metadata:
  name: my-destination-rule
spec:
  ### my-svc: 이 규칙이 적용될 대상 서비스가 my-svc임을 명시함.
  host: my-svc
  
  ### 기본 로드 밸런싱 전략
  trafficPolicy:
    loadBalancer:
      simple: RANDOM
  subsets:
  ### subset v1
  - name: v1
    labels:
      version: v1
  
  ### subset v2
  - name: v2
    labels:
      version: v2
    trafficPolicy:
      loadBalancer:
        simple: ROUND_ROBIN
  
  ### subset v3
  - name: v3
    labels:
      version: v3
```

요약
-  my-svc라는 서비스에 대한 기본 로드 밸런싱 전략은 랜덤(RANDOM)으로 설정됨.
-  v1, v2, v3 버전별로 라벨이 붙어 있고, v2 버전만 로드 밸런싱 전략이 순환(ROUND_ROBIN)으로 설정됨