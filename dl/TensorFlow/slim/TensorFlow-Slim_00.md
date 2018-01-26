# 0 前言
TF-slim是Tensorflow的一个新的轻量级的高级API，用来定义、训练、评价复杂模型。这个目录包含了使用tf-slim训练和评价几个广泛使用的CNN图像分类模型的代码。它包含了一些脚本，可以让你来重新或者从已经训练好的权重微调来训练模型。它也包含了以下代码：下载标准数据集、转换数据到tf原生tfrecord格式、从tf-slim's数据读取和队列程序读取它们。你可以轻松地在这些数据集上训练模型，就像我们如下展示的一样。我们也提供了一个jupyter notebook， 它提供了如何使用tf-slim进行图像分类的示例。为了开发或者修改我们的模型，也可以看tf-slim主页。

# 1 安装和设置
在本节中，我们将介绍安装相应的必备软件包所需的步骤。

## 1.1 安装最新版本TF-slim
TF-Slim可以通过TensorFlow 1.0作为tf.contrib.slim使用。 要测试您的安装正在工作，请执行以下命令; 它应该运行没有提出任何错误。
```
python -c "import tensorflow.contrib.slim as slim; eval = slim.evaluation.evaluate_once"
```

## 1.2 安装 TF-slim 图像模型库
为了用TF-Slim做图像分类，你也需要安装TF-Slim image models library，它不是核心TF库的部分。要做这到这一点，检出tensorflow/models仓库：
```
cd $HOME/workspace
git clone https://github.com/tensorflow/models/
```
这将把TF-Slim 图像模型库放在 ```$HOME/workspace/models/research/slim```。（它将创建一个叫models/inception的文件夹，它包含一个旧版本的slim；你可以放心地忽略它。）

为了验证一个是不是正常工作，执行如下命令；它将不引发任何错误。
```
cd $HOME/workspace/models/research/slim
python -c "from nets import cifarnet; mynet = cifarnet.cifarnet"
```

# 2 准备数据集
作为这个库的一部分，我们包含了下载几个常用图像数据集和转换它们到Slim格式的脚本。

## 2.1 下载和转换到TFRecord格式
对于每个数据集，我们需要下载原数据，并转成TFRecord格式。每个TFRecord包含一个TF-Example protocol buffer。

## 2.2 创建TF-Slim 数据描述子

## 2.3 处理ImageNet数据的自动脚本


# 3 使用预训练模型
当神经网络有很多参数使它为强有力的逼近函数时，效果很好。

注意这些准确率是通过评价一个crop来计算的。一些学术论文记录了更高的准确率，通过多crop多尺度。

# 4 从头训练

# 5 微调一个新任务
Fine-tuning a model from an existing checkpoint

我们经常想从一个预训练模型开始微调，而不是从头开始。为了表示要微调的起始点，我们用```--checkpoint_path```标志来调用训练，并为检查点文件指定一个绝对路径。

在微调模型时我们要注意恢复检查点权重。尤其当我们在一个不同输出标签数量的新任务上微调模型时，不能恢复最后的分类层。为此我们要使用```--checkpoint_exclude_scopes```标志。这个标志阻碍某些变量被加载。
当对一个类别数量与训练好的模型不同的分类模型进行微调时，新模型将有最后的logits层，它的维度不同于预训练模型。比如，在Flowers数据集上用ImageNet-trained进行微调时，预训练模型的维度是[2048x1001]，但是新的分类层将是[2048x5]。因此，这个标志表示TF-Slim来避免从检查点加载这些参数。



```
--checkpoint_path 用来微调的检查点
--checkpoint_exclude_scopes 阻碍某些变量被加载
--trainable_scopes 指定被训练的部分
```

# 6 评价性能
# 7 导出前向图
# 8 问题解决

# 9 参考资料
[TensorFlow-Slim image classification library](https://github.com/tensorflow/models/tree/master/slim)
[tensorflow/tensorflow/contrib/slim/](https://github.com/tensorflow/tensorflow/tree/master/tensorflow/contrib/slim)

