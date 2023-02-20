# Tips of how to use wandb for version control
## Configs
```
import wandb
# all your config params
run = wandb.init(
    # set the wandb project where this run will be logged
    project="your project name created on wandb",
    
    # track hyperparameters and run metadata
    config={
    "learning_rate": args.lr,
    "architecture": "UNet",
    "dataset": args.dataset,
    "epochs": args.epochs,
    "batch_size": args.batch_size,
    "steps_per_epoch": args.steps_per_epoch,
    "bidir": args.bidir,
    "enc_nf": enc_nf,
    "dec_nf": dec_nf,
    "image-loss": args.image_loss,
    "loss_weights": weights
    }
)
```

## Model version control
https://wandb.ai/wandb/common-ml-errors/reports/How-to-Save-and-Load-Models-in-PyTorch--VmlldzozMjg0MTE
https://docs.wandb.ai/guides/data-and-model-versioning/model-versioning
```
artifact = wandb.Artifact('model_name', type='model')
artifact.add_file(os.path.join(model_dir, '%04d.pt' % epoch)) # add your model file to wandb
run.log_artifact(artifact) # upload your file to cloud
```

## Loss & Image logging
```
src_im = wandb.Image(inputs[0].cpu().detach().numpy()[0, 0][:, :, 32])
tgt_im = wandb.Image(inputs[1].cpu().detach().numpy()[0, 0][:, :, 32])
 
wandb.log({"loss": np.mean(epoch_total_loss), "src_im": src_im, "tgt_im": tgt_im}) # log using a dict
```
