## Find who is running a process
First find the PID (i.e. 2415343) using nvidia-smi
```
ps -u -p PID
```

## Watch GPU process
Refresh nvidia-smi every 0.1 seconds
```
watch -n 0.1 nvidia-smi
```
