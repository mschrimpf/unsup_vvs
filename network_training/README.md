# Prerequisites

Our network training is based on tfutils. 
Please install [tfutils](https://github.com/neuroailab/tfutils) first.
To use tfutils, you need to host a mongodb, please see general instructions about how to do that.
We suggest making the mongodb accessible through port 27007, so you don't need to modify experiment settings.
Due to a conflict in requirements which will not influence this repo, you need to reinstall `tensorflow_gpu==1.15.0` after installing tfutils.

# Scripts for network training

Typical command:
```
python train_combinet_clean.py --gpu [gpu_numbers] --cacheDirPrefix /path/to/model/cache --load_setting_func [set_func_name] --overall_local /path/to/datasets
```

This `overall_local` parameter is used to set the dataset path. 
Please check `utilities/data_path_utils.py` for details. 
If you have set the dataset directories as suggested when preparing the datasets, this is all you need. 
Otherwise, you need to modify contents in `utilities/data_path_utils.py`.

The `set_func_name` parameter should be `script_name.function_name`. Here the `script_name` should be scripts hosted in `exp_settings` folder. `function_name` is the function in the script you want to run.

Certain models may require multiple gpus. To do that, just set `gpu_numbers` as all the gpus you want to use separated by commas. Please use 1 or even number of gpus.

If the training is unexpectedly interrupted, you can just run the same command to resume the training, which should load from the latest saved model.

## Supervised

`set_func_name` should be `supervised.super_res18_s0`, `supervised.super_res18_s1`, `supervised.super_res18_s2`, corresponding to three networks with different initializations.

## Local Aggregation

`set_func_name` should be `la.res18_la_s0`, `la.res18_la_s1`, `la.res18_la_s2`. Due to an implmenetation problem, if your training is interrupted, you need to comment a sentence in the setting before resuming the training, see line 51 of `exp_settings/la.py`.


## SimCLR

SimCLR needs to be trained through preparing ImageNet following instructions in folder `models/simclr` and using TPUs (v3-pod-256 recommended). After preparing the dataset and building TPUs, run scripts `training_bashes/train_res18_in_0.sh`, `training_bashes/train_res18_in_1.sh`, and `training_bashes/train_res18_in_2.sh` in that folder.


## Instance Recognition

`set_func_name` should be `ir.res18_ir_s0`, `ir.res18_ir_s1`, `ir.res18_ir_s2`.


## Relative Position

`set_func_name` should be `rp.res18_rp_s0`, `rp.res18_rp_s1`, `rp.res18_rp_s2`.


## Colorization

`set_func_name` should be `col.res18_col_s0`, `col.res18_col_s1`, `col.res18_col_s2`.


## CPC

`set_func_name` should be `cpc.res18_cpc_s0`, `cpc.res18_cpc_s1`, `cpc.res18_cpc_s2`.


## Auto-Encoder

`set_func_name` should be `ae.res18_ae_s0`, `ae.res18_ae_s1`, `ae.res18_ae_s2`.
