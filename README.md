# PaddleClas_Using_3

AiStudio:[PaddleClas全流程文档（三）](https://aistudio.baidu.com/aistudio/projectdetail/1184186)
### **PaddleClas全流程文档（三）：主要介绍Windows下如何C++编译，如何使用cmake生成sln解决方案，编译出exe预测程序文件，以及dll库，用于python和C#调用预测**
### 上一篇[部署二，Serving服务](https://aistudio.baidu.com/aistudio/projectdetail/1585531) ，下一篇[部署四，传参调用DLL](https://aistudio.baidu.com/aistudio/projectdetail/1589564)


# 一、如何进行C++预测代码的编译（生成.sln解决方案，exe方案）

## 1.1准备
- **工具：Cmake，VS2019社区版， Git（三个安装包已载入到项目）**
-  **依赖库：**
-  [Opencv](https://sourceforge.net/projects/opencvlibrary/files/3.4.6/opencv-3.4.6-vc14_vc15.exe/download) （3.4.6版，已载入到项目 opencv-3.4.6-vc14_vc15.exe，解压时目录要和预测库放在一个目录下）
-  [Paddle预测库](https://www.paddlepaddle.org.cn/documentation/docs/zh/develop/guides/05_inference_deployment/inference/windows_cpp_inference.html)（Windows  cuda10 paddle2.0版，paddle_inference_install_dir.zip，需要自行下载）  
-  [PaddleClas：](https://github.com/PaddlePaddle/PaddleClas/blob/release/2.0)（release2.0版）
#### **Aistudio截图：**

<br/>

<img src="https://ai-studio-static-online.cdn.bcebos.com/bcbf865df3724b2786029c6cd4f1c5a82eca42fef7f24da49f031ddbc32aa6e0" width = "800" height = "400" align=center />

<br/>

## 1.2 将依赖库和预测代码存放在一个目录下
- **Opencv打开后会显示解压路径，选择或者新建一个文件夹（之后的预测库和Clas都会放在该目录下）**

<br/>

<img src="https://ai-studio-static-online.cdn.bcebos.com/1a674c2fc5714357bfe696a33f2efa1ef2464e8650a14cacb136a90b4f2416ee" width = "800" height = "400" align=center />


<br/>

<img src="https://ai-studio-static-online.cdn.bcebos.com/3373707348df45589c540df010a1842ab007d66aaf924d329999a756f1b22574" width = "800" height = "400" align=center />

## 1.3 将opencv添加到环境变量
- **打开opencv目录，把opencv路径下的的opencv\build\x64\vc14\bin 路径添加到path环境变量中：**
- **环境变量打开方式：右键计算机图标->高级系统设置->高级->环境变量**
- **编辑系统变量 path：添加变量值“G:\projects\opencv\build\x64\vc14\bin”，确定**

<br/>

<img src="https://ai-studio-static-online.cdn.bcebos.com/7cc12f9b6bad4d54b5a07b239d34a25c8b08dd01d19b48f6b261093efd50aae2" width = "800" height = "400" align=center />

<br/>

## 1.4 利用Cmake软件进行编译
#### **在Windows搜索栏输入Cmake打开Cmake gui（如果没有请重新安装下，安装包见1.1章节）**

<img src="https://ai-studio-static-online.cdn.bcebos.com/fa368e301d1a4f219f6c7c4ebcde4c87abcb06655ca442e5888cd92a9d012d64" width = "800" height = "400" align=center />

#### **点击configure，选择vs2019 X64选项后，点击Generate**
<br/>

<img src="https://ai-studio-static-online.cdn.bcebos.com/aba88ded36a046c6bf08b5b8c4d9ce82ef723e4d0e734116a71c418c5d762bec" width = "800" height = "400" align=center />

<br/>

#### **然后会发现报错：如下：**

<br/>

<img src="https://ai-studio-static-online.cdn.bcebos.com/068ed825291c4295ab06a7a64c9ae6280222bdd689be462bb7d65d502edbc25a" width = "800" height = "400" align=center />

<br/>

#### **根据报错进行修改，主要修改cuda_lib、cudnn_lib、opencv、paddle_dir路径（双击修改）**

```
CUDA_LIB:
C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v10.0\lib\x64
CUDNN_LIB:
C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v10.0\lib\x64
OPENCV:G:\projects\opencv
PADDLE_DIR:G:\projects\paddle_inference_install_dir
```

<br/>

<img src="https://ai-studio-static-online.cdn.bcebos.com/bcad5a0e89274a14b121809b2b46b288581adf110138443ca679254d51327130" width = "800" height = "400" align=center />

<br/>

#### **修改完成，再次点击 Generate，表示生成sln解决方案。**

<br/>

#### ----------------------------------------------------------------------------------------------------------------------------------------------------------------

#### **如果出现错误，请检查各路径是否正确，以及预测库对应版本是否正确**

#### ----------------------------------------------------------------------------------------------------------------------------------------------------------------

## 1.5 生成exe文件
#### **当显示Generating done 后点击open Project（已经安装好vs2019）打开sln解决方案**

<br/>

<img src="https://ai-studio-static-online.cdn.bcebos.com/71916a0c5bfa4b34a268a6e448fedd0790d57191b8104bdf8565f16675f57cf0" width = "800" height = "400" align=center />

<br/>

#### **打开后需要重新生成解决方案，同时把debug改为release：**

<br/>

<img src="https://ai-studio-static-online.cdn.bcebos.com/dff8197b95da46c9af7185a87693ba6f4e63fb3172cc4718ad183a0e3056307f" width = "800" height = "400" align=center />

<br/>

<img src="https://ai-studio-static-online.cdn.bcebos.com/7566847ac8d945748c84e62c1a4d36127eb714bee78944189e2fd6e4821bea4f" width = "800" height = "400" align=center />

<br/>


#### **生成可能会有段时间，稍等一会，有如下显示表示生成完成**

<br/>

<img src="https://ai-studio-static-online.cdn.bcebos.com/019bba4c8fcd481985b90f290d755ead1cd795ce7b7446f0b716f995bbf387d8" width = "800" height = "400" align=center />

<br/>



## 1.6 使用exe文件预测
#### **当我们使用vs重新生成完成后，会发现 out目录下面有一个release文件文件夹，该文件夹下是我们刚才生成的 clas_system.exe 文件：**

<br/>

<img src="https://ai-studio-static-online.cdn.bcebos.com/7396ba7577374d169319548bdc32993948da1a3ff88d4fbf973dd8984ff51553" width = "800" height = "400" align=center />

<br/>

#### **接下来，我们使用该exe来预测图片：**
#### **预测前需要准备配置文件 ：配置文件为cpp_infer\tools目录下 config.txt**

<br/>

<img src="https://ai-studio-static-online.cdn.bcebos.com/a90c711877ce4d6e97d62eb84acdd292f9231233e14540c5a0c2f111ba928d12" width = "800" height = "400" align=center />

<br/>

#### **记事本打开该文件，并作如下修改：**


- use_gpu 1  表示使用gpu预测
- gpu_id 0   这里如果电脑有多张卡（核显和集显），需要去设备管理器禁用掉不用的那张显卡，不能写1 ，因为Windows不支持多卡训练，默认为0
- cls_model_dir 使用预测模型的路径，根据之前自己训练的模型，转换成inference模型后的路径（如果没有训练，请查看链接4.2章节，因为版本更新，需要把__model__和__variables__分别改名为model和params）

<br/>

<img src="https://ai-studio-static-online.cdn.bcebos.com/51fd6140cb5844a8b4030977f90642aa085c58b2e9934b748d81f1fc686c1131" width = "800" height = "400" align=center />

<br/>
#### **例：如下**

<br/>

<img src="https://ai-studio-static-online.cdn.bcebos.com/f9d458ad48ae48eea4bb7d26366ed43b3ef04eeff2674247ac933eee05d4832e" width = "800" height = "400" align=center />

<br/>

#### **以上更改完成后使用cmd来预测一下（此为示例，具体目录根据自己路径来）：**
#### **cd到release目录：**

<br/>

<img src="https://ai-studio-static-online.cdn.bcebos.com/a6dd1fa6e61a447e9bc8dbea1d7c2775189bb34ff107497684225efdb22d147a" width = "800" height = "400" align=center />

<br/>

#### **使用clas_system.exe 配置文件路径 图片路径 进行预测：**

`.\clas_system.exe ..\..\tools\config.txt ..\..\..\..\dataset\flowers102\jpg\image_00001.jpg`

#### **预测结果如下：**

<br/>

<img src="https://ai-studio-static-online.cdn.bcebos.com/8f4a233fa6784d2b8705b0a44b2ecf2920a60a24bd314a1bbfa628a207695d93" width = "800" height = "400" align=center />

<br/>

#### **注：预测的图片为dataset/flowers102目录下图片，如果没有下载，请查看链接2.1章节**
#### **以上我们完成了使用exe文件的预测流程**



# 二、如何将C++预测代码封装成一个dll、
#### 上面章节我们完成了exe文件的预测流程，但是如果我们打算通过别的程序来预测呢！这里我们将完成dll的封装
## 2.1 修改CMakeLists.txt
#### 该文件在deploy/cpp_infer目录下
#### 修改该文件的倒数第20行
#### add_executable(${DEMO_NAME} ${SRCS})
#### 改为ADD_library(${DEMO_NAME} SHARED ${SRCS})

<br/>

<img src="https://ai-studio-static-online.cdn.bcebos.com/f514eb31d51440758f7c35ce5b1dea9f9027753d9b0d4f7e8c953ab1feba8d21" width = "800" height = "400" align=center />

<br/>

#### 改成如下字样：

<br/>

<img src="https://ai-studio-static-online.cdn.bcebos.com/796846025f774509b7a4a5594cee3255b71aefab7b76420e90fd43813ced5e4c" width = "800" height = "400" align=center />

<br/>

## 2.2 按照上文1.4章节继续重新cmake一次

<br/>

<img src="https://ai-studio-static-online.cdn.bcebos.com/3cf7ecbed6fe4154a1cecad2b4d9d4b75d1f69e316ae4f17b3991bcba6cd83a7" width = "800" height = "400" align=center />

<br/>

## 2.3 修改属性

#### 打开该sln后，在属性—常规—配置类型中修改成.dll文件，确定

<br/>

<img src="https://ai-studio-static-online.cdn.bcebos.com/34a7126498144ca6b5f5d856dd96b41ef0770c063530451985025b073d6c0207" width = "800" height = "400" align=center />

<br/>


#### 右键cls_system重新生成

<br/>

<img src="https://ai-studio-static-online.cdn.bcebos.com/e3b2440c06e24a9e9624c48f57d489f94dde8c303bd14fb2b0654317b91b767b" width = "800" height = "400" align=center />

<br/>

#### 待生成成功

 
<br/>

<img src="https://ai-studio-static-online.cdn.bcebos.com/6cbc1c32b6574eb8bbb23ac7c85651c2864215311b0c442db63a93aee8389a49" width = "800" height = "400" align=center />

<br/>
 
#### 然后我们打开release目录，会发现有clas_system.dll文件

<br/>

<img src="https://ai-studio-static-online.cdn.bcebos.com/fecf51822c584a2a854517bb84b4721459a42ba2d24f44ebaac09c1a6941ecd9" width = "800" height = "400" align=center />

<br/>

#### 您以为这就好了？不，还要改嘞！！！
## 2.4 修改main.cc
#### 在main.cc文件内添加代码：
#### 1.在int main(int argc, char **argv) 代码上方添加如下代码：

`extern "C" __declspec(dllexport) int main(int argc, char** argv);  //表示python可以调用该dll`

#### 2.把Config config(argv[1]); 改为：

`Config config("G:/projects/PaddleClas-dygraph/deploy/cpp_infer/tools/config.txt");`

#### 该路径为预测配置文件路径
#### 3.把std::string img_path(argv[2]); 改为：

`std::string img_path("E:/PaddleClas-dygraph/dataset/flowers102/jpg/image_00001.jpg");`

#### 该路径为预测图片路径
#### 4.删掉if (argc<3){...}
#### 结果如下：

<br/>

<img src="https://ai-studio-static-online.cdn.bcebos.com/efde2edfa3c745638dc559b67d53a32bb72e855f27eb47088e443c7d46085a4d" width = "800" height = "400" align=center />

<br/>

#### 5.修改完成后重新生成...

<br/>

<img src="https://ai-studio-static-online.cdn.bcebos.com/28b840952d8f4ab78fa9bd74dbec4e0a4267902c168e45fc9f9d2bd117720edc" width = "800" height = "400" align=center />

<br/>

## 2.5 python调用dll 预测
#### 重新生成完成后，在release目录新建python文件：
#### 内容为：

```
import ctypes
from ctypes import *
dll=CDLL("clas_system.dll")
print(dll.main())
```

#### 运行：
#### cmd 进入该目录，运行clas_system.py
#### 预测结果如下。

<br/>

<img src="https://ai-studio-static-online.cdn.bcebos.com/22a84efebffd4c2082dcf88582dab392bd3e60ecc96b4d1893d500c03ddc1a53" width = "800" height = "400" align=center />

<br/>

#### **到这里我们的python端调用dll预测流程已经完成**。

## 2.6 c#调用dll预测
### 1.创建c#控制台应用

<br/>

<img src="https://ai-studio-static-online.cdn.bcebos.com/5e0e0a8789e848faa2738cde37ebe58bfa3f2fa695cd4e3d83992ba5b881da4b" width = "800" height = "400" align=center />

<br/>

### 2.修改代码如下：

```
using System;
using System.Runtime.InteropServices;

namespace ConsoleApp1
{
    class Program
    {
        [DllImport("clas_system.dll", EntryPoint = "main", CharSet = CharSet.Ansi)]
        public static extern void main();
        static void Main(string[] args)
        {
            main();

            Console.Write("Press any key to continue . . . ");
            Console.ReadKey(true);
        }
    }
}
```

### 3.将我们之前在release目录中生成的dll全部复制到新建的控制台项目中
#### 目录为：.......\ConsoleApp1\ConsoleApp1\bin\x64\Debug\netcoreapp3.1

<br/>

<img src="https://ai-studio-static-online.cdn.bcebos.com/3cd8699cecb34fbba88827dd8dce0ffff7e5aa5dbc43417b93d1452623248a7c" width = "800" height = "400" align=center />

<br/>

<img src="https://ai-studio-static-online.cdn.bcebos.com/aa8ace8652094516b49e4cabc497e170c553c51e918248959fa22f12ad2a004f" width = "800" height = "400" align=center />

<br/>

### 4.Debug编译
#### 编译前需要修改下 “解决方案平台”
#### ConsoleApp属性->生成->目标平台->x64

<br/>

<img src="https://ai-studio-static-online.cdn.bcebos.com/246380f396204eca8a54bedda7ebeeba9c4c273b9391469db0e5c2327c3ab769" width = "800" height = "400" align=center />

<br/>

#### 修改完成后，重新生成

<br/>

<img src="https://ai-studio-static-online.cdn.bcebos.com/5a5571009211499db2d94ca83d29dd0199dc6c4a3ff34b4a9dd5d6fec910df26" width = "800" height = "400" align=center />

<br/>

#### 单击上方 ConsoleApp1 运行

<br/>

<img src="https://ai-studio-static-online.cdn.bcebos.com/bdc6e75bddc444d785c0ed261c66d4d9da1a737288fc4a59a565413913d49d3f" width = "800" height = "400" align=center />

<br/>

<img src="https://ai-studio-static-online.cdn.bcebos.com/c293840dd30649e5807d76293d3015bf8ca287cbfb2f4ad8a6b8d6de17d3e24f" width = "800" height = "400" align=center />

<br/>






#### 成功输出预测结果，当然，我们生成的程序存放在目录G:\projects\c#\ConsoleApp1\ConsoleApp1\bin\x64\Debug\netcoreapp3.1下面直接打开该exe文件也可预测

<br/>

<img src="https://ai-studio-static-online.cdn.bcebos.com/764f46a6be4945b9afbfc93d5285f9c0ebdda1c14259481691d68a38aa107d85" width = "800" height = "400" align=center />

<br/>

### **如果在操作过程中有任何问题欢迎在评论区提出，或者在[PaddleClas-Github](https://github.com/PaddlePaddle/PaddleClas)提issue**
