# defillama-tvl-analysis
Comparative analysis of Uniswap and PancakeSwap TVL using DeFiLlama data
# 🧠 DeFi TVL Analysis — Uniswap vs PancakeSwap

### A comparative data visualization using DeFiLlama API & Python

---

## 🌍 Overview

This project analyzes and compares the **Total Value Locked (TVL)** between two leading decentralized exchanges — **Uniswap (Ethereum)** and **PancakeSwap (BNB Chain)** — using data fetched directly from the **DeFiLlama API**.

It serves as an example of how open DeFi data can be leveraged to generate insights about liquidity trends, user behavior, and cross-chain growth dynamics.

---

## ⚙️ Tools & Libraries

- 🐍 **Python**
- 📡 **DeFiLlama API**
- 📊 **pandas**
- 📈 **matplotlib**
- ☁️ **Google Colab**

---

## 💻 Code Example

```python
import requests
import pandas as pd
import matplotlib.pyplot as plt

protocol_1 = "uniswap"
protocol_2 = "pancakeswap"

def get_tvl_data(protocol):
    url = f"https://api.llama.fi/protocol/{protocol}"
    data = requests.get(url).json()
    df = pd.DataFrame(data["tvl"])
    df["date"] = pd.to_datetime(df["date"], unit="s")
    df["protocol"] = data["name"]
    return df

tvl1 = get_tvl_data(protocol_1)
tvl2 = get_tvl_data(protocol_2)
merged = pd.concat([tvl1, tvl2])

plt.figure(figsize=(10,6))
for p, d in merged.groupby("protocol"):
    plt.plot(d["date"], d["totalLiquidityUSD"], label=p)
plt.title("DeFi TVL Comparison: Uniswap vs PancakeSwap")
plt.xlabel("Date")
plt.ylabel("TVL (USD)")
plt.legend()
plt.grid(True)
plt.tight_layout()
plt.show()
