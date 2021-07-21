# Expose ArgoCD port
```
kubectl -n argocd patch svc argocd-server -p '{"spec": {"type": "NodePort"}}'
```{{execute}}

This will allocate a random port on the node for the argocd server.

# Get the password for the admin user
```
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d | echo
```{{execute}}

# Get the port
```
arogcd_port=$(kubectl -n argocd get services argocd-server -o jsonpath='{.spec.ports[?(@.name=="http")].nodePort}')
echo "https://[[HOST_SUBDOMAIN]]-${arogcd_port}-[[KATACODA_HOST]].environments.katacoda.com/"
```{{execute}}
