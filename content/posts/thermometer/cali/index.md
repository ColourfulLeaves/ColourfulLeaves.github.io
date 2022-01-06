---
title: "红外测温之校准"
date: 2021-12-15T08:06:25+06:00
description: Sample post with multiple images, embedded video ect.
menu:
  sidebar:
    name: 红外测温之校准
    identifier: cali
    parent: thermometer
    weight: 20
hero: images/hero.jpg
tags: ["Markdown","Content Organization","Multi-lingual"]
categories: ["Basic"]
---
### 系统总介

{{< img src="/posts/thermometer/cali/images/1.png" align="center" title="校准系统">}}

Elim红外测温模块的校准系统如上图所示。整个系统采用CS结构进行设计。在这个CS系统中，CaliServer是Server端。它负责维护全部的校准数据，定义校准过程，也维护整个校准系统用户和其权限。

CaliWare和及其配属的硬件是作为整个系统的Client端，它对应的是校准过程中的每一个校准站，即校准点。它的主要功能是控制校准点的环境，记录校准数据，计算校准参数和读写模块。

这种CS结构设计的优点是：

1. 采用了权限管理，只有具有授权的人才可以访问校准数据，设置校准流程和校准点数据，确保数据的安全。
2. 校准流程和校准点数据可设置，整个系统可适配多种型号的校准。
3. 支持更灵活的校准产线，可以根据生产情况，随时调整工作流水线的设定，具有更大的柔性。
4. 易用的CaliWare，更适合产线操作员。


### 相关设置

#### 工作站
工作站又称机位。它是用来设置当前Client端在整个校准序列中的位置。它的设置项为系统默认，分为：“初站”，“间站”和“终站”。

CaliWare在工作时，如果它的设置为“初站”，它会首先向CaliServer申请一新的ID，并将这一ID写入到模块中。它也会完成对模块的其他必要的初始化的工作。随后，它会完成同“间站”设置相同的功能。

如果CaliWare的设置为“间站”，它仅仅完成模块对该校准点的测量，并将测量结果保存到CaliServer中。

如果CaliWare的设置为“终站”，在完成上面“间站”设置相同的功能后，它会从CaliServer上下载全部的测量数据，计算校准参数，把校准参数写入到模块中。

#### 校准点
校准点即在校准过程中选取的标准点。为了能够更高的精度，这些校准点应该均匀分布在产品的测量范围。所以，不同的型号会对应不同的校准点设置。




### CaliServer

CaliServer是基于python Flask框架编写的一Web App。它的主要作用是：
    
* 校准过程中的数据的记录
* 维护产品数据库
* 操作人员权限管理维护
* 校准过程的管理和维护

权限管理页面
{{< img src="/posts/thermometer/cali/images/2.PNG" align="center" title="权限管理">}}
{{<vs 3>}}

用户管理页面
{{< img src="/posts/thermometer/cali/images/3.PNG" align="center" title="用户管理">}}
{{<vs 3>}}

校准点管理页面
{{< img src="/posts/thermometer/cali/images/4.PNG" align="center" title="校准点管理">}}
{{<vs 3>}}

校准数据管理页面
{{< img src="/posts/thermometer/cali/images/5.PNG" align="center" title="校准数据管理">}}


### CaliWare
CaliWare是基于Python+Qt5编写的桌面软件。它的主要功能有：
* 控制恒温室温度，为校准过程提供稳定的环境
* 控制红外辐射源的温度，为校准过程提供准确的目标温度
* 通过校准通讯板读取模块采集到的原始值
* 保存采集到的原始值到CaliServer中
* 计算校准参数
* 更新模块中的校准参数
* 保存校准参数到CaliServer中
* 将工厂数据写入到模块中

登陆
{{< img src="/posts/thermometer/cali/images/6.PNG" align="center" title="登陆">}}
{{<vs 3>}}

校准过程
{{< img src="/posts/thermometer/cali/images/7.PNG" align="center" title="校准">}}
