# [下载](https://modelscope.cn/docs/%E6%A8%A1%E5%9E%8B%E7%9A%84%E4%B8%8B%E8%BD%BD)

## 使用Library下载模型
```python
from modelscope.models import Model model = Model.from_pretrained('damo/nlp_xlmr_named-entity-recognition_viet-ecommerce-title', revision='v1.0.1') # revision为可选参数，不指定版本会取模型默认版本，默认版本，默认版本为ModelScope library发布前最后一个版本 # 如何得到发布时间 # import modelscope # print(modelscope.version.__release_datetime__) #model = Model.from_pretrained('damo/nlp_structbert_word-segmentation_chinese-base')
```

## 使用Library Hub下载模型

```python
# 您可以使用modelscope modelhub从 repos 创建、删除、更新和检索信息。您还可以从 repos 下载文件或将它们集成到您的库中，并且可指定下载模型的地址。

from modelscope.hub.snapshot_download import snapshot_download model_dir = snapshot_download('damo/nlp_xlmr_named-entity-recognition_viet-ecommerce-title', cache_dir='path/to/local/dir', revision='v1.0.1')
```

```python
# 您也可以使用modelscope modelhub从repos中指定下载单个文件。

from modelscope.hub.file_download import model_file_download model_dir = model_file_download(model_id='AI-ModelScope/rwkv-4-world',file_path='RWKV-4-World-CHNtuned-7B-v1-20230709-ctx4096.pth',revision='v1.0.0')
```

