# Encrypted Volumes

### Create secret for cluster wide encryption key
`master $ kubectl -n portworx create secret generic px-vol-encryption --from-literal=cluster-wide-secret-key=Il0v3Portw0rX`

### Validate the secret exists
`master $ kubectl get secrets -n portworx | grep vol`

### Give Portworx the cluster wide key
`node01 $ pxctl secrets set-cluster-key --secret cluster-wide-secret-key`

### View the Secure Storage Class
`master $ cat px-secure-sc.yaml`

### Apply the Storage Class
`master $ kubectl apply -f px-secure-sc.yaml`

### Create the PVC
`master $ kubectl apply -f px-secure-pvc.yaml`

### Validate the volume is encrypted
`node01 $ pxctl volume list`

### Apply the standard Storage Class
`master $ kubectl apply -f px-sc.yaml`

### Create the new secret for the PVC encryption
`master $ kubectl -n portworx create secret generic volume-secrets --from-literal=secure-pvc=SuperSecur3Key`

### Verify the secret exists
`master $ kubectl get secrets -n portworx`

### View the secure PVC extra parameters
`master $ cat px-secure-pvc2.yaml`

### Apply the secure PVC
`master $ kubectl apply -f px-secure-pvc2.yaml`

### Validate the volume is encrypted
`node01 $ pxctl volume list`

### Store the PVC ID in an env variable
`node01 $ PX_VOL=<secure pvc>`

### Attempt to access the PVC
`node01 $ pxctl host attach $PX_VOL`

