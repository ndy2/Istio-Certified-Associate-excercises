## Control Plane

```bash
deukyun@deukyun-adsl:~$ k get po -n istio-system
NAME                                   READY   STATUS    RESTARTS   AGE
grafana-949c6db6-dzxk9                 1/1     Running   0          61s
istio-egressgateway-774fcbcf58-w9t54   1/1     Running   0          61s
istio-ingressgateway-99b74c4dd-bkbnd   1/1     Running   0          61s
istiod-6db46967dc-6l7fq                1/1     Running   0          61s
jaeger-59cd78bf84-qtfxh                1/1     Running   0          61s
kiali-54845965d9-jhrnt                 1/1     Running   0          60s
prometheus-8d4d6c6dd-66tx4             2/2     Running   0          61s

```

## Data Plane


![[data-plane.excalidraw|800]]

The Proxies are collectively called the **"Data Plane"** in Istio

application container 만 존재하는 기본 상태

```bash
deukyun@deukyun-adsl:~$ k get po -n default
NAME                                  READY   STATUS    RESTARTS   AGE
api-gateway-6fd64d789c-c8tdm          1/1     Running   0          39m
photo-service-67f67ccc8-s8psf         1/1     Running   0          39m
position-simulator-55497db89f-l2r4m   1/1     Running   0          39m
position-tracker-57d8c9598f-snk6g     1/1     Running   0          39m
staff-service-6bf5d69d56-mvn45        1/1     Running   0          39m
vehicle-telemetry-6c85684cc-tbt8m     1/1     Running   0          39m
webapp-cc9d989d-24q82                 1/1     Running   0          39m

```


```bash
deukyun@deukyun-adsl:~$ k get ns default --show-labels
NAME      STATUS   AGE    LABELS
default   Active   231d   istio-injection=enabled,kubernetes.io/metadata.name=default

```

미리 설치된 pod 에 자동으로 반영 되지는 않는다.

```bash
deukyun@deukyun-adsl:~$ k get po -n default
NAME                                  READY   STATUS    RESTARTS   AGE
api-gateway-6fd64d789c-t5ljj          2/2     Running   0          9s
photo-service-67f67ccc8-s964t         2/2     Running   0          8s
position-simulator-55497db89f-974gp   2/2     Running   0          9s
position-tracker-57d8c9598f-ktxwr     2/2     Running   0          9s
staff-service-6bf5d69d56-cvqd2        2/2     Running   0          8s
vehicle-telemetry-6c85684cc-fd7kw     2/2     Running   0          9s
webapp-cc9d989d-kcptv                 2/2     Running   0          9s

```

application 을 다시 배포하면 -> sidecar container 가 주입되었다.