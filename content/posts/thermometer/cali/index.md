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

{{< img src="/posts/thermometer/cali/images/1.png" align="center" title="校准系统">}}

Elim红外测温模块的校准系统如上图所示。整个系统可分为软件部分和硬件部分。软件部分是由CaliServer和CaliWare两套软件组成。硬件部分则由恒温箱、红外辐射源、校准辅助板和计算机组成。

在整个校准系统中，软件部分是最重要的。它负责控制校准环境，记录校准数据，计算校准参数，读写校准参数等。这套软件采用CS结构进行设计。CaliServer作为服务端，提供数据的存储等服务。CaliWare作为客户端，实现对校准系统的控制，对被校准模块的读写，校准参数的计算等功能。


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
* 通过校准辅助板读取模块采集到的原始值
* 保存采集到的原始值到CaliServer中
* 从CaliServer下载模块对应的全部原始值，并计算校准参数
* 更新模块中的校准参数
* 保存校准参数到CaliServer中
* 将工厂数据写入到模块中

登陆
{{< img src="/posts/thermometer/cali/images/6.PNG" align="center" title="登陆">}}
{{<vs 3>}}

校准过程
{{< img src="/posts/thermometer/cali/images/7.PNG" align="center" title="校准">}}
