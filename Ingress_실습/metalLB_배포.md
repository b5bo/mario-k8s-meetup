# Service(LoadBalancer) 사용을 위해서 metalLB를 배포

<br />

### 간단하게 manifests 로 설치
```sh
kubectl apply -f https://raw.githubusercontent.com/metallb/metallb/v0.12.1/manifests/namespace.yaml
kubectl apply -f https://raw.githubusercontent.com/metallb/metallb/v0.12.1/manifests/metallb.yaml
```

<br />

### 확인
```sh
kubectl get all -n metallb-system
kubectl get pod -n metallb-system -o wide
```

<br />

### configmap 생성
```sh
cat <<EOF | kubectl create -f -
apiVersion: v1
kind: ConfigMap
metadata:
  namespace: metallb-system
  name: config
data:
  config: |
    address-pools:
    - name: default
      protocol: layer2
      addresses:
      - 192.168.10.200-192.168.10.210
EOF
```

<br />

### configmap 확인
```sh
kubectl get all -n metallb-system
```