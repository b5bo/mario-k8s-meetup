# mario 배포
<br />

### mario deployment와 service 생성
```sh
cat <<EOF | kubectl create -f -
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mario
  labels:
    app: mario
spec:
  replicas: 1
  selector:
    matchLabels:
      app: mario
  template:
    metadata:
      labels:
        app: mario
    spec:
      containers:
      - name: mario
        image: pengbai/docker-supermario
---
apiVersion: v1
kind: Service
metadata:
   name: mario
spec:
  selector:
    app: mario
  ports:
  - port: 80
    protocol: TCP
    targetPort: 8080
type: NodePort
EOF
```

<br />

### 확인
```sh
kubectl get deploy,pod -o wide
kubectl get node -o wide
kubectl get endpoints mario
```

<br />

### nodeport확인
```sh
kubectl get svc mario
kubectl describe svc mario
```