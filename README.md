# PGOT: Physics-Guided Optimal Transport for Urban Traffic Flow Forecasting

PGOT 是一个用于城市交通流量预测的新型模型框架。它显式建模了局部的物理迁移关系和全局的时空依赖关系，在多个真实交通数据集上达到了最先进的性能。

---

## 一、项目特点

- 🚦 **局部建模**：利用最优传输（Optimal Transport）理论显式建模区域间的流动关系
- 🌐 **全局建模**：引入时空 MLP 模块挖掘全局时空依赖
- 🧠 **模块清晰**：包含局部建模模块、全局 MLP 模块、门控融合模块
- 💻 **支持多数据集**：适用于 TaxiBJ、BikeNYC、TaxiNYC 等多个交通数据集
- ⚙️ **易于训练**：支持多 GPU、AMP 训练，加速大规模训练任务

---

## 二、目录结构

```
PGOT/
├── data/                # 存放交通数据 CSV 文件
├── exp/                 # 实验运行入口
│   └── exp_pgot.py
├── models/              # 模型结构定义
│   ├── pgot.py          # 主模型 PGOT
│   ├── attn.py          # 注意力与条件注意力
│   ├── encoder.py       # 编码器结构
│   ├── embed.py         # 时空嵌入模块
│   └── optionT.py       # 最优传输 OT 模块
├── utils/               # 工具库
├── main.py              # 主训练与测试脚本
└── requirements.txt     # Python 依赖
```

---

## 三、环境配置

```bash
Python >= 3.8
PyTorch >= 1.10
numpy
pandas
```
安装方式：
```bash
pip install -r requirements.txt
```

---

## 四、运行示例

以 Bike1NYC 数据集为例：
```bash
python main.py \
--data Bike1NYC \
--data_path Bike1NYC.csv \
--seq_len 12 --label_len 0 --pred_len 12 \
--l 16  --w 8 \
--train_epochs 15
```

---

## 五、参数说明

| 参数名 | 含义 |
|--------|------|
| `--seq_len` | 输入的历史时间步 |
| `--pred_len` | 预测未来的时间步数 |
| `--l`, `--w` | 输入空间的划分维度（长、宽） |
| `--d_model` | 模型嵌入维度 |
| `--e_layers` | 编码器层数 |
| `--dropout` | Dropout 比例 |
| `--use_gpu` | 是否使用 GPU |

---

## 六、支持的数据集

| 名称 | 城市 | 描述 |
|------|------|------|
| TaxiBJ   | 北京 | 出租车交通流量网格数据 |
| TaxiNYC  | 纽约 | 纽约出租车流量 |
| Bike1NYC | 纽约 | 公共自行车租赁数据 |
| Bike2NYC | 纽约 | 更高质量版本的 BikeNYC |

将数据 CSV 文件放置在 `./data/` 目录下即可。

---
