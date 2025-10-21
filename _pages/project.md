---
layout: page
permalink: /VNIV-fall-2025/project/
title: Course Project
description: Guidelines and suggestions for course projects
---

# INTR 6000P - Introduction to Visual Navigation Final Project：Building and improving ORB-SLAM2 for Trajectory Construction

## Overview

**INTR 6000P - Introduction to Visual Navigation Final Project：Building and improving ORB-SLAM2 for Trajectory Construction**

Welcome to the final project of INTR 6000P Introduction to Visual Navigation course! This project challenge you to develop your own SLAM system that can computes the camera trajectory in different situations.

📖**How to build ORB-SLAM 2 **:
https://github.com/raulmur/ORB_SLAM2?tab=readme-ov-file

This project asks you to build and improve ORB-SLAM2 to reconstruct trajectories from 7 provided datasets using a monocular camera, and to evaluate results against provided ground truth using EVO. You will submit fully reproducible code, evaluation outputs, and a technical report. This is an solo-only project.

---

## Description

### The Challenge

Although OrbSlam2 can identify trajectories within the camera's captured environment, trajectory reconstruction may fail or yield low accuracy for relatively complex scene data. In such cases, adjusting relevant codes and parameters or introducing additional optimization methods is necessary to enable the SLAM system to reconstruct trajectories with high precision across multiple scene datasets of varying difficulty. Your task is to build and refine your own OrbSlam2 implementation to achieve the most complete and accurate trajectory reconstruction possible across the seven distinct scene datasets provided(monocular only).

### Dataset Details

-**Categories**: carwelding2, factory1, factory2, factory6, hospital, amusement1, amusement2
-**Difficulty**: Easy, Medium, Hard
-**Files**: image_left, pose_left.txt, timestamps.txt

### Groundtruth and Evaluation Method Provided

The groundtruth trejactory files of seven datasets will be provided. And you are required to use EVO to evaluate the trajectory results of SLAM comparing with the groundtruth.

📖**How to build EVO **:
https://github.com/MichaelGrupp/evo/tree/master?tab=readme-ov-file

### Technical Requirements

**Complete Submission Package:**

1. **Source Code**: All SLAM and relative files
2. **Technical Report**: Introduction, refined SLAM code and optimization method, trajectory results, discussion and conclusion, citation
3. **Result Figures**: RMSE Error Curve for ATE, trajectory curve, RMSE Error
4. **AI-generated Report**

### Learning Objectives

- Understand trajectory reconstruction through different cameras
- Experience building environment and SLAM system
- Learn to optimize SLAM system through different methods
- Learn to write a academic report/paper with formal structure.

This project emphasizes **engineering excellence** over pure performance optimization. Clean, well-documented code and report that demonstrates understanding of the underlying principles will be highly valued. Try to complete all datasets' trajectory reconstruction as possible as you can.

---

## Getting Started Guide

### Workflow

1. Goals and delieverable
2. Set up Ubuntu + development toolchain
3. Build and run ORB-SLAM2 (monocular)
4. Generate trajectories for 7 datasets
5. Evaluate with EVO (ATE RMSE for translation and rotation) and visualize
6. Write a technical and academic report.
7. Submit a report, full code package, and result artifacts

### Environment Setup

Before starting, install **Ubuntu 20.04** and **VMware Workstation**(if needed). If you haven't already, download and install all:

👉 [VMware Workstation](https://www.vmware.com/products/desktop-hypervisor/workstation-and-fusion)
👉 [Ubuntu 20.04](https://ubuntu.com/download)

Then create a clean environment.
Make sure the setting of ROM, Core, and Disk Space are suitable for SLAM
Suggested resources: CPU ≥ 4 cores, RAM ≥ 4 GB, Disk ≥ 40 GB

### Environment Setup

Open terminal

1. Install CMake (on terminal):
  Most important environment setup

```bash
sudo apt-get install cmake
sudo apt-get install build-essential libgtk2.0-dev libavcodec-dev libavformat-dev libjpeg-dev libswscale-dev libtiff5-dev
sudo apt-get install libgtk2.0-dev
sudo apt-get install pkg-config
```

2. Install Dependences:
  Necessary Libraries including : OpenGL, GLEW, Boost, Python3…

```bash
sudo apt-get update
sudo apt install libgl1-mesa-dev
sudo apt-get install libglew-dev
sudo apt-get install libboost-dev libboost-thread-dev libboost-filesystem-dev
sudo apt-get install libpython3-dev
sudo apt-get install python3-tk
```

### Install libraries

3. Install Pangolin 0.6
  Necessary Libraries including : OpenGL, GLEW, Boost, Python3…

```bash
cd pangolin-0.6
sudo apt -y install libeigen3-dev libjpeg-dev libpng-dev libtiff-dev
mkdir build && cd build
cmake .. -DCMAKE_BUILD_TYPE=Release
make -j$(nproc)  %make -4(if you set nproc = 4)
sudo make install
```

4. Install Eigen 3
  Download package from: http://eigen.tuxfamily.org, then unzip and install

```bash
cd eigen3
mkdir build
cd build
cmake ..
sudo make install
```

5. Install OpenCV 3.4.5
  Download package from: http://opencv.org, ,then unzip, build and install

```bash
cd opencv3.4.5
make build
sudo cmake -D CMAKE_BUILD_TYPE=Release -D 
CMAKE_INSTALL_PREFIX=/usr/local ..
sudo make -j8
sudo make install
```

Modify configuration file
Step1. sudo gedit /etc/ld.so.conf **(run in the terminal)
Step2. include /usr/local/lib **(fill in the file and save)
Step3. sudo ldconfig **(close file and run in the terminal)
Step4. sudo gedit /etc/ld.so.conf **(run in the terminal)
Step5. PKG_CONFIG_PATH=$PKG_CONFIG_PATH:/usr/local/lib/pkgconfig
 export PKG_CONFIG_PATH **(fill in the file and save)
Step6. source /etc/bash.bashrc **(run in the terminal)
Step7. pkg-config opencv --modversion

### Tool Setup

6. Install ORB-SLAM 2
  Download package from: https://github.com/raulmur/ORB_SLAM2?tab=readme-ov-file ,then unzip, build and install

(Tips1: ORB-SLAM2 requires the support of DBoW2 and g2o, which are included in the third-party folder of downloaded package, thus no need to download and install again. )

(Tips2: build.sh file includes the building and installing of two libraries and orb-slam2, and make sure the number behind make order match the core number of the system)

```bash
cd ORB_SLAM2
chmod +x build.sh
./build.sh
```

### Run SLAM

**Step 1: Download data and camera file**

Download 7 provided datasets and camera file(.yaml) from CANVAS
(Category considering difficulty: 3 easy, 2 medium, 2 hard)

**Step 2: . Putting data in the data folder of ORB_SLAM2 folder**

Such as: /主目录/ORB_SLAM2/data/v1_01_easy/mav0/cam0/data

**Step 3: Putting camera file and TimeStamps data in folder of ORB_SLAM2 folder**

Such as: /主目录/ORB_SLAM2/Examples/Monocular/EuRoC_TimeStamps/MH_01.txt

**Step 3: Run the code below in terminal**

```bash
cd ORB_SLAM2
./Examples/Monocular/mono_euroc Vocabulary/ORBvoc.txt Examples/Monocular/EuRoC.yaml 主目录/ORB_SLAM2/data/v1_01_easy/mav0/cam0/data 主目录/ORB_SLAM2/data/v1_01_easy/mav0/cam0/data Examples/Monocular/EuRoC_TimeStamps/MH_01.txt
```

After running SLAM successfully, you will get a trajectory file.

(Tips: better using absolute path as code input)

---

## Evaluation

### Install Virtualenvwrapper and Run EVO

Open terminal

1. Install Virtualenvwrapper
  https://github.com/MichaelGrupp/evo/blob/master/doc/install_in_virtualenv.md

```bash
sudo apt install python3-virtualenvwrapper
echo "export WORKON_HOME=$HOME/.virtualenvs && source /usr/share/virtualenvwrapper/virtualenvwrapper.sh" >> ~/.bashrcsource ~/.bashrc
```

2. Setting up a virtualenv for EVO

```bash
mkvirtualenv evaluation --system-site-packages
workon evaluation
pip install evo
pip install --editable .
```

3. Run EVO for Trajectory Results and Ground Truth Dara (Using EVO_APE)

https://github.com/MichaelGrupp/evo/tree/master?tab=readme-ov-file

```bash
evo_ape tum ground_truth.txt trajectory.txt -r trans_part --plot --plot_mode xyz -as
```

### Evaluation Metrics

- **Translation RMSE (meters)**: RMS of positional error after alignment between estimated and GT trajectories
- **Rotation error (deg/rad):**: RMS of rotational discrepancy; typically reported via relative pose error (RPE) angles;
- **Completion Definition for Each Dataset**: Discard upon tracking loss and Initialize no more than 10% of images

Conclusion:

1. High Accuracy for all provided datasets;
2. Extra Optimization Application meets high score.

---

## Submission Checklist

### Required Deliverables

✅ **Source Code**: Complete files in one folder with clear documentation

✅ **Technical Report**: Detailed explanation of your method including:

- Abstract and key words
- Introduction
- Method and code improvements
- Results and analysis for each datasets
- Relative codes
- Discussions
- Conclusion
- Citation

✅ **Evaluation Results**: Figures of evaluation results of all datasets

✅ **Slides for presentation**: PPT

### Formatting Requirements

**Template**:: Must use the official lEEE conference template. Please refer to the authorguidelines and templates from recent lEEE International Conference on Robotics andAutomation (lCRA) proceedings for examples.

**Length**: Maximum 8 pages, including all figures, tables, and references.

**Layout**: Double-column format, as standard for lEEE conferences.

**Style**: Follow all lEEE formatting guidelines for citations, figures, and sections.

### Policy on the Use of Large Language Models (LLMs)

The generation of core content using LLMs is strictly prohibited. This includes the generation of originalanalysis, technical explanations, literature reviews, and conclusions.
Permitted use is limited to:
Proofreading and correcting grammar, spelling, and punctuationPolishing sentence structure and clarity for existing, self-written text.Formatting assistance (e.g. ensuring citation style compliance).

### Academic Integrity

- **Collaboration**: Solo only
- **External Data**: Only provided dataset permitted
- **Optimization Methods Freedom**: Allowed any new methods applied for the optimization

### Timeline

- **Project Start**: October 21, 2025
- **Submission Deadline**: December 1, 2025, 11:59 PM
- **Results Presentation**: Everyone present on December 2, 2025

These serve as reference implementations to help you get started. Your final scores will be determined by your performance.

***

* (The list will be replaced with the table of contents.)
{:toc}

***

