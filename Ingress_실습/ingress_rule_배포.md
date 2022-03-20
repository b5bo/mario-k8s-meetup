# ingress(정책) 배포
<br />

### ingress(정책) 생성
```sh
cat <<EOT> ingress.yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: ingress-bo
spec:
  ingressClassName: nginx
  rules:
  - host: "mario.bo.com"
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: mario
            port:
              number: 8080
  - host: "tetris.bo.com"
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: tetris
            port:
              number: 80
EOT
```

<br />

### 배포
```sh
kubectl apply -f ingress.yaml
```

<br />

### 확인
```sh
kubectl get ingress
kubectl describe ingress ingress-bo | sed -n "5, \$p"
```