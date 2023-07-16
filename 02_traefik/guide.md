## 설치

```
> kubectl create ns traefik
> helm upgrade -i -n traefik traefik traefik/traefik -f values.yaml

# values.yaml에서 providers > kubernetesCRD > allowCrossNamespace 옵션이 존재하는데, 이 값이 false면 다른 namespace에 접근할 수 없습니다.
```

## Dashboard 접근

1. Dashboard에 접근할 때 사용할 유저의 정보를 secret으로 설정.
```
# 아래의 명령어로 base64로 인코딩된 인증 정보를 추출합니다.
> htpasswd -nb USERNAME PASSWORD | openssl base64

# secret-dashboard.yaml과 같이 Opaque 타입의 secret으로 저장합니다.
```

2. Ingress, Middleware 작성
https://doc.traefik.io/traefik-enterprise/v2.0/operating/dashboard/
를 참고하여 ingress.yaml와 middleware.yaml을 작성합니다.
route의 match 부분은 접속할 Endpoint를 가리키므로 잘 확인하고 설정합니다.

3. 작성한 yaml 파일을 배포
```
> kubectl apply -f secret-dashboard.yaml
> kubectl apply -f middleware.yaml
> kubectl apply -f ingress.yaml
```

위의 과정을 거치면 ingress에서 match에 지정한 host로 접근시 1번에서 생성한 인증정보를 바탕으로 dashboard에 접근할 수 있게됩니다.
