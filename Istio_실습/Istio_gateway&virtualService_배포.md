# Istio Gateway/VirtualService 설정
<br />

### Istio Gateway/VirtualService 생성
```sh
cat <<EOF | kubectl create -f -
apiVersion: networking.istio.io/v1alpha3
kind: Gateway
metadata:
  name: bo-gateway
spec:
  selector:
    istio: ingressgateway
  servers:
  - port:
      number: 80
      name: http
      protocol: HTTP
    hosts:
    - "*"
---
apiVersion: networking.istio.io/v1alpha3
kind: VirtualService
metadata:
  name: mario-service
spec:
  hosts:
  - "$MYDOMAIN"
  gateways:
  - bo-gateway
  http:
  - route:
    - destination:
        port:
          number: 80
        host: mario
EOF
```

<br />

### 확인
```sh
kubectl get gw,vs
```