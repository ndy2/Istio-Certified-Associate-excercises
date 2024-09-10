## AS-IS

deploy 를 이용한 canary

versioned app graph
![[Pasted image 20240910080040.png]]

label 에 version 을 추가하면 보인다.

![[Pasted image 20240910080526.png]]


service 의 wigthed routing

![[Pasted image 20240910080946.png]]


![[Pasted image 20240910081021.png]]


![[Pasted image 20240910081100.png]]


## VirtualService

- a routing configuration
- custom routing something like that


```yaml
apiVersion: networking.istio.io/v1beta1
kind: VirtualService
metadata:
  # "Just" a name for this virtualservice
  # name: a-set-of-routing-rules-we-can-call-this-anything
  name: fleetman-staff-service 
  namespace: default
spec:
  hosts:
    # The Service DNS (i.e. the regular K8S service) name
    # that we're applying routing rules to
    - fleetman-staff-service.default.svc.cluster.local
  http:
  - route:
    - destination:
        # The Target DNS name
        host: fleetman-staff-service.default.svc.cluster.local
        # From Destination Rule!
        subset: safe
      weight: 0
    - destination:
        # The Target DNS name
        host: fleetman-staff-service.default.svc.cluster.local
        # From Destination Rule!
        subset: risky
      weight: 100
```

K8s Service - for service discovery

![[regular-k8s-service.excalidraw]]


Virtual Service - for configuring proxies

![[whereis-virtual-service.excalidraw]]


## DestinationRule

```yaml
apiVersion: networking.istio.io/v1beta1
kind: DestinationRule
metadata:
  name: fleetman-staff-service
  namespace: default
spec:
  host: fleetman-staff-service.default.svc.cluster.local
  trafficPolicy: ~
  subsets:
  - labels:
      version: safe
    name: safe
  - labels:
      version: risky
    name: risky
```