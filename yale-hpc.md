## when globus is not working
https://docs.ycrc.yale.edu/clusters-at-yale/access/ssh/#mobaxterm
install mobaxterm on local windows/linux machine and transfer files from there.... Fxxx Globus...

## Track live GPU status
```bash
watch -n 0.1 nvidia-smi
```

## Yale hpc request an interactive gpu job
```bash
srun --pty -t 0:10:00 --mem=64G --gpus=v100:1 --partition gpu_devel bash
```
the name of the job is ``bash''
```
srun --pty -t 0:30:00 --mem=64G --gpus=1 --partition gpu_devel bash
```
request multi-GPU
```
srun --pty -t 0:30:00 --mem=64G --gpus=2 --gpus-per-node 2 --partition gpu_devel bash 
```

## check my job queues
```bash
squeue --me
```

## check submission rules:
```bash
sacctmgr show qos \
  format=Name%-30,MaxJobsPerUser%-15,MaxSubmitJobsPerUser%-20,MaxTRESPU%-30,MaxWall
```

## organize tmux nested jobs
1. constraint: you can only nest two layers on the Yale cluster
2. nest 1: yale_bouchet: manage your compute node, run your `srun` command here
3. nest 2: manage you vllm_server, and parallel processes

## standard gpu job example (train4d_job1.sh)
```bash
#!/bin/bash
#SBATCH --job-name=train4d_job1
#SBATCH --out="./slurm_out/slurm-%j.out"
#SBATCH --time=04:00:00
#SBATCH --gpus=v100:1
#SBATCH --mem=64G
#SBATCH --partition gpu

pwd
nvidia-smi
module load miniconda
source activate pytorch_env
python train4d.py --ncrop 4 --losstype l2 --dataset ACDC17_norm_z12_4d --lmbd 0.0001 
```

## cheatsheet
https://research.computing.yale.edu/sites/default/files/files/cheatsheet.pdf
