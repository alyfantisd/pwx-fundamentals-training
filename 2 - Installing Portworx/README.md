# Installing Portworx

### Portworx spec generator
https://install.portworx.com

### Values for the install generator

| Item                         | Value                 |
| -----------------------------|:---------------------:|
| Kubernetes Version           | 1.16.2                |
| ETCD                         | Built In              |
| Storage (existing)           | /dev/nvme1n1          |
| Data and Mngmt interface     | ens5                  |
| Enable Stork                 | Yes                   |
| Secrets type                 | Kubernetes            |
| Cluster name                 | px-demo               |

### Generated command
```
[root@master-1 ~]# kubectl apply -f 'https://install.portworx.com/2.2?mc=false&kbver=1.16.2&b=true&c=px-demo&stork=true&lh=true&st=k8s'
```

### Check Portworx pods are running
`[root@master-1 ~]# watch kubectl get pods -n kube-system -l name=portworx -o wide`

### View the config file
`[root@node-1-1 ~]# cat /etc/pwx/config.json`
