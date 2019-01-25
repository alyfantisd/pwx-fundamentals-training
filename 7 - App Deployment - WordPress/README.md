# App Deployment - WordPress

### Apply both specs
```
master $ kubectl apply -f mysql-vol.yaml
master $ kubectl apply -f wp-vol.yaml
```

### Verify creation
```
master $ kubectl get sc
master $ kubectl get pvc
```

### Apply MySQL deployment
`kubectl apply -f mysql-deploy.yaml`

### Apply WordPress deployment
`kubectl apply -f wp-deploy.yaml`

### Get WordPress Pod ID
`kubectl get pods`

### Replace WordPress theme header file
`master $ kubectl exec <pod> -- curl -Lo wp-content/themes/twentyfifteen/header.php https://git.io/fAfod`

### Scale WordPress deployment
`master $ kubectl scale --replicas=5 deployment/wordpress`
