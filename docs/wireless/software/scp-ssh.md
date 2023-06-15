# SCP/SSH Commands

## SCP

```bash
# Local path to remote path ... remote path can be a directory too
scp $LOCAL_PATH $USER@$IP:$REMOTE_PATH

# Remote path to local path ... local path can be a directory too
scp $USER@$IP:$REMOTE_PATH $LOCAL_PATH
```

## SSH

```bash
ssh $USER@$IP
```