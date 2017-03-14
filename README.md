windows 下安装使用tensorflow
====
[中文文档](http://wiki.jikexueyuan.com/project/tensorflow-zh/)<br>
[官网地址](https://www.tensorflow.org/)<br>
##基本环境：
win10X64<br>
[python3.5](https://www.python.org/downloads/release/python-352/)<br>
tensorflow 0.12<br>
[cuda8.0](https://developer.nvidia.com/cuda-downloads)<br>
[cudnn5.1](https://developer.nvidia.com/rdp/cudnn-download)<br>
<br>
##准备工作
由于THE GREAT WALL , tensorflow官网有时候打不开，所以通过修改hosts的方式解决。<br>在C:\Windows\System32\drivers\etc\hosts中添加以下内容：<br>
```
#TensorFlow start
64.233.188.121 www.tensorflow.org
#TensorFlow end
```
由于我之前用的是python2.7，而tensorflow在windows上要用python3.5，所以我将两者都保留，具体做法如下：<br>
下载并安装python3.5，原来的python2.7不改动任作为默认版本。<br>进入python3.5的安装文件夹如：C:\Python35。将python.exe 和 pythonw.exe改为python3.exe 和 pythonw3.exe。<br>
右键”我的电脑” –> “选择属性” –> “高级系统设置” –> “环境变量”，然后选择path并添加两个路径：【C:\Python35】和【C:\Python35\Scripts】。<br>
具体使用pip时需要指定版本，如pip install *** 是默认的python2.7，python3 -m pip install *** 是python3.5
##安装tensorflow
cpu版本：<br>
```python3 -m pip install --upgrade https://storage.googleapis.com/tensorflow/windows/cpu/tensorflow-0.12.0rc1-cp35-cp35m-win_amd64.whl```
<br>gpu版本：<br>
```python3 -m pip install --upgrade https://storage.googleapis.com/tensorflow/windows/gpu/tensorflow_gpu-0.12.0rc1-cp35-cp35m-win_amd64.whl```
##为gpu版本安装cuda和cudnn<br>
首先查看[显卡的计算能力](https://developer.nvidia.com/cuda-gpus)，需要3.0及以上。<br>
下载安装cuda8.0.<br>
下载解压cudnn5.1,得到一个cuda文件夹，分别将cuda/include、cuda/lib/x64、cuda/bin三个目录中的内容拷贝到C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v8.0对应的include、lib/x64、bin目录下。
<br>检查cuda是否安装成功<br>
在C:\ProgramData\NVIDIA Corporation\CUDA Samples\v8.0\1_Utilities\deviceQuery目录下打开相应版本的sln文件并编译。<br>
然后在C:\ProgramData\NVIDIA Corporation\CUDA Samples\v8.0\bin\win64\Release目录下用CMD运行deviceQuery.exe,会输出显卡信息。<br>
##测试
```
python3
>>> import tensorflow as tf<br>
>>> hello = tf.constant('Hello, TensorFlow!')<br>
>>> sess = tf.Session()<br>
>>> print(sess.run(hello))<br>
Hello, TensorFlow!<br>
>>> a = tf.constant(10)<br>
>>> b = tf.constant(32)<br>
>>> print(sess.run(a + b))<br>
42
```
