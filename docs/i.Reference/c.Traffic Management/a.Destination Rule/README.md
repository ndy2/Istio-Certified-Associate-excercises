---
url: https://istio.io/latest/docs/reference/config/networking/destination-rule/
---
DestionationRule 은 *Routing 이 발생한 이후에*  traffic 에 적용될 정책을 정의함.
- 이는 Load balancing, Connection poll size (from side car) 를 의미

## TrafficPolicy 예시

```yaml
apiVersion: networking.istio.io/v1
kind: DestinationRule
metadata:
  name: bookinfo-ratings
spec:
  host: ratings.prod.svc.cluster.local
  trafficPolicy:
    loadBalancer:
      simple: LEAST_REQUEST
  subsets:
  - name: testversion
    labels:
      version: v3
    trafficPolicy:
      loadBalancer:
        simple: ROUND_ROBIN
```

