## when globus is not working
https://docs.ycrc.yale.edu/clusters-at-yale/access/ssh/#mobaxterm
install mobaxterm on local windows/linux machine and transfer files from there.... Fxxx Globus...

## Yale hpc request an interactive gpu job
```
srun --pty -t 0:10:00 --mem=64G --gpus=v100:1 --partition gpu bash
```
the name of the job is ``bash''
```
srun --pty -t 0:30:00 --mem=64G --gpus=1 --partition gpu bash
```

## check my job queues
```
squeue --me
```

## standard gpu job example (train4d_job1.sh)
```
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
