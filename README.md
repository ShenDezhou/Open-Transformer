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
