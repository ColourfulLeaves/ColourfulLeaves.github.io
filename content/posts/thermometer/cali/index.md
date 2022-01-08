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

Elim红外测温模块的校准系统如上图所示。这是一个CS结构的系统。在这个CS系统中，CaliServer是Server端。它负责维护全部的校准数据，定义校准过程，也维护整个校准系统用户和其权限。Cali Serverd可以同时为多个CaliWare提供服务。

CaliWare和及其配属的硬件是作为整个系统的Client端，它用来实现在校准过程中对每个校准点的校准操作。它的主要功能是控制校准点的环境，记录校准数据，计算校准参数和读写模块，与CaliServer互动（上传校准数据和结果，权限管理和更新校准配置信息）。

这种CS结构设计的优点是：

1. 采用了权限管理，只有具有授权的人才可以访问校准数据，设置校准流程和校准点数据，确保数据的安全。
2. 校准流程和校准点数据可设置，整个系统可适配多种型号的校准。
3. 支持更灵活的校准产线，可以根据生产情况，随时调整工作流水线的设定，具有更大的生产柔性。
4. 易用的CaliWare，更适合产线操作员。


### CaliServer

CaliServer是基于python Flask框架编写的一Web App。它的主要作用是：
    
* 校准过程中数据的记录
* 维护产品数据库
* 操作人员权限管理维护
* 校准过程的管理和维护

部分页面截图如下：

权限管理页面

在这个系统中，将用户分为两类，Admin和Public。 Admin是管理员，具有全部的系统操作权力。Public是为操作员准备的，具有此类权限的用户仅通过使用CaliWare与Cali Server进行交互，不能使用浏览器登陆系统或对系统进行查询等操作。
{{< img src="/posts/thermometer/cali/images/2.PNG" align="center" title="权限管理">}}
{{<vs 3>}}

用户管理页面
{{< img src="/posts/thermometer/cali/images/3.PNG" align="center" title="用户管理">}}
{{<vs 3>}}

工作站管理页面

工作站在CaliWare中被称为“机位”。此项设置对所有型号通用。
{{< img src="/posts/thermometer/cali/images/8.PNG" align="center" title="工作站管理">}}
{{<vs 3>}}


校准点管理页面

校准点即在校准过程中选取的标准点。为了能够更高的精度，这些校准点应该均匀分布在产品的测量范围。所以，不同的型号会对应不同的校准点设置。
{{< img src="/posts/thermometer/cali/images/4.PNG" align="center" title="校准点管理">}}
{{<vs 3>}}

校准数据管理页面

在这个页面，管理员可是实现对校准数据的增删改查等操作。
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

登陆UI

CaliWare此时会使用用户输入的账号密码登陆CaliServer，登陆成功后，获得CaliServer颁发的key，进入主UI。
{{< img src="/posts/thermometer/cali/images/6.PNG" align="center" title="登陆">}}
{{<vs 3>}}

主UI

操作员将模块准备好后，点击“开始校准”按钮开始对模块的校准。CaliWare在用户点击后，按照“机位”的设置，执行校准过程，并将执行的结果显示在提示框中。
{{< img src="/posts/thermometer/cali/images/7.PNG" align="center" title="校准">}}
