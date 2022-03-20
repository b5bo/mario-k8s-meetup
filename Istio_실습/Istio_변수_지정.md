# Istio 접속 테스트를 위한 변수 지정
<br />

## k8s-pc, k8s-m 에서 아래 실행

<br />

### istio ingress gw NodePort(HTTP 접속용) 변수 지정
```sh
export IGWHTTP=$(kubectl get service -n istio-system istio-ingressgateway -o jsonpath='{.spec.ports[1].nodePort}')
echo $IGWHTTP
```

<br />

### istio-ingressgateway pod 정보 확인
```sh
export ISTIOINGRSS=$(kubectl get pods -n istio-system -l app=istio-ingressgateway -o jsonpath='{.items[0].metadata.name}')
kubectl get pod -n istio-system $ISTIOINGRSS -owide
```

<br />

### istio-ingressgateway pod가 배치된 node
```sh
export ISTIONODE=$(kubectl get pod -n istio-system $ISTIOINGRSS -o jsonpath={.spec.nodeName})
echo $ISTIONODE
```

<br />

### istio-ingressgateway pod가 배치된 node의 IP
```sh
export ISTIONODEIP=$(kubectl get node $ISTIONODE -o jsonpath={.status.addresses[0].address})
echo $ISTIONODEIP
```

<br />

### /etc/hosts 파일 수정 >> istio-ingressgateway pod가 있는 node의 IP를 지정
```sh
MYDOMAIN=mario.bo.com
echo "$ISTIONODEIP $MYDOMAIN" >> /etc/hosts
```

<br />

### istio ingress gw 접속 테스트 : 아직은 설정이 없어서 접속 실패
```sh
curl -v -s $MYDOMAIN:$IGWHTTP
```
