### conda源
```
conda config --show channels
conda config --show-sources
```

```
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/
conda config --set show_channel_urls yes
```

### pip源
```
pip config list

pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple

http://mirrors.cloud.tencent.com/pypi/simple
-i https://pypi.tuna.tsinghua.edu.cn/simple
```

### 安装qwen_72b
https://gitee.com/ascend/ModelLink/tree/master/examples/qwen#qwen-72b

```
cd /home/HwHiAiUser/ModelLink/
conda activate qwen_72b


# git下载模型(大文件)需要安装git-lfs
export PATH=/home/HwHiAiUser/git-lfs-3.5.1/bin:$PATH

git断点续传 git clone --recursive --resume  https://www.modelscope.cn/qwen/Qwen-72B-Chat.git

```


https://download.pytorch.org/whl/torch_stable.html

# 参数配置介绍
https://gitee.com/mindspore/mindformers/blob/dev/configs/README.md

# 模型权重转换

8转1
```
python /home/HwHiAiUser/mindformers2/mindformers/tools/transform_ckpt.py \
--src_ckpt_strategy /home/HwHiAiUser/model/output/strategy/merged_ckpt_strategy.ckpt \
--src_ckpt_dir /home/HwHiAiUser/model/output/checkpoint_network \
--dst_ckpt_dir /home/HwHiAiUser/model/output/out \
--prefix "checkpoint_"
```



# 训练集

```
/home/HwHiAiUser/model/qwen/Qwen-14B-Chat-hf/qwen.tiktoken
/home/HwHiAiUser/model/qwen/qwen_14b_ms_8
/home/HwHiAiUser/mindformers2/dataset/mindrecord/alpaca.mindrecord
/home/HwHiAiUser/mindformers2/train_check_point

/home/HwHiAiUser/model/qwen/Qwen-14B-Chat-ms/qwen_14b_ms.ckpt

```

### alpaca格式转换
```sh
python research/qwen/alpaca_converter.py \
--data_path ./dataset/alpaca_data.json \
--output_path ./dataset/alpaca-data-conversation.json
```

### json格式转mindrecord
```sh
python research/qwen/qwen_preprocess.py \
--input_glob ./dataset/conversation-json/qwen_train_data.json \
--model_file /home/HwHiAiUser/model/qwen/Qwen-14B-Chat/qwen.tiktoken \
--seq_length 2048 \
--output_file ./dataset/mindrecord/qwen.mindrecord
```

政策数据
```sh
python research/qwen/qwen_preprocess.py \
--input_glob /home/HwHiAiUser/mindformers2/dataset/conversation-json/qwen_train_data.json \
--model_file /home/HwHiAiUser/model/qwen/Qwen-14B-Chat/qwen.tiktoken \
--seq_length 2048 \
--output_file /home/HwHiAiUser/mindformers2/dataset/qwen_mindrecord/qwen.mindrecord
```
### 启动lora训练
```
bash run_singlenode.sh "python qwen/run_qwen.py \
--config qwen/run_qwen_14b_lora.yaml \
--load_checkpoint /home/HwHiAiUser/model/qwen/Qwen-14B-Chat-ms/qwen_14b_ms.ckpt \
--use_parallel True \
--run_mode finetune \
--train_data /home/HwHiAiUser/mindformers2/dataset/qwen_mindrecord/qwen.mindrecord" \
rank_table_8.json [0,8] 8
```
# 微调

```sh

# tokenlization
./model_from_hf/Qwen-72B-Chat/
# 权重
./model_weights/Qwen-72B-Chat-v0.1-tp8-pp1/
# 数据集
./dataset/Qwen-72B-Chat/alpaca_text_document
# lora
./ckpt/Qwen-72B-Chat-hf/
```

```python
python ./tools/preprocess_data.py \
  --input ./finetune_dataset/train-00000-of-00001-a09b74b3ef9c3b56.parquet \
  --tokenizer-name-or-path ./model_from_hf/Llama-2-13b-hf \
  --output-prefix ./finetune_dataset/Llama-2-13b-hf/alpaca \
  --workers 4 \
  --log-interval 1000 \
  --tokenizer-type PretrainedFromHF \
  --handler-name GeneralInstructionHandler \
  --append-eod
```

### lora微调
```bash
bash run_singlenode.sh "python qwen/run_qwen.py \
--config qwen/run_qwen_14b_lora.yaml \
--load_checkpoint /home/HwHiAiUser/model/qwen/Qwen-14B-Chat-ms/qwen_14b_ms.ckpt \
--use_parallel True \
--run_mode finetune \
--auto_trans_ckpt True \
--train_dataset /home/HwHiAiUser/mindformers/dataset/qwen_mindrecord/qwen.mindrecord" \
hccl_8p_01234567_26.205.198.97.json [0,6] 6
```


## 机器配置需求
https://github.com/QwenLM/Qwen/tree/main/recipes/finetune/deepspeed#settings-and-gpu-requirements


# 推理

### 8卡分布式启动
```
bash ./run_singlenode.sh \
"python qwen/run_qwen.py \
--config qwen/run_qwen_14b.yaml \
--run_mode predict \
--use_parallel True \
--load_checkpoint /home/HwHiAiUser/mindformers/run/ \
--auto_trans_ckpt True \
--predict_data 比较适合深度学习入门的书籍有" \
rank_table_8.json [0,8] 8
```
# FAQ

一、问题现象（附报错日志上下文）：  


二、软件版本:  
--npu-driver_23.0.rc3_linux-aarch64
--npu-firmware_6.4.0.4.220
--CANN 版本 : 7.0.0  
--Pytorch 版本: torch=2.1.0 ,torch_npu=2.1.0.post23023121  
--Python 版本 : 3.8

三、测试步骤：  
bash examples/qwen/generate_qwen_7b_ptd.sh

四、推理报错AttributeError: module 'mindspore.ops' has no attribute 'ApplyRotaryPosEmb'
  mindspore为2.2.11版本，mindformers使用rc1.0分支
  