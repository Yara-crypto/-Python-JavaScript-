# -Python-JavaScript-
一个用于计算数字资产交易收益情况的小工具，支持现货 / 合约场景的基础收益估算，包括：  - 收益率计算 - 复利模拟 - 手续费影响测算 - 分批建仓成本计算 - 简单年化收益估算  适用于学习、策略验证或个人资产记录分析。
## 一、功能介绍

在数字资产交易过程中，收益往往受到多个因素影响，例如：

- 买入均价
- 卖出价格
- 杠杆倍数
- 手续费率
- 资金费率
- 多次加仓成本

本项目实现了常见收益计算模型，帮助理解收益构成。

---

## 二、收益计算原理

### 1. 基础收益率公式


收益率 = (卖出价 - 买入价) / 买入价


### 2. 实际收益（考虑手续费）


净收益 = (卖出价 × (1 - 手续费)) - (买入价 × (1 + 手续费))


### 3. 杠杆收益估算


实际收益率 ≈ 基础收益率 × 杠杆倍数


（未考虑强平机制与维持保证金要求）

---

## 三、Python 示例代码

```python
def calculate_spot_profit(buy_price, sell_price, amount, fee_rate=0.001):
    buy_cost = buy_price * amount * (1 + fee_rate)
    sell_value = sell_price * amount * (1 - fee_rate)
    profit = sell_value - buy_cost
    roi = profit / buy_cost
    return {
        "profit": round(profit, 4),
        "roi": round(roi * 100, 2)
    }

result = calculate_spot_profit(
    buy_price=20000,
    sell_price=22000,
    amount=0.5
)

print(result)

输出示例：

{'profit': 998.0, 'roi': 9.98}
四、JavaScript 示例
function calculateSpotProfit(buyPrice, sellPrice, amount, feeRate = 0.001) {
    const buyCost = buyPrice * amount * (1 + feeRate);
    const sellValue = sellPrice * amount * (1 - feeRate);
    const profit = sellValue - buyCost;
    const roi = profit / buyCost;

    return {
        profit: profit.toFixed(4),
        roi: (roi * 100).toFixed(2) + "%"
    };
}

console.log(
    calculateSpotProfit(20000, 22000, 0.5)
);
五、复利模拟函数
def compound_growth(principal, rate, periods):
    for _ in range(periods):
        principal *= (1 + rate)
    return round(principal, 2)

print(compound_growth(10000, 0.02, 30))

适用于模拟固定收益率下的增长情况。

六、分批建仓成本计算
def average_price(orders):
    total_cost = sum(price * amount for price, amount in orders)
    total_amount = sum(amount for _, amount in orders)
    return total_cost / total_amount

orders = [
    (20000, 0.2),
    (19000, 0.3),
    (21000, 0.5)
]

print(average_price(orders))
七、API 数据接入（可选）

如果需要实时行情数据，可通过主流交易平台的公开 API 获取最新价格。

示例流程：

请求行情接口

获取最新成交价

传入计算函数

不同平台 API 文档示例：

OKX API

Binance API

Bybit API

本项目不依赖特定平台接口，可自由扩展。

八、适用场景

学习收益计算逻辑

验证简单交易策略

量化初学者练习

资产记录分析

教学演示

九、免责声明

本项目仅用于学习与研究目的。

数字资产交易具有较高风险，请在充分理解相关机制后参与市场。

十、后续可扩展方向

支持永续合约爆仓价格计算

加入资金费率模型

增加可视化图表

支持历史数据回测

Web UI 版本

欢迎 Fork / Issue / PR 交流。
