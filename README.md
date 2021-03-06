# LSVO
LS-VO code repository

# Introduction

This repository contains the source code of the LS-VO approach described in the article "LS-VO: Learning Dense Optical Subspace for Robust Visual Odometry Estimation" by Gabriele Costante and Thomas A. Ciarfuglia

If you use LSVO in an academic work, please cite the Robotics and Autonomous Letter (RAL) version of the paper which will be available soon.

# Environment Setup

The LS-VO code has thee following dependencies: 
* Keras framework https://keras.io/ 
* Tensorflow as the backend framework for Keras https://www.tensorflow.org/. 
* Python 3.5. 
* The Robotic Toolbox (already provided in this repository) https://github.com/petercorke/robotics-toolbox-python
* The h2py library to process HDF5 files.

We suggest to create a virtual environment to install the project dependencies:
    
    #Install python 3 and virtualenv
    sudo apt-get install python3-pip python3-dev python-virtualenv
    
    #Create a virtualenv directory
    virtualenv --system-site-packages -p python3 lsvo-environment
    
    #Activate the ennvironment on the current shell
    source ~/lsvo-environment/bin/activate
    
    #Install tensorflow with GPU support
    pip3 install --upgrade tensorflow-gpu
    
    #Install Keras
    pip3 install keras
    
    #Install h5py
    pip3 install h5py
    
    #clone this repository 
    git clone https://github.com/isarlab-department-engineering/LSVO.git
   
# Dataset and model weights

We provide the optical flow (currently only the Flownet-based ones) computed for the test sequences of each dataset. The archives contain the optical flow for the d1 tests (no downsampling), the d2 test (sub-sampled sequences) and the d2+blur tests (sub-sampled and blurred).
We also provide the weights of the ST-VO(Flow) and the LS-VO(Flow) architectures for all the experiments in the paper.
You can download them with the following commands:

    #Download the optical flow for the KITTI test sequences (08, 09, 10)
    wget http://sira.diei.unipg.it/supplementary/lsvo_ral2018/KITTI_RGB_dataset.tar.gz
    
    #Download the optical flow for the Malaga test sequences (02, 03, 09)
    wget http://sira.diei.unipg.it/supplementary/lsvo_ral2018/Malaga_dataset.tar.gz
    
    #Download the weights files
    wget http://sira.diei.unipg.it/supplementary/lsvo_ral2018/weights.tar.gz
    
After unpacking them change the 'data_set_dir' argument and the 'weights_dir' argument in the config.py file to match the directories where you unpacked the datasets and the weights file 

# Testing the Models

To test the model and reproduce the results of the paper you can use the following scripts

    #First, activate the virtual environment
    source ~/lsvo-environment/bin/activate
    
    #Go to the directory of the project
    cd /home/user/LSVO
    
    #Kitti d1 test - change the config.strategy parameter in the file to switch between ST-VO and LS-VO
    python3 -m app.kitti_test_dns_1
    
    #Kitti d2 test - change the config.strategy parameter in the file to switch between ST-VO and LS-VO
    python3 -m app.kitti_test_dns_2
    
    #Kitti d2 +  blur test - change the config.strategy parameter in the file to switch between ST-VO and LS-VO
    python3 -m app.kitti_test_dns_2_blurred
    
    #Malaga d1 test - change the config.strategy parameter in the file to switch between ST-VO and LS-VO
    python3 -m app.malaga_test_dns_1
    
    #Malaga d2 test - change the config.strategy parameter in the file to switch between ST-VO and LS-VO
    python3 -m app.malaga_test_dns_2
    
    #Malaga d2 + blur test - change the config.strategy parameter in the file to switch between ST-VO and LS-VO
    python3 -m app.malaga_test_dns_2_blurred
    
Each test generates a directory inside results/trajectories named multi_task_{dataset}_{exp_type} where the computed transformation are stored. If you want to compute the errors as in the paper you need to download the kitti devkit from the KITTI Benchmark web page http://www.cvlibs.net/datasets/kitti/eval_odometry.php
    
# Soon available

The code for training will be made available soon, as well as the images and the computed optical flow used for training the models.
