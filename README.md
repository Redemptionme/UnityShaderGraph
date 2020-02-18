# UnityShaderGraph

## common step

以下为必须步骤

建立unity工程，本工程使用unity 2019.3.6f

打开Windows-package manager 下载安装shader graph

安装Lightweight RP

工程设置 打开工程文件 右键create-rendering-Universal -pipeline-pipeline asset 

打开unity-edit-project setting- graphics-将刚才生成的配置文件拖入(别拖错了)

//

## effect 1 边缘发光

效果显示

![](./Doc\pic\效果 边缘发光.png)

step1

pbrmaster ALbedo 可以修改颜色，下面效果需要连接到emission

新建node: fresnel effect 设置power 为 3

新建Node:color 选择颜色

新建mutiply，fresnell 和color 分别连接此项的AB，再将输出给emision 

效果完成，新建material shader选择上述shader既可看到效果

优化

step2

可以将color右键变成convert to proprities

在预览窗口可以修改custom mesh 来修改预览物件

如果要让颜色变化起来

新建node： time 将sinetime 连接一个新建remap node（因为我们希望输出的值在0 - 1之间）

将step1结果与step2 联合一个新的node mutiply再给 PBR Master emission

至此变化的效果完成

step 3

添加纹理（使效果更明显可以使用物件一样的纹理)

proprities 新建texture，将属性拖入编辑器中，连接一个新建的sample texture 2d，最后连接到PBR Master 的Oclusion 

场景中的shader里面可以修改贴图，如果效果更明显可以使用物件一样的纹理



## effect2 dissvoe 消融消失

![](.\Doc\pic\消融消失.png)



step 1

新建 simple noise,scale 选择30，节点连接到PBR Master alpha

修改PBM master 设置的surface 为tranparent

//创建 vector1 连接到PBr Master 的 alphaclipThreshold 

上述注释可以看到效果，创建一个time 用sinetime 连接一个remap ，再连接aplhaclipthreshold

step 2

将simple nosie 的out多拉一个step，将step out 到PBR Master emission

将remap out 多拉一个Add B，A填入0.01 ，add的out 给step 的in

step3 修改颜色

添加一个color ，mutiply 另外一个入口选择 step的out，然后将mutiply的out 连接到PBR emission

将colore convert to proprety,再添加一个vector1 修改add的a为它

## effect3 ShadeFlag 摇晃的旗帜

![]()

step1 

