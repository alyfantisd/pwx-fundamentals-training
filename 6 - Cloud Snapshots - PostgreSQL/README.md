# Cloud Snapshots - PostgreSQL

### Create a backing volume for the objectstore
```
node01 $ pxctl volume create objectstorevol --size 10
Volume successfully created: 539767001152046527
```

### Create the object store with the created volume
```
node01 $ pxctl objectstore create -v objectstorevol
Successfully created object store
```

### Start the object store
```
node01 $ sudo pxctl objectstore enable
Successfully updated object store
```

### Check ObjectStore status
`node01 $ pxctl objectstore status`

### View secrets options
`node01 $ pxctl secrets`

### Login to K8s secrets
`node01 $ pxctl secrets k8s login`

### Create secrets store credentials
```bash
node01 $ pxctl credentials create --provider s3 \
--s3-access-key <access key> \
--s3-secret-key <secret key> \
--s3-region us-east-1 \
--s3-endpoint node01:9010 \
--s3-disable-ssl
```
### Check credentials exist
`node01 $ pxctl credentials list`

### Validate credentials
`node01 $ pxctl credentials validate --uuid <UUID>`

### Get UUID of original Postgres snapshot
`node01 $ pxctl volume list`

### Backup this snapshot to the ObjectStore
`node01 $ pxctl cloudsnap backup <snapshot volume ID>`

### Check the backup completes
`node01 $ watch pxctl cloudsnap status`

### Delete the local snapshot
```
node01 $ pxctl volume list
node01 $ pxctl volume delete <snapshot volume ID>
```

### Retrieve the cloudsnap ID
`node01 $ pxctl cloudsnap list`

### Restore the snapshot
`node01 $ pxctl cloudsnap restore --snap <snap ID>`

