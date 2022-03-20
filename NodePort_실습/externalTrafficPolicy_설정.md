# externalTrafficPolicy 설정

<br />

### 기본 정보 확인
```sh
kubectl get svc mario -o json | grep 'TrafficPolicy"'
```

<br />

### externalTrafficPolicy: local 설정 변경
```sh
kubectl get svc mario -o yaml | sed -e "s/externalTrafficPolicy: Cluster/externalTrafficPolicy: Local/" | kubectl apply -f -
```

<br />

### externalTrafficPolicy: local 설정 확인
```sh
kubectl get svc mario -o json | grep 'TrafficPolicy"'
```

<br />

## 외부 클라이언트(k8s-pc)에서 실행
<br />

### service(NodePort) 접속 확인 : pod가 존재하지 않는 node로는 접속 실패!, pod가 존재하는 node는 접속 성공 및 client IP 확인!
```sh
NPORT=<service의 NodePort>
NODE1=<node1의 IP주소>
NODE2=<node2의 IP주소>
curl -s --connect-timeout 1 $NODE1:$NPORT
for i in {1..100}; do curl -s --connect-timeout 1 $NODE1:$NPORT | egrep 'Hostname|client_address'; done | sort | uniq -c | sort -nr
curl -s --connect-timeout 1 $NODE2:$NPORT
for i in {1..100}; do curl -s --connect-timeout 1 $NODE2:$NPORT | egrep 'Hostname|client_address'; done | sort | uniq -c | sort -nr
```



<br />

### pod 로그 실시간 확인 (pod에 접속자의 IP가 출력)
```sh
kubetail -l app=mario -f
```
<br />

## 웹 브라우저에서 실행
- 접속 테스트는 vagrant 가 동작하는 **자신의 호스트 PC**에서 **웹브라우저**에서 **접속** 할 것
- 웹 브라우저 접속 시 node의IP:NodePort