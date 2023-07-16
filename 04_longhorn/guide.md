## 설치

```
> kubectl create ns longhorn
> helm upgrade -i -n longhorn longhorn longhorn/longhorn -f values.yaml
```

## UI 접근


1. UI에 접근할 때 사용할 유저의 정보를 secret으로 설정.
```
# 아래의 명령어로 base64로 인코딩된 인증 정보를 추출합니다.
> htpasswd -nb USERNAME PASSWORD | openssl base64

# secret-ui.yaml과 같이 Opaque 타입의 secret으로 저장합니다.
```

2. Ingress, Middleware 작성
https://doc.traefik.io/traefik-enterprise/v2.0/operating/dashboard/
를 참고하여 ingress.yaml와 middleware.yaml을 작성합니다.
route의 match 부분은 접속할 Endpoint를 가리키므로 잘 확인하고 설정합니다.

3. 작성된 service, ingress yaml 파일 배포
```
> kubectl apply -f ./ui
```

위의 과정을 거치면 ./ui/ingress.yaml에서 match에 지정한 host로 접근시 dashboard에 접근할 수 있게됩니다.
