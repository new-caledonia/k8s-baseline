# Argo CD

## Installation

1. Create namespace

    ```
    kubectl create ns argocd
    ```

2. Add helm repo

    ```
    helm repo add argo https://argoproj.github.io/argo-helm
    ```

3. Install argocd as helm

    ```
    helm install argocd argo/argo-cd --namespace argocd

    # If you want HA settings please check link below.
    # https://artifacthub.io/packages/helm/argo/argo-cd#high-availability

    NAME: argocd
    LAST DEPLOYED: Sun Jul 16 09:46:13 2023
    NAMESPACE: argocd
    STATUS: deployed
    REVISION: 1
    TEST SUITE: None
    NOTES:
    In order to access the server UI you have the following options:

    1. kubectl port-forward service/argocd-server -n argocd 8080:443

        and then open the browser on http://localhost:8080 and accept the certificate

    2. enable ingress in the values file `server.ingress.enabled` and either
          - Add the annotation for ssl passthrough: https://argo-cd.readthedocs.io/en/stable/operator-manual/ingress/#option-1-ssl-passthrough
          - Set the `configs.params."server.insecure"` in the values file and terminate SSL at your ingress: https://argo-cd.readthedocs.io/en/stable/operator-manual/ingress/#option-2-multiple-ingress-objects-and-hosts


    After reaching the UI the first time you can login with username: admin and the random password generated during the installation. You can find the password by running:

    kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d

    (You should delete the initial secret afterwards as suggested by the Getting Started Guide: https://argo-cd.readthedocs.io/en/stable/getting_started/#4-login-using-the-cli)
    ```

4. Get admin user password

    ```
    kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d

    ADMINPASSWORD
    ```

5. Edit argocd-server service type as nodeport

    you need to access argocd console. so for now, change service type as nodeport and access it.

    ```
    kubectl edit svc argocd-server -n argocd
    ```

6. Access to argocd console

    check which port is allocated and access to it!

    ```
    kubectl get svc -n argocd
    ```
