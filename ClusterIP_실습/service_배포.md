# service 배포
<br />

### service(ClusterIP) 생성
```sh
cat <<EOT> svc-clusterip.yaml
apiVersion: v1
kind: Service
metadata:
  name: svc-clusterip
spec:
  ports:
    - name: svc-webport
      port: 9000
      targetPort: 80
  selector:
    app: mario
  type: ClusterIP
EOT
```

<br />

### 생성
```sh
kubectl apply -f svc-clusterip.yaml
```

<br />

### 확인
```sh
kubectl get svc,ep
```