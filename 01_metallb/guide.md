많은 사람들이 쿠버네티스를 사용하면서 어렵다고 느끼는 요소중 하나는 자신의 서비스를 밖으로 노출시키는 것입니다.
이러한 부분을 빠르고 쉽게 하기 위해서 만들어진 MetalLB에 대해서 알아보도록 하곘습니다.

MetalLB 란?
쿠버네티스를 위한 베어메탈 로드밸런서입니다.

# metallb
```
kubectl apply -f namespace.yaml

helm repo add metallb https://metallb.github.io/metallb

helm repo update

helm upgrade -i -n metallb-system metallb metallb/metallb

kubectl apply -f address-pool.yaml
```

address-pool의 경우, 버전에 따라서 지정 방식이 상이하므로 적용전에 확인이 필요합니다.
여기까지 완료되었을 경우, 
kubectl expose deploy $POD_NAME --port 80 --type LoadBalancer
등의 명령어로 LoadBalancer를 생성하면 EXTERNAL-IP에 address-pool에서 지정한 IP 주소가 할당된 것을 확인할 수 있을것입니다.

