---
date: 2024-12-03T22:00:00+08:00
lastmod: 2024-12-05T12:00:00+08:00
description: Seispy workshop
featured_image: "images/seispy_shortcut.png"
tags: [RF,Seispy]
title: "接收函数和Seispy总结"
categories: 
---
# **接收函数(Receiver Function)**
## **基本原理**

震源与仪器介质结构的卷积
```

```

时间域的卷积变换为频率域的乘积

# **Seispy**

### **数据格式**
原数据是按事件分类存放的，文件夹为事件发生时间。内部文件命名格式为%Y.%M.%D.%h.%m.%s.%station.%component.sac
```sh
```
用plot绘图sac数据，数据为90s,包括P波到达前20s和后70s。
```python
```

### **数据预处理**

**数据分类**
将原本按事件分类的sac文件重新按照台站分类
```
```

**数据重命名**
用下列脚本数据重命名为%station_name.%compotnent.%Y.%J.%h%m%s.sac
```
```



### **计算接收函数**

**修改rf.cfg配置文件参数**
数据已经是截取了P波前20s和后70s的了
```
```

**修改批量计算脚本**
```
```

**挑选接收函数**
```python
pickrf RFresult/%station_name  

#%station_name 为存放有单台接收函数文件夹名字，计算结束后会生成一个finallist.dat的文件
#不挑选接收函数无法进行H-κ和CCP计算
```
### **H-κ**


### **CCP叠加**

---
---

### **学习收获**
##### **数据处理流程**
单个台站？
识别远震信息：震中距30~90°，震级Mw大于的远震事件？
截取远震波形
事件波形预处理
计算震中距
旋转三分量
计算接收函数
### SAC
**配置SAC环境与全局变量**
```sh
export SACHOME=/usr/local/sac
export SACAUX=${SACHOME}/aux
export PATH=${SACHOME}/bin:${PATH}
export SAC_DISPLAY_COPYRIGHT=1
export SAC_PPK_LARGE_CROSSHAIRS=1
export SAC_USE_DATABASE=0
source ~/.bashrc
```
**SAC绘制波形图**
```sh
sac
#进入sac后前面会显示SAC>
r %file_name.sac
p
q
```
**SAC获取P波初至**