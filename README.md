# Simultaneous_VO_Depth

An implementation of Simultaneous visual odometry and single-image depth estimation described in **"An Unsupervised Approach for Simultaneous Visual Odometry and Single Image Depth Estimation" 2022 IJCNN**. This code can achieve better results than ori paper.

## Getting Started

### Train
```
-Mono:
nohup python train.py --data_path /home/depth_merge_mono_stereo/kitti_data --log_dir logs/  --model_name mono_depth_clue   --scheduler_step_size 5 --split eigen_zhou --disparity_smoothness 0  >mono.log &
```

```
-Stereo:
nohup python train.py --data_path /home/depth_merge_mono_stereo/kitti_data --log_dir logs/  --model_name stereo_depth_clue   --frame_ids 0  --use_stereo  --scheduler_step_size 5 --split eigen_full --disparity_smoothness 0 >stereo.log &
```

```
-Mono+Stereo model:
python train.py --data_path /home/depth_merge_mono_stereo/kitti_data --log_dir logs/  --model_name mono_depth_clue   --scheduler_step_size 5  --disparity_smoothness 0

python train.py --data_path /home/depth_merge_mono_stereo/kitti_data --log_dir logs/  --model_name mono_stereo_clue   --frame_ids 0 -1 1  --use_stereo  --scheduler_step_size 5  --disparity_smoothness 0  --load_weights_folder /home/depth_merge_mono_stereo/logs/mono_depth_clue/models/weights_19
```

### Evaluate
```
-Mono:
python evaluate_depth.py --data_path /home/depth_merge_mono_stereo/kitti_data  --load_weights_folder /home/depth_merge_mono_stereo/logs/mono_depth_clue/models/weights_19   --eval_mono
-> Computing predictions with size 640x192
-> Evaluating

abs_rel |   sq_rel |     rmse | rmse_log |       a1 |       a2 |       a3 |
0.119  &   0.936  &   4.867  &   0.194  &   0.870  &   0.957  &   0.981  \\
```

```
-Stereo:
python evaluate_depth.py --data_path /home/depth_merge_mono_stereo/kitti_data  --load_weights_folder /home/depth_merge_mono_stereo/logs/stereo_depth_clue/models/weights_19   --eval_stereo
-> Computing predictions with size 640x192
-> Evaluating

abs_rel |   sq_rel |     rmse | rmse_log |       a1 |       a2 |       a3 |
0.112  &   0.888  &   4.938  &   0.206  &   0.864  &   0.950  &   0.976  \\
```

```
-Mono+Stereo
python evaluate_depth.py --data_path /home/depth_merge_mono_stereo/kitti_data  --load_weights_folder /home/depth_merge_mono_stereo/logs/mono_stereo_clue/models/weights_19   --eval_mono
-> Computing predictions with size 640x192
-> Evaluating

abs_rel |   sq_rel |     rmse | rmse_log |       a1 |       a2 |       a3 |
0.108  &   0.777  &   4.643  &   0.185  &   0.881  &   0.961  &   0.983  \\
```

## Model path
Model checkpoints can be found here:
[Models](https://mega.nz/folder/Td1GiChL#G8jmF5E5PDgjP2X-7Zm_sA)

## Acknowledge

This implementation borrows codes from open-source Monodepth2, if you find this is useful, consider cite:

```
@inproceedings{lu2022unsupervised,
  title={An Unsupervised Approach for Simultaneous Visual Odometry and Single Image Depth Estimation},
  author={Lu, Yawen and Lu, Guoyu},
  booktitle={2022 International Joint Conference on Neural Networks (IJCNN)},
  pages={01--08},
  year={2022},
  organization={IEEE}
}
```

```
@inproceedings{godard2019digging,
  title={Digging into self-supervised monocular depth estimation},
  author={Godard, Cl{\'e}ment and Mac Aodha, Oisin and Firman, Michael and Brostow, Gabriel J},
  booktitle={Proceedings of the IEEE/CVF international conference on computer vision},
  pages={3828--3838},
  year={2019}
}
```
