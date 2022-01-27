# Depth_pl:

This is a pytorch lightning implementation of **SC-Depth** (V1, V2) for **self-supervised learning of monocular depth from video**.

## Install
```
conda create -n sc_depth_env python=3.7
conda activate sc_depth_env
conda install pytorch==1.7.1 torchvision==0.7.0 cudatoolkit=10.1 -c pytorch
pip install -r requirements.txt
```

## Dataset

We preprocess all existing video datasets to the following general video format for training and testing:

    Dataset
      -Training
        --Scene0000
          ---*.jpg (list of images)
          ---cam.txt (3x3 intrinsic)
          ---depth (a folder containing gt depths, optional for validation)
        --Scene0001
        ...
        train.txt (containing training scene names)
        val.txt (containing validation scene names)
      -Testing
        --color (containg testing images)
        --depth (containg ground truth depths)
You can convert it by yourself (on your own video data) or download our pre-processed standard datasets:

[**[kitti_raw]**](https://1drv.ms/u/s!AiV6XqkxJHE2mUax6F2N-rjAs43R?e=gwn6Zi) [**[nyu]**](https://1drv.ms/u/s!AiV6XqkxJHE2mUUA5hElvhZXnqOn?e=51SIE1)

## Training

We provide "scripts/run_train.sh", which shows how to train on kitti and nyu.

Then you can start a `tensorboard` session in this folder by
```bash
tensorboard --logdir=ckpts/
```
and visualize the training progress by opening [https://localhost:6006](https://localhost:6006) on your browser. 


## Testing

We provide "scripts/run_test.sh", which shows how test on kitti and nyu.



## Inference

We provide "scripts/run_inference.sh", which shows how to save depths (.npy) and visualization results (.jpg). 

A demo is given here. You can put your images in "demo/input/" folder and run
```bash
python inference.py --config configs/v2/nyu.txt \
--input_dir demo/input/ \
--output_dir demo/output/ \
--ckpt_path ckpts/nyu_scv2/version_10/epoch=101-val_loss=0.1580.ckpt \
--save-vis --save-depth
```
and find the results in "demo/output/" folder.

