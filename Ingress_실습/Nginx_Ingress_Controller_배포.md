# Nginx Ingress Controller 배포 시 Service(LoadBalancer) 타입을 사용

<br />

### nginx ingress controller v1.1.1 설치 (control plane에 설치)
```sh
https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.1.1/deploy/static/provider/cloud/deploy.yaml
```

<br />

### 확인
```sh
kubectl get all -n ingress-nginx
kubectl get svc -n ingress-nginx ingress-nginx-controller
```

<br />

### 기본 nginx conf 파일 확인
```sh
kubectl exec deploy/ingress-nginx-controller -n ingress-nginx -it -- cat /etc/nginx/nginx.conf
```

<br />

### ingress-nginx-controller NodePort(HTTP 접속용) 변수 지정
```sh
export IngHttp=$(kubectl get service -n ingress-nginx ingress-nginx-controller -o jsonpath='{.spec.ports[0].nodePort}')
echo $IngHttp
```

<br />

### ingress-nginx-controller NodePort(HTTP 접속용) 변수 지정
```sh
export IngHttps=$(kubectl get service -n ingress-nginx ingress-nginx-controller -o jsonpath='{.spec.ports[1].nodePort}')
echo $IngHttps
```

<br />

### Service(LoadBalancer) 타입 설정
```sh
kubectl -n ingress-nginx patch svc/ingress-nginx-controller -p '{"spec": {"type": "LoadBalancer"}}'
```

<br />

### 확인
```sh
kubectl get all -n ingress-nginx
kubectl get svc -n ingress-nginx ingress-nginx-controller
```
