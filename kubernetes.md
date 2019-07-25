### Fazer uma requisição na API do Kubernetes e trazer informações dos deployments realizando o parse do JSON com o ```jq```

```curl -Sks -u username:password \
   https://k8sapi.example.com/apis/apps/v1/deployments | \
   jq -r '[.items[] | {name:.metadata.name, live: .spec.template.spec.containers[].livenessProbe.initialDelaySeconds }]'
```


### Instalando HELM

#### Fazendo o download do script do helm
curl -L https://git.io/get_helm.sh | bash


#### yaml para criação das accounts do helm
apiVersion: v1
kind: ServiceAccount
metadata:
  name: tiller
  namespace: kube-system
---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: tiller
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: cluster-admin
subjects:
  - kind: ServiceAccount
    name: tiller
    namespace: kube-system

#### Aplicando o yaml
kubectl apply -f helm-rbac.yaml

#### Inicializando o helm no cluster
helm init --service-account=tiller --history-max 300

#### Fazendo deploy de um nginx-ingress simples
helm install stable/nginx-ingress --name nginx-ingress




