# 快速在Linux上部署大型中文对话模型(类似GPT)
>基于Chinese-Alpaca-Plus-7B官方项目改编：https://github.com/ymcui/Chinese-LLaMA-Alpaca  
>官方项目中除了Chinese-Alpaca-Plus-7B(14G)外还有多种型号  
>CPU上运行要有32G内存；GPU上运行要有20G内存  
## Chinese-Alpaca-Plus-7B介绍
>类似GPT一样有对话交互能力的大型语言模型  
>2022年facebook发布LLaMA-7B模型，此后中文团队训练出中文模型补丁  
>中文模型只是部分权重，原LLaMA-7B模型、Chinese-LLaMA-Plus-7B补丁、Chinese-Alpaca-Plus-7B补丁要合并后才可使用  
### 项目介绍
>本项目记录了在Linux上部署Chinese-Alpaca-Plus-7B模型的流程  
>如果直接下载合并好的chinese_alpaca_plus_7b_hf模型(推荐)，可直接使用模型，详见(*，直接下载chinese_alpaca_plus_7b_hf)  
### 1，环境：linux
>torch==1.12.0：https://pytorch.org/get-started/previous-versions/  
>```
>pip install transformers sentencepiece -i https://pypi.doubanio.com/simple  
>pip install git+https://github.com/huggingface/peft  
>```
### 2，下载llama_hf(13G)
>huggingface地址：https://huggingface.co/decapoda-research/llama-7b-hf/tree/main  
>```
>sudo apt-get install git-lfs：安装git lfs  
>git lfs install：启用lfs。不使用lfs无法下载大文件  
>git clone https://huggingface.co/decapoda-research/llama-7b-hf：下载模型  
>```
### 3，下载chinese_llama_plus_lora_7b(790M)
>百度网盘：https://pan.baidu.com/s/1zvyX9FN-WSRDdrtMARxxfw?pwd=2gtr  
>google网盘(外网)：https://drive.google.com/uc?id=1N97m3rBj-rp-J1X8rgRfluyomEscfAq0&export=download  
### 4，下载chinese_alpaca_plus_lora_7b(1.1G)
>百度网盘：https://pan.baidu.com/s/12tjjxmDWwLBM8Tj_7FAjHg?login_type=qzone&pwd=32hc&_at_=1683274834793  
>google网盘(外网)：https://drive.google.com/uc?id=1EDcTmq6tDmRxqarpapdyDGBE9opY0zrB&export=download  
### 5，merge_model.py
>合并llama_7b_hf、chinese_llama_plus_lora_7b、chinese_alpaca_plus_lora_7b为chinese_alpaca_plus_7b_hf(14G)  
>```
>python merge_model.py --base_model /TRAINING_CACHE/llama_7b_hf --lora_model /TRAINING_CACHE/chinese_llama_plus_lora_7b,/TRAINING_CACHE/chinese_alpaca_plus_lora_7b --output_type huggingface --output_dir /TRAINING_CACHE/chinese_alpaca_plus_7b_hf  
>--offload_dir cache：如果内存不够可使用缓存，命令中加上缓存路径  
>```
### *，直接下载chinese_alpaca_plus_7b_hf
>使用huggingface上别人合并好上传的chinese_alpaca_plus_7b_hf模型，若不能使用，可以再找找其他的  
>huggingface地址：https://huggingface.co/shibing624/chinese-alpaca-plus-7b/tree/main  
>```
>sudo apt-get install git-lfs：安装git lfs  
>git lfs install：启用lfs。不使用lfs无法下载大文件  
>git clone https://huggingface.co/shibing624/chinese-alpaca-plus-7b：下载模型  
>```
### 6，inference_hf.py
>启动模型(不具备记忆功能)  
>交互式：  
>```
>python inference_hf.py --base_model /TRAINING_CACHE/chinese_alpaca_plus_7b_hf --with_prompt --interactive  
>```
>读取文本式：  
>```
>python inference_hf.py --base_model /TRAINING_CACHE/chinese_alpaca_plus_7b_hf --with_prompt --data_file data.txt  
>--data_file：待预测数据，按行读取  
>```
### 更多模型和功能
>请参考原项目：https://github.com/ymcui/Chinese-LLaMA-Alpaca  
### 其他
>github链接：https://github.com/TWK2022/ChineseAlpacaPlus7b  
>学习笔记：https://github.com/TWK2022/notebook  
>邮箱：1024565378@qq.com  