# Volume Snapshots - PostgreSQL

### Apply the spec
`master $ kubectl create -f px-snap.yaml`

### Drop the Postgres database
Exec into the pod
`master $ kubectl exec -it <postgres-pod> bash`

```bash

$ psql
drop database pxdemo;
\l
\q
exit
exit
```

### Scale down the postgres deployment and verify
```bash
master $ kubectl scale --replicas=0 deployment/postgres
master $ kubectl get pods
```

### Get the snap and volume IDs
`node01 $ pxctl v l`

### Restore to the original PVC with the CLI
`node01 $ pxctl volume restore -s <snap ID> <volume ID>`

### Scale the deployment back up to 1
```bash
master $ kubectl scale --replicas=1 deployment/postgres
master $ kubectl get pods
```

### Verify data
`master $ kubectl exec -it <postgres-pod> bash`

```bash

psql pxdemo

\dt

select count(*) from pgbench_accounts;

 count  
---------
 5000000
(1 row)
```

### Apply the restore spec
`master $ kubectl create -f px-snap-pvc.yaml`

### View the created PVCs
`master $ kubectl get pvc`

### Apply the spec
`master $ kubectl apply -f postgres-app-restore.yaml`

### Wait for the pod to come up
`master $ watch kubectl get pods`

### Check the data is restored
`master $ kubectl exec -it postgres-snap-<id> bash`

```bash

$ psql pxdemo
# \dt
# select count(*) from pgbench_accounts;
# \q
# exit
# exit
```
