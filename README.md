# LightWing
Intelligent Manufacturing/
├── checkpoints/          # 训练产生的模型权重（预训练与 SFT）
├── model/                # 模型核心架构与配置文件
│   ├── model_im.py       # IMR-LLM 模型定义
│   ├── tokenizer.json    # 分词器核心配置
│   └── tokenizer_config.json
├── trainer/              # 训练辅助工具
│   └── utils.py          # 包含分布式初始化与日志工具
├── train_pretrain.py # 预训练主程序
├── train_sft.py      # 指令微调（SFT）程序
├── make_bin.py       # 语料转化为二进制预训练格式
└── eval_sft.py       # SFT 效果评估
└── LightWing_IMR_10000_Full.jsonl # 生成的 SFT 指令数据集

环境准备
确保环境中安装了 torch, transformers, tokenizers 以及 tqdm 等依赖。
数据预处理
首先，需要将原始文本语料（im_pretrain_corpus.txt）转换为模型可读的二进制格式：
python make_bin.py
模型预训练
基于工业语料库进行基础语义学习：
python train_pretrain.py
指令微调 (SFT)
使用生成的 10,000 条 LightWing_IMR 任务数据集进行微调，使模型具备离散图分析与代码生成能力：
python train_sft.py
推理与评估
运行评估脚本验证模型在工业任务指令下的表现：
python eval_sft.py
