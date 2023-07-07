# Training A Transformer Model

本项目提供了一个T5模型训练框架。

## 预训练

```shell
python main.py optim.name=adamwscale optim.lr_scheduler=legacy model.compile=true optim.batch_size=16
```

We recommend adding `model.compile=true` flag for pre-training, if you are able to install PyTorch 2.0.


### 下载Super-Natural Instructions数据集

下载[NI](https://github.com/allenai/natural-instructions.git)项目中的task文件夹数据到data/tasks下。

### 微调

We strictly follow the fine-tuning [config](configs/task/ft.yaml) of Tk-Instruct. It remains unclear whether Tk-Instruct was initialised from a regular checkpoint (*google/t5-v1_1-base*) or the one adapted explicitly for Language Modelling with continued training (*google/t5-base-lm-adapt*). Therefore, we decided to evaluate both. Run the following command to reproduce the Tk-Instruct experiments:

```shell
python main.py task=ft model.name=google/t5-v1_1-base model.random_init=false model.checkpoint_path="" model.compile=true optim.batch_size=4```
```

Setting `model.random_init=false model.checkpoint_path=""` corresponds to downloading pre-trained weights from HuggingFace Hub.

Setting `model.random_init=false model.checkpoint_path="/path/to/pytorch_model.bin"` corresponds to using the weights [**pre-trained**](#pre-training) with nanoT5.

Setting `model.random_init=true model.checkpoint_path=""` corresponds to a random initialisation.

## 训练日志

一个参考训练日志在[T5_pretraining_for_beginner.ipynb](colab%2FT5_pretraining_for_beginner.ipynb)。

## 致谢

项目作者： Brian Shen. Twitter @dezhou.

## 关注我们
欢迎关注知乎专栏号。

[深度学习兴趣小组](https://www.zhihu.com/column/thuil)

## 问题反馈 & 贡献
如有问题，请在GitHub Issue中提交。
我们没有运营，鼓励网友互相帮助解决问题。
如果发现实现上的问题或愿意共同建设该项目，请提交Pull Request。