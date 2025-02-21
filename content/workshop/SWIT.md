---
date: 2024-12-20T00:00:00+08:00
lastmod: 2024-12-20T12:00:00+08:00
description: Seismic Waveform Inversion Toolbox
featured_image: "images/SWIT/SWITlogo.png"
tags: [SWIT,FWI]
title: "SWIT"
categories:
---
# **Introduction**
**SWIT**（**Seismic** **Waveform** **Inversion** **Toolbox**）是一个用于地震波形反演（**FWI**）的软件工具，使用Fortran和Python编写，由[Haipeng Li和Junlun Li][SWITauthor]开发。

该工具实现了两种非线性反演优化方案，即非线性共轭梯度（NLCG）方法和拟牛顿方法（L-BFGS），并配有高效的线搜索策略。软件提供了多种拟合函数，包括L-2波形（Tarantola，1984）、交叉相关（Luo&Schuster，1991）和归一化全局相关系数（Choi&Alkhalifah，2012）。用户可以通过Python脚本运行FWI项目，并使用提供的GUI进行参数设置。SWIT-1.0包括前向和伴随求解器、反演工具箱和GUI工具箱三个部分，用于地震波形反演。软件包还提供了图形用户界面（GUI），方便用户使用。

该工具的特点包括前向波场建模（FD）、伴随波场建模（FD）、梯度计算、预处理和正则化、L-BFGS和NLCG优化算法、有效步长搜索、多种不匹配函数以及多尺度反演。它使用Fortran（MPI）进行前向模拟，Python进行反演，并提供了三种使用方式：图形用户界面（GUI）、Python脚本和Jupyter Notebook。
 

开源地址：[https://github.com/seisfwi/SWIT](https://github.com/seisfwi/SWIT)

类似的全波形反演工具：



# **Installation**

安装SWIT需要先安装OpenMPI，然后是Anaconda和Python依赖项，如numpy、obspy、scipy、matplotlib等。运行SWIT可以通过GUI或Python脚本执行。在反演过程中，用户可以设置不同的不匹配函数、优化方案、步长、迭代次数、速度模型的最大值和最小值，以及梯度的静默和平滑参数。SWIT的输出包括波形/波场数据。用户可以在提供的example文件夹中找到案例研究。
### **Step 1**
```sh
sudo apt-get install build-essential
sudo apt install gfortran

# Download the OpenMPI package, 
# or go to: http://www.open-mpi.org/software/ompi to download the desired version
wget https://download.open-mpi.org/release/open-mpi/v4.1/openmpi-4.1.1.tar.gz 
tar xvfz openmpi-4.1.1.tar.gz
cd openmpi-4.1.1

# Configure & install OpenMPI (this would take quite a while)
# If no sudo permision granted, install OpenMPI in your personal folder, i.e.
# /home/user-name/softare/openmpi/
./configure --prefix=/usr/local/openmpi CC=gcc FC=gfortran
make
# if you install on: /usr/local/openmpi 
sudo make install
# if you install on your personal folder, no sudo required
make install

# Add path to ~/.bashrc
# If you use a personal path, change to your path
echo export PATH=/usr/local/openmpi/bin:$PATH >> ~/.bashrc
source ~/.bashrc

# Check
which mpirun

```

### **Step 2**

```sh
# Install Python dependencies (the USTC mirror is used here).
pip install numpy obspy scipy matplotlib multiprocess PySimpleGUI psutil Pillow -i https://pypi.mirrors.ustc.edu.cn/simple/

# Complie the fd2dmpi forward solver with gfortran & mpif90.
cd /your/own/path/to/SWIT-1.0/fd2dmpi/
rm *.mod
make clean
make

# Add paths of fd2dmpi & Python toolbox to ~/.bashrc 
echo export PATH=/your/own/path/to/SWIT-1.0/bin:$PATH >> ~/.bashrc
echo export PYTHONPATH=/your/own/path/to/SWIT-1.0/toolbox >> ~/.bashrc
source ~/.bashrc

# Check the solver 
which fd2dmpi

# Check the Python toolbox in a Python Shell 
import base, inversion, preprocess, postprocess, solver, tools 
```


### **Step 3**

```sh
cd /your/own/path/to/SWIT-1.0/toolbox/
python runswit_Linux.py   # python runswit_MacOS.py    
```

```sh
cd /your/own/path/to/SWIT-1.0/examples/case-XX/
python SWIT_workflow.py  # Please modify paths before running  
```
---
[SWITauthor]: https://doi.org/10.1029/2022JB025748