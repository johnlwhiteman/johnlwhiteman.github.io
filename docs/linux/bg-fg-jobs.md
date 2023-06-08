# bg fg jobs

```bash
# Execute a long running job and put it in the background
xload &

# View it in the jobs queue
jobs

# Bring the job back to the foreground
fg %1

# Or kill it
kill %1

# Execute a long running job
sleep 20000

# Suspend it in the background
ctrl+z

# Restart the suspended job and run it in the background
bg
```
