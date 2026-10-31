# 酒店预订取消行为与渠道分析｜Python EDA

基于 **Hotel Booking Demand** 的 119,390 条酒店预订记录，使用 Python 分析两类酒店的订单取消情况，重点比较预订提前期、入住月份、渠道和客户行为，并结合订单量与名义房费确定重点监控对象。

**技术：** Python · Pandas · NumPy · Matplotlib · Seaborn · Spearman 相关分析  
**样本：** 原始 119,390 条，清洗后 119,210 条  
**完整分析：** [打开 Jupyter Notebook](notebooks/hotel_booking_cancellation_eda.ipynb)

## 项目工作

- **数据清洗与指标构建：** 检查缺失值、零客人订单、零晚住宿及房价异常，剔除 180 条零客人记录；生成入住日期、季节、提前期分组、订单名义房费等分析字段。
- **多维探索：** 从酒店类型、月份、提前预订时间、ADR、渠道、客源国和预订行为等维度开展分组统计与可视化，并使用 Spearman 相关矩阵检查数值变量关联。
- **渠道诊断：** 结合取消率、订单数量、取消订单名义房费比较主要市场细分，识别优先关注的渠道与预订群体。
- **运营建议：** 针对 Online TA、长提前期订单和 Groups 团队订单，提出分层监控、入住前确认与库存管理思路。

## 主要发现

| 维度 | 分析结果 |
|---|---|
| 酒店类型 | 城市酒店取消率 **41.8%**，度假酒店 **27.8%** |
| 提前预订 | 提前 **180 天以上**订单取消率 **57.0%**，提前 **7 天内**为 **9.6%** |
| Online TA | 取消率 **36.8%**，占取消订单名义房费约 **61.1%** |
| Groups | 市场细分中的取消率 **61.1%** |
| 特殊请求 | 无特殊请求订单取消率 **47.8%**，有至少一项特殊请求约 **21.8%** |
| 金额规模 | 取消订单对应约 **1,673 万**名义房费，占全部订单名义房费约 **39.2%** |

## 核心图表

**两类酒店订单与取消情况**

![酒店类型取消情况](assets/01_hotel_cancellation.png)

**预订提前期与取消率**

![预订提前期分析](assets/02_lead_time.png)

**渠道规模、取消率与取消订单名义房费**

![渠道对比](assets/03_channel_risk.png)

**数值变量相关矩阵**

![相关矩阵](assets/04_spearman.png)

## 运行方法

1. 从 [Hotel Booking Demand（Kaggle）](https://www.kaggle.com/datasets/jessemostipak/hotel-booking-demand) 下载 `hotel_bookings.csv`，放到 `data/` 文件夹。
2. 在本项目根目录安装依赖：`python -m pip install -r requirements.txt`。
3. 打开 `notebooks/hotel_booking_cancellation_eda.ipynb`，按顺序运行代码。

```text
hotel-booking-cancellation-eda/
├── README.md
├── notebooks/
│   └── hotel_booking_cancellation_eda.ipynb
├── assets/
│   ├── 01_hotel_cancellation.png
│   ├── 02_lead_time.png
│   ├── 03_channel_risk.png
│   └── 04_spearman.png
├── data/
│   └── README.md
├── requirements.txt
└── .gitignore
```

## 数据来源

- [Hotel Booking Demand（Kaggle）](https://www.kaggle.com/datasets/jessemostipak/hotel-booking-demand)
- António, N., de Almeida, A., & Nunes, L. (2019). *Hotel booking demand datasets*. Data in Brief, 22, 41–49. [DOI](https://doi.org/10.1016/j.dib.2018.11.126)

## 数据口径与局限

- 取消率按 `is_canceled=1` 的订单记录占比计算；名义房费按 `ADR × 住宿晚数` 估算，**并非酒店实际损失**。
- 数据来自 2015–2017 年的两家酒店；分析基于观察数据，所提出的运营措施尚未经过实际干预验证。
- 复现时需自行下载原始 CSV；仓库不包含该数据文件。
