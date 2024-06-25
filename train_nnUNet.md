1. Installation:
https://github.com/MIC-DKFZ/nnUNet/blob/master/documentation/installation_instructions.md
3. Dataset conversion:
https://github.com/MIC-DKFZ/nnUNet/blob/master/nnunetv2/dataset_conversion/Dataset027_ACDC.py#L6
4. Verify the integrity of data
https://github.com/MIC-DKFZ/nnUNet/blob/master/documentation/how_to_use_nnunet.md#model-training
```
nnUNet_raw="../../../Dataset/nnUNet_raw" nnUNet_preprocessed="../../../Dataset/nnUNet_preprocessed" nnUNet_results="../../../Dataset/nnUNet_results" nnUNetv2_plan_and_preprocess -d 1 --verify_dataset_integrity
```
3. Perform training 
```
nnUNet_raw="../../../Dataset/nnUNet_raw" nnUNet_preprocessed="../../../Dataset/nnUNet_preprocessed" nnUNet_results="../../../Dataset/nnUNet_results"  CUDA_VISIBLE_DEVICES=0 nnUNetv2_train Dataset001_CAMUS 2d 0 --npz
```
4. 
