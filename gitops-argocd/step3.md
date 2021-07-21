# Expose ArgoCD port
```
kubectl -n argocd patch svc argocd-server -p '{"spec": {"type": "NodePort"}}'
```{{execute}}

This will allocate a random port on the node for the argocd server.

# Get the port
```
arogcd_port=$(kubectl -n argocd get services argocd-server -o jsonpath='{.spec.ports[?(@.name=="http")].nodePort}')
echo "https://[[HOST_SUBDOMAIN]]-${arogcd_port}-[[KATACODA_HOST]].environments.katacoda.com/"
```{{execute}}
