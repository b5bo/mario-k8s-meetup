# mario 배포
<br />

### mario pod 생성
```sh
cat <<EOT> 2pod.yaml
apiVersion: v1
kind: Pod
metadata:
  name: mario1
  labels:
    app: mario
spec:
  nodeName: k8s-w1
  containers:
  - name: container
    image: traefik/whoami
  terminationGracePeriodSeconds: 0
---
apiVersion: v1
kind: Pod
metadata:
  name: mario2
  labels:
    app: mario
spec:
  nodeName: k8s-w2
  containers:
  - name: container
    image: traefik/whoami
  terminationGracePeriodSeconds: 0
EOT
```

<br />

### 생성
```sh
kubectl apply -f 2pod.yaml
```

<br />

### 확인
```sh
kubectl get pod
```