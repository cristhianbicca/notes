### Fazer uma requisição na API do Kubernetes e trazer informações dos deployments realizando o parse do JSON com o ```jq```

```curl -Sks -u username:password \
   https://k8sapi.example.com/apis/apps/v1/deployments | \
   jq -r '[.items[] | {name:.metadata.name, live: .spec.template.spec.containers[].livenessProbe.initialDelaySeconds }]'
```
