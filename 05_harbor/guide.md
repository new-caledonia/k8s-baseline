## 설치

```
> kubectl create ns harbor
> helm upgrade -i -n harbor harbor bitnami/harbor -f values.yaml
```

## Dashboard

1. 작성된 ingressroute.yaml 파일 배포
```
> kubectl apply -f ./portal/ingressroute.yaml
```

2. harbor.example.com 에서 harbor portal 접속
