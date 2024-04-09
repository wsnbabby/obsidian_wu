```python
import mindspore as ms
from mindformers import AutoConfig, AutoModel, AutoTokenizer
import time

# 指定图模式，指定使用训练卡id
ms.set_context(mode=ms.GRAPH_MODE, device_target="Ascend", device_id=0)
tokenizer = AutoTokenizer.from_pretrained('/home/HwHiAiUser/model/chatglm3-6b_ms')
model = AutoModel.from_pretrained('/home/HwHiAiUser/model/chatglm3-6b_ms')


```


用户：hello

ChatGLM：Traceback (most recent call last):
  File "/home/HwHiAiUser/mindformers/my_scripts/my_cli_demo.py", line 57, in <module>
    main()
  File "/home/HwHiAiUser/mindformers/my_scripts/my_cli_demo.py", line 43, in main
    for response, history, past_key_values in model.stream_chat(tokenizer, query, history=history, top_p=1,
  File "/root/miniconda3/envs/mindspore_py39/lib/python3.9/site-packages/mindspore/nn/cell.py", line 387, in __getattr__
    raise AttributeError("The '{}' object has no attribute '{}'.".format(type(self).__name__, name))
AttributeError: The 'ChatGLM2ForConditionalGeneration' object has no attribute 'stream_chat'.
(mindspore_py39) [root@bms-c551 mindformers]# timed out waiting for input: auto-logout