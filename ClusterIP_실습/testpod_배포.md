# TestPod 배포
<br />

### 클라이언트(TestPod) 생성
```sh
cat <<EOT> netpod.yaml
apiVersion: v1
kind: Pod
metadata:
  name: service-test
spec:
  restartPolicy: Never
  containers:
  - name: test-client
    image: alpine
    command: ["/bin/sh"]
    args: ["-c", "echo 'GET / HTTP/1.1\r\n\r\n' | nc 10.0.2.2 8080"]
EOT
```

<br />

### 생성
```sh
kubectl apply -f netpod.yaml
```

<br />

### 확인
```sh
kubectl get pod
```