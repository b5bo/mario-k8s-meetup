# istio 설치

<br />

### istioctl 설치
```sh
curl -L https://istio.io/downloadIstio | sh -
ISTIO_VERSION=1.13.2
cp istio-$ISTIO_VERSION/bin/istioctl /usr/bin/istioctl
istioctl operator init
```

<br />

### init : istio-operator namespace 생성, istio-operator deployment 생성
```sh
istioctl operator init
```

<br />

### demo profile 생성
```sh
kubectl apply -f - <<EOF
apiVersion: install.istio.io/v1alpha1
kind: IstioOperator
metadata:
  namespace: istio-system
  name: example-istiocontrolplane
spec:
  profile: demo
EOF
```

<br />

### 버전 확인
```sh
istioctl version
```

<br />

### Auto Injection with namespace label : 해당 namespace에 생성되는 모든 pod들은 istio sidecar가 자동으로 injection 된다.
```sh
kubectl label ns default istio-injection=enab
```

<br />

### istio-ingressgateway 의 svc 설정 변경
- LoadBalancer type 을 굳이 NodePort 로 변경하지 않아도 되지만, 깔끔한 보기를 위해 설정
```sh
kubectl patch svc -n istio-system istio-ingressgateway -p '{"spec":{"type":"NodePort"}}'
kubectl patch svc -n istio-system istio-ingressgateway -p '{"spec":{"externalTrafficPolicy":"Local"}}'
```

<br />

### istio-ingressgateway 의 envoy 버전 확인
```sh
kubectl exec -it deploy/istio-ingressgateway -n istio-system -c istio-proxy -- envoy --version
```