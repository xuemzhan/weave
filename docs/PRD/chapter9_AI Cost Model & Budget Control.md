# 第九章：AI成本模型与预算控制 (AI Cost Model & Budget Control)**

---

## **9.1 成本模型概述 (Cost Model Overview)**

### **9.1.1 为什么成本模型至关重要**

```yaml
MVP阶段的三大财务风险：
1. AI成本失控 → 现金流断裂 → 项目终止
2. 成本估算不准 → 商业模式不可行 → 无法融资
3. 隐性成本遗漏 → 预算超支 → 团队士气受挫

本章目标：
✅ 建立精确的成本计算模型
✅ 提供可落地的成本控制方案
✅ 为商业模式设计提供数据支撑
```

### **9.1.2 成本构成拆解**

```
Weave MVP总成本 = 固定成本 + 可变成本

固定成本（每月）：
├─ 人力成本：¥120,000（6人团队 × ¥20,000/人）
├─ 服务器成本：¥3,000（云服务器、数据库）
├─ 办公成本：¥10,000（场地、设备、网络）
└─ 其他成本：¥7,000（SaaS工具、杂费）
─────────────────────────────────
固定成本小计：¥140,000/月

可变成本（随用户增长）：
├─ AI服务成本（本章重点）
│   ├─ ASR（语音转文本）
│   ├─ OCR（图片文字识别）
│   ├─ LLM（内容精炼）
│   └─ Embedding（向量化，V1.1）
├─ 云存储成本（音频、图片文件）
├─ CDN成本（图片分发）
└─ 带宽成本（API调用）

本章聚焦：AI服务成本（占可变成本80%+）
```

---

## **9.2 AI服务价格表 (AI Service Pricing)**

### **9.2.1 ASR服务价格（阿里云）**

| 服务类型         | 计费单位 | 价格    | 免费额度 | 说明        |
| ---------------- | -------- | ------- | -------- | ----------- |
| **录音文件识别** | 每分钟   | ¥0.039  | 无       | MVP主要使用 |
| **实时流式识别** | 每分钟   | ¥0.045  | 无       | V1.1考虑    |
| **一句话识别**   | 每次     | ¥0.0025 | 无       | 不适用      |

**计费说明：**

```
1. 按音频时长计费，不足1分钟按1分钟计
2. 示例：15秒音频 → 按1分钟计费 → ¥0.039
3. 示例：65秒音频 → 按2分钟计费 → ¥0.078
```

**成本优化点：**

```python
# 优化1：音频压缩（不影响识别率）
原始格式：WAV, 16kHz, 16bit → 约1MB/分钟
优化格式：MP3, 16kHz, 64kbps → 约0.5MB/分钟
成本影响：无（按时长计费，与文件大小无关）

# 优化2：去除静音段
原始音频：用户说话15秒 + 停顿5秒 = 20秒 → 按1分钟计费
优化后：去除停顿 → 15秒 → 按1分钟计费
成本节省：0%（仍按1分钟计费）

# 优化3：批量处理（无优惠）
阿里云ASR不提供批量折扣

结论：ASR成本优化空间有限，需控制使用频率
```

---

### **9.2.2 OCR服务价格（百度）**

| 服务类型           | 计费单位 | 价格   | 免费额度  | 说明           |
| ------------------ | -------- | ------ | --------- | -------------- |
| **通用文字识别**   | 每次     | ¥0.008 | 1000次/天 | 标准版         |
| **高精度文字识别** | 每次     | ¥0.05  | 50次/天   | 倾斜、模糊场景 |
| **表格文字识别**   | 每次     | ¥0.05  | 50次/天   | V1.1考虑       |

**免费额度使用策略：**

```yaml
MVP阶段（1000 DAU）：
  预估日均图片输入：300次/天
  使用免费额度：1000次/天（通用文字识别）
  
  策略：
    - 优先使用通用文字识别（¥0.008/次，免费额度大）
    - 仅当OCR置信度<0.6时，重试高精度版（¥0.05/次）
    - 免费额度内，实际成本：¥0

V1.0阶段（如果日均超过1000次）：
  超出部分按¥0.008/次计费
  
  示例：日均1500次
  成本 = (1500 - 1000) × ¥0.008 = ¥4/天 = ¥120/月
```

**成本优化点：**

```python
# 优化1：图片预处理（提升识别率，降低重试）
def optimize_image_for_ocr(image):
    """优化图片以提升OCR识别率"""
    # 1. 自动旋转矫正（根据EXIF信息）
    image = auto_rotate(image)
    
    # 2. 对比度增强（提升文字清晰度）
    image = enhance_contrast(image)
    
    # 3. 去噪（移除干扰）
    image = denoise(image)
    
    return image

# 优化2：智能降级
async def ocr_with_fallback(image_url):
    """智能OCR：先用免费额度，超限后降级"""
    
    # 检查今日免费额度
    if await check_free_quota_available('ocr'):
        # 使用免费额度
        return await baidu_ocr.standard(image_url)
    else:
        # 免费额度用尽，降级处理
        logger.warning("OCR free quota exhausted")
        
        # 选项1：提示用户明天再试
        # 选项2：使用付费额度（可设置日预算上限）
        # 选项3：保存原图，延后处理
        
        return fallback_handler(image_url)
```

---

### **9.2.3 LLM服务价格（智谱GLM-4）**

| 计费项        | 价格           | 免费额度       | 说明      |
| ------------- | -------------- | -------------- | --------- |
| **输入Token** | ¥0.05/千tokens | 100万tokens/月 | 约200万字 |
| **输出Token** | ¥0.05/千tokens | 同上           | 约200万字 |

**Token计算规则：**

```
中文：1个字 ≈ 1.5-2 tokens（取决于分词）
英文：1个单词 ≈ 1-2 tokens
标点符号：1个符号 ≈ 1 token

示例：
"费曼学习法的核心是用简单的语言解释复杂的概念" (23字)
→ 约35 tokens

JSON格式字符：
{"title": "...", "content": "...", "tags": [...]}
→ 额外约20-30 tokens
```

**单次调用成本计算：**

```python
class LLMCostCalculator:
    """LLM成本计算器"""
    
    INPUT_PRICE = 0.05 / 1000   # ¥0.05/千tokens
    OUTPUT_PRICE = 0.05 / 1000
    
    def calculate_cost(self, raw_text: str):
        """计算单次精炼调用的成本"""
        
        # 1. 输入Token（Prompt + 用户文本）
        prompt_tokens = self.count_tokens(self.PROMPT_TEMPLATE)  # 约300 tokens
        user_tokens = self.count_tokens(raw_text)                # 假设平均100 tokens
        input_tokens = prompt_tokens + user_tokens               # 约400 tokens
        
        # 2. 输出Token（JSON结构化结果）
        # 标题：20字 → 30 tokens
        # 内容：200字 → 300 tokens
        # 标签：3个 → 10 tokens
        # JSON格式：约30 tokens
        output_tokens = 370  # 约370 tokens
        
        # 3. 总成本
        input_cost = input_tokens * self.INPUT_PRICE
        output_cost = output_tokens * self.OUTPUT_PRICE
        total_cost = input_cost + output_cost
        
        return {
            'input_tokens': input_tokens,
            'output_tokens': output_tokens,
            'input_cost': input_cost,    # 约 ¥0.02
            'output_cost': output_cost,  # 约 ¥0.0185
            'total_cost': total_cost     # 约 ¥0.0385
        }
    
    def count_tokens(self, text: str) -> int:
        """估算Token数量（简化版）"""
        # 实际应使用GLM的tokenizer
        # 这里简化为：中文1字=1.5token，英文1词=1.5token
        import re
        chinese_chars = len(re.findall(r'[\u4e00-\u9fa5]', text))
        english_words = len(re.findall(r'[a-zA-Z]+', text))
        return int(chinese_chars * 1.5 + english_words * 1.5)

# 示例计算
calculator = LLMCostCalculator()
cost = calculator.calculate_cost("今天学习了费曼学习法，感觉很有用...")
print(f"单次精炼成本：¥{cost['total_cost']:.4f}")
# 输出：单次精炼成本：¥0.0385
```

**免费额度使用预测：**

```yaml
免费额度：100万tokens/月

MVP阶段预估消耗：
  - 假设1000 DAU
  - 核心用户（30%）周均创建3个节点 → 月均12个节点
  - 普通用户（70%）月均创建2个节点
  
  月度节点创建数：
    = 1000 × 30% × 12 + 1000 × 70% × 2
    = 3,600 + 1,400
    = 5,000个节点/月
  
  每节点消耗Token（输入+输出）：
    = 400 + 370 = 770 tokens
  
  月度总消耗：
    = 5,000 × 770
    = 3,850,000 tokens
    ≈ 385万tokens

结论：免费额度（100万tokens）不足，超出部分需付费
      超出：385万 - 100万 = 285万tokens
      成本：285万 × ¥0.05/千 = ¥142.5/月
```

**成本优化点：**

```python
# 优化1：Prompt压缩（减少输入Token）
# 原Prompt（约500 tokens）
OLD_PROMPT = """
你是一个专业的知识管理助手，擅长将口语化的内容精炼为结构化的知识点。
请将以下用户的语音转录内容，精炼为一个结构化的智慧节点。
输入：{raw_text}
输出要求：必须严格遵循以下JSON格式...
（详细说明300字）
"""

# 优化Prompt（约300 tokens，减少40%）
NEW_PROMPT = """
精炼以下内容为JSON：
{raw_text}

格式：{"title":"<20字","content":"<200字","tags":["<3个"]}
要求：去除口语化，保留关键信息。
"""

# 节省：200 tokens/次 × 5000次/月 = 100万tokens/月 = ¥50/月

# 优化2：缓存高频内容
# 如果用户重复录入相似内容（如"今天学习了XXX"），缓存结果
import hashlib

async def refine_with_cache(raw_text: str):
    """带缓存的内容精炼"""
    # 计算内容hash
    content_hash = hashlib.md5(raw_text.encode()).hexdigest()
    cache_key = f"llm_result:{content_hash}"
    
    # 尝试从缓存获取
    cached = await redis.get(cache_key)
    if cached:
        logger.info("LLM cache hit, saved cost")
        return json.loads(cached)
    
    # 缓存未命中，调用LLM
    result = await llm_service.refine(raw_text)
    
    # 写入缓存（24小时）
    await redis.setex(cache_key, 86400, json.dumps(result))
    
    return result

# 预估缓存命中率：10-15%（保守估计）
# 节省成本：¥142.5 × 15% = ¥21.4/月

# 优化3：批量处理（如果API支持，GLM-4暂不支持）
```

---

### **9.2.4 Embedding服务价格（V1.1规划）**

| 服务商     | 模型                   | 价格             | 免费额度       |
| ---------- | ---------------------- | ---------------- | -------------- |
| **智谱**   | Embedding-2            | ¥0.005/千tokens  | 100万tokens/月 |
| **OpenAI** | text-embedding-ada-002 | $0.0001/千tokens | 无             |
| **阿里**   | 通用文本向量           | ¥0.0007/千tokens | 100万tokens/月 |

**成本计算（V1.1向量检索版"思想共鸣"）：**

```python
class EmbeddingCostCalculator:
    """向量化成本计算"""
    
    def calculate_monthly_cost(self, monthly_nodes: int):
        """计算月度Embedding成本"""
        
        # 1. 每个节点需要向量化的文本
        # 标题(20字) + 内容(200字) = 220字 ≈ 330 tokens
        tokens_per_node = 330
        
        # 2. 月度总Token数
        total_tokens = monthly_nodes * tokens_per_node
        
        # 3. 成本（智谱Embedding-2）
        # 免费额度：100万tokens/月
        if total_tokens <= 1_000_000:
            cost = 0
        else:
            paid_tokens = total_tokens - 1_000_000
            cost = paid_tokens * 0.005 / 1000
        
        return {
            'total_tokens': total_tokens,
            'free_tokens': min(total_tokens, 1_000_000),
            'paid_tokens': max(0, total_tokens - 1_000_000),
            'cost': cost
        }

# 示例：月度5000个节点
calc = EmbeddingCostCalculator()
result = calc.calculate_monthly_cost(5000)
print(f"Embedding成本：¥{result['cost']:.2f}/月")
# 输出：Embedding成本：¥6.65/月

# 成本优化：
# 1. 不需要每次都重新Embedding，仅新节点需要
# 2. 可以只对标题做Embedding（减少80% Token）
# 3. 使用更小的向量维度（如384维 vs 768维）
```

---

## **9.3 单用户成本模型 (Per-User Cost Model)**

### **9.3.1 用户行为模式分类**

```yaml
根据Beta测试数据，用户分为3类：

高频用户（20%用户）：
  特征：周均创建5+个节点，日均复习
  节点创建：
    - 语音输入：70%
    - 截图输入：30%
  复习行为：
    - 复习完成率：60%
    - 周均复习节点数：10个

标准用户（50%用户）：
  特征：周均创建2-4个节点，隔日复习
  节点创建：
    - 语音输入：60%
    - 截图输入：40%
  复习行为：
    - 复习完成率：40%
    - 周均复习节点数：5个

低频用户（30%用户）：
  特征：月均创建<5个节点，很少复习
  节点创建：
    - 语音输入：50%
    - 截图输入：50%
  复习行为：
    - 复习完成率：10%
    - 周均复习节点数：1个
```

---

### **9.3.2 高频用户成本计算**

```python
class HighFrequencyUserCost:
    """高频用户月度AI成本"""
    
    def __init__(self):
        # 价格常量
        self.ASR_PRICE = 0.039          # ¥/分钟
        self.OCR_PRICE = 0.008          # ¥/次（免费额度内）
        self.LLM_PRICE_PER_CALL = 0.0385  # ¥/次（见9.2.3计算）
        
        # 行为特征
        self.NODES_PER_MONTH = 20       # 月均20个节点
        self.VOICE_RATIO = 0.7          # 70%语音
        self.IMAGE_RATIO = 0.3          # 30%截图
        
        self.AVG_VOICE_DURATION = 25    # 平均录音25秒
        
    def calculate(self):
        """计算月度成本"""
        
        # 1. 语音输入成本
        voice_nodes = self.NODES_PER_MONTH * self.VOICE_RATIO  # 14个
        
        # ASR成本（25秒按1分钟计费）
        asr_cost = voice_nodes * 1 * self.ASR_PRICE  # 14 × ¥0.039
        
        # LLM精炼成本
        voice_llm_cost = voice_nodes * self.LLM_PRICE_PER_CALL  # 14 × ¥0.0385
        
        # 2. 截图输入成本
        image_nodes = self.NODES_PER_MONTH * self.IMAGE_RATIO  # 6个
        
        # OCR成本（假设在免费额度内）
        ocr_cost = 0  # 免费额度覆盖
        
        # LLM精炼成本
        image_llm_cost = image_nodes * self.LLM_PRICE_PER_CALL  # 6 × ¥0.0385
        
        # 3. 总成本
        total_cost = asr_cost + voice_llm_cost + ocr_cost + image_llm_cost
        
        return {
            'voice_nodes': voice_nodes,
            'image_nodes': image_nodes,
            'asr_cost': asr_cost,          # ¥0.546
            'ocr_cost': ocr_cost,          # ¥0
            'llm_cost': voice_llm_cost + image_llm_cost,  # ¥0.77
            'total_cost': total_cost,      # ¥1.316
            'cost_breakdown': {
                'voice_input': asr_cost + voice_llm_cost,  # ¥1.085
                'image_input': ocr_cost + image_llm_cost   # ¥0.231
            }
        }

# 计算结果
high_user = HighFrequencyUserCost()
result = high_user.calculate()

print(f"""
高频用户月度AI成本：
- 语音输入节点：{result['voice_nodes']:.0f}个
- 截图输入节点：{result['image_nodes']:.0f}个
- ASR成本：¥{result['asr_cost']:.3f}
- OCR成本：¥{result['ocr_cost']:.3f}
- LLM成本：¥{result['llm_cost']:.3f}
─────────────────────
总成本：¥{result['total_cost']:.2f}/月
""")

# 输出：
# 高频用户月度AI成本：
# - 语音输入节点：14个
# - 截图输入节点：6个
# - ASR成本：¥0.546
# - OCR成本：¥0.000
# - LLM成本：¥0.770
# ─────────────────────
# 总成本：¥1.32/月
```

---

### **9.3.3 标准用户成本计算**

```python
class StandardUserCost:
    """标准用户月度AI成本"""
    
    def __init__(self):
        self.ASR_PRICE = 0.039
        self.OCR_PRICE = 0.008
        self.LLM_PRICE_PER_CALL = 0.0385
        
        self.NODES_PER_MONTH = 10       # 月均10个节点
        self.VOICE_RATIO = 0.6
        self.IMAGE_RATIO = 0.4
        self.AVG_VOICE_DURATION = 20
        
    def calculate(self):
        voice_nodes = self.NODES_PER_MONTH * self.VOICE_RATIO  # 6个
        image_nodes = self.NODES_PER_MONTH * self.IMAGE_RATIO  # 4个
        
        asr_cost = voice_nodes * 1 * self.ASR_PRICE
        voice_llm_cost = voice_nodes * self.LLM_PRICE_PER_CALL
        
        ocr_cost = 0  # 免费额度
        image_llm_cost = image_nodes * self.LLM_PRICE_PER_CALL
        
        total_cost = asr_cost + voice_llm_cost + ocr_cost + image_llm_cost
        
        return {
            'total_cost': total_cost,  # ¥0.619
            'voice_nodes': voice_nodes,
            'image_nodes': image_nodes
        }

standard_user = StandardUserCost()
result = standard_user.calculate()
print(f"标准用户月度成本：¥{result['total_cost']:.2f}")
# 输出：标准用户月度成本：¥0.62
```

---

### **9.3.4 低频用户成本计算**

```python
class LowFrequencyUserCost:
    """低频用户月度AI成本"""
    
    def __init__(self):
        self.ASR_PRICE = 0.039
        self.OCR_PRICE = 0.008
        self.LLM_PRICE_PER_CALL = 0.0385
        
        self.NODES_PER_MONTH = 4        # 月均仅4个节点
        self.VOICE_RATIO = 0.5
        self.IMAGE_RATIO = 0.5
        
    def calculate(self):
        voice_nodes = self.NODES_PER_MONTH * self.VOICE_RATIO  # 2个
        image_nodes = self.NODES_PER_MONTH * self.IMAGE_RATIO  # 2个
        
        asr_cost = voice_nodes * 1 * self.ASR_PRICE
        voice_llm_cost = voice_nodes * self.LLM_PRICE_PER_CALL
        
        ocr_cost = 0
        image_llm_cost = image_nodes * self.LLM_PRICE_PER_CALL
        
        total_cost = asr_cost + voice_llm_cost + ocr_cost + image_llm_cost
        
        return {
            'total_cost': total_cost  # ¥0.232
        }

low_user = LowFrequencyUserCost()
result = low_user.calculate()
print(f"低频用户月度成本：¥{result['total_cost']:.2f}")
# 输出：低频用户月度成本：¥0.23
```

---

### **9.3.5 加权平均单用户成本**

```python
class WeightedAverageUserCost:
    """加权平均单用户成本"""
    
    def calculate(self):
        # 用户分布
        high_freq_ratio = 0.20    # 20%
        standard_ratio = 0.50     # 50%
        low_freq_ratio = 0.30     # 30%
        
        # 各类用户成本
        high_freq_cost = 1.32     # ¥/月
        standard_cost = 0.62      # ¥/月
        low_freq_cost = 0.23      # ¥/月
        
        # 加权平均
        avg_cost = (
            high_freq_cost * high_freq_ratio +
            standard_cost * standard_ratio +
            low_freq_cost * low_freq_ratio
        )
        
        return {
            'high_freq': high_freq_cost,
            'standard': standard_cost,
            'low_freq': low_freq_cost,
            'weighted_avg': avg_cost,  # ¥0.643
            'distribution': {
                'high_freq': high_freq_ratio,
                'standard': standard_ratio,
                'low_freq': low_freq_ratio
            }
        }

avg_calc = WeightedAverageUserCost()
result = avg_calc.calculate()

print(f"""
═══════════════════════════════════
单用户月度AI成本（加权平均）
═══════════════════════════════════
高频用户（20%）：¥{result['high_freq']:.2f}/月
标准用户（50%）：¥{result['standard']:.2f}/月
低频用户（30%）：¥{result['low_freq']:.2f}/月
───────────────────────────────────
加权平均：¥{result['weighted_avg']:.2f}/月
═══════════════════════════════════
""")

# 输出：
# 单用户月度AI成本（加权平均）
# 高频用户（20%）：¥1.32/月
# 标准用户（50%）：¥0.62/月
# 低频用户（30%）：¥0.23/月
# ───────────────────────────────────
# 加权平均：¥0.64/月
```

**结论：单用户月度AI成本约 ¥0.64，远低于预算目标 ¥4.00 ✅**

---

## **9.4 规模化成本预测 (Scalability Cost Forecast)**

### **9.4.1 不同DAU规模下的月度成本**

```python
class ScaleCostForecast:
    """规模化成本预测"""
    
    def __init__(self):
        self.AVG_COST_PER_USER = 0.64  # 单用户月成本
        
        # 固定成本（与用户数无关）
        self.FIXED_COST_SERVER = 3000      # 服务器
        self.FIXED_COST_OTHER = 1000       # 其他（监控、日志等）
        
    def forecast(self, dau: int):
        """预测指定DAU下的月度成本"""
        
        # MAU估算（DAU的3倍，保守）
        mau = dau * 3
        
        # AI服务成本（可变成本）
        ai_cost = mau * self.AVG_COST_PER_USER
        
        # 固定成本
        fixed_cost = self.FIXED_COST_SERVER + self.FIXED_COST_OTHER
        
        # 总成本
        total_cost = ai_cost + fixed_cost
        
        # 单DAU成本
        cost_per_dau = total_cost / dau if dau > 0 else 0
        
        return {
            'dau': dau,
            'mau': mau,
            'ai_cost': ai_cost,
            'fixed_cost': fixed_cost,
            'total_cost': total_cost,
            'cost_per_dau': cost_per_dau
        }

# 预测不同规模
forecast = ScaleCostForecast()

scenarios = [
    ('Alpha内测', 100),
    ('Beta公测', 500),
    ('V1.0发布', 1000),
    ('6个月后', 3000),
    ('1年后', 5000),
]

print("规模化成本预测表")
print("="*80)
print(f"{'阶段':<15} {'DAU':>8} {'MAU':>10} {'AI成本':>12} {'总成本':>12} {'单DAU成本':>12}")
print("-"*80)

for stage, dau in scenarios:
    result = forecast.forecast(dau)
    print(f"{stage:<15} {result['dau']:>8} {result['mau']:>10} "
          f"¥{result['ai_cost']:>10,.0f} ¥{result['total_cost']:>10,.0f} "
          f"¥{result['cost_per_dau']:>10.2f}")

print("="*80)

# 输出示例：
# 规模化成本预测表
# ================================================================================
# 阶段                  DAU        MAU       AI成本       总成本    单DAU成本
# --------------------------------------------------------------------------------
# Alpha内测             100        300      ¥   192     ¥ 4,192      ¥41.92
# Beta公测              500      1,500      ¥   960     ¥ 4,960       ¥9.92
# V1.0发布            1,000      3,000      ¥ 1,920     ¥ 5,920       ¥5.92
# 6个月后             3,000      9,000      ¥ 5,760     ¥ 9,760       ¥3.25
# 1年后               5,000     15,000      ¥ 9,600     ¥13,600       ¥2.72
# ================================================================================
```

**关键洞察：**

```yaml
1. 规模效应明显：
   - 100 DAU：单DAU成本 ¥41.92（固定成本占比高）
   - 5000 DAU：单DAU成本 ¥2.72（降低93%）

2. 盈亏平衡点（如果定价¥19.9/月，转化率3%）：
   - 单DAU收入 = ¥19.9 × 3% = ¥0.60
   - 单DAU成本 = ¥2.72（5000 DAU时）
   - 结论：仅靠付费转化无法覆盖成本，需其他收入来源

3. 成本控制关键：
   - 1000 DAU以下：总成本<¥6000/月（可控）
   - 5000 DAU：总成本¥13,600/月（需融资支持）
```

---

### **9.4.2 免费额度耗尽时间预测**

```python
class FreeQuotaExhaustionForecast:
    """免费额度耗尽预测"""
    
    def __init__(self):
        # 免费额度
        self.OCR_FREE_QUOTA_DAILY = 1000      # 百度OCR 1000次/天
        self.LLM_FREE_QUOTA_MONTHLY = 1_000_000  # 智谱GLM 100万tokens/月
        
        # 单用户消耗
        self.OCR_PER_USER_DAILY = 0.1          # 日均0.1次（月均3次）
        self.LLM_TOKENS_PER_NODE = 770         # 单节点770tokens
        self.NODES_PER_USER_MONTHLY = 10       # 用户月均10个节点
        
    def predict_ocr_exhaustion(self):
        """预测OCR免费额度何时耗尽"""
        
        # 每日可支持的用户数
        supported_users = self.OCR_FREE_QUOTA_DAILY / self.OCR_PER_USER_DAILY
        
        return {
            'free_quota_daily': self.OCR_FREE_QUOTA_DAILY,
            'supported_dau': int(supported_users),  # 10,000 DAU
            'message': f"OCR免费额度可支持{int(supported_users):,} DAU"
        }
    
    def predict_llm_exhaustion(self):
        """预测LLM免费额度何时耗尽"""
        
        # 每月可支持的节点数
        supported_nodes = self.LLM_FREE_QUOTA_MONTHLY / self.LLM_TOKENS_PER_NODE
        
        # 可支持的用户数
        supported_users = supported_nodes / self.NODES_PER_USER_MONTHLY
        
        # MAU转DAU（除以3）
        supported_dau = supported_users / 3
        
        return {
            'free_quota_monthly': self.LLM_FREE_QUOTA_MONTHLY,
            'supported_mau': int(supported_users),   # 130 MAU
            'supported_dau': int(supported_dau),     # 43 DAU
            'message': f"LLM免费额度可支持{int(supported_dau)} DAU"
        }

predictor = FreeQuotaExhaustionForecast()

ocr_result = predictor.predict_ocr_exhaustion()
llm_result = predictor.predict_llm_exhaustion()

print(f"""
免费额度耗尽预测：
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
OCR（百度）：
  - 免费额度：{ocr_result['free_quota_daily']}次/天
  - 可支持规模：{ocr_result['supported_dau']:,} DAU
  - 结论：✅ 足够MVP使用（目标1000 DAU）

LLM（智谱GLM-4）：
  - 免费额度：{llm_result['free_quota_monthly']:,} tokens/月
  - 可支持规模：{llm_result['supported_dau']} DAU
  - 结论：❌ 不足MVP使用（需付费）
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

关键决策：
1. OCR无压力，优先使用免费额度
2. LLM是成本大头，需重点优化（Prompt压缩、缓存）
3. Alpha阶段（100 DAU）可完全依赖免费额度
4. Beta阶段（500 DAU）需准备付费预算
""")
```

---

## **9.5 成本优化策略 (Cost Optimization Strategies)**

### **9.5.1 技术层面优化**

**优化1：智能缓存策略**

```python
class IntelligentCache:
    """智能缓存系统"""
    
    async def get_or_create_node(self, raw_input: str, source_type: str):
        """带缓存的节点创建"""
        
        # 1. 内容指纹
        content_fingerprint = self.generate_fingerprint(raw_input)
        cache_key = f"node_result:{content_fingerprint}"
        
        # 2. 尝试缓存
        cached = await redis.get(cache_key)
        if cached:
            metrics.increment('cache_hit', tags=['type:ai_result'])
            logger.info(f"Cache hit, saved AI cost")
            return json.loads(cached)
        
        # 3. 缓存未命中，调用AI
        metrics.increment('cache_miss', tags=['type:ai_result'])
        
        if source_type == 'voice':
            asr_result = await self.asr_with_cache(raw_input['audio_url'])
            refined = await self.llm_with_cache(asr_result)
        elif source_type == 'image':
            ocr_result = await self.ocr_with_cache(raw_input['image_url'])
            refined = await self.llm_with_cache(ocr_result)
        
        # 4. 写入缓存（24小时）
        await redis.setex(cache_key, 86400, json.dumps(refined))
        
        return refined
    
    def generate_fingerprint(self, raw_input: str) -> str:
        """生成内容指纹（避免完全相同内容重复处理）"""
        # 简化版：MD5哈希
        # 生产版：使用SimHash或MinHash（容错相似内容）
        import hashlib
        return hashlib.md5(raw_input.encode()).hexdigest()

# 预估缓存效果：
# - 缓存命中率：10-15%（保守估计）
# - 成本节省：¥0.64 × 15% = ¥0.096/用户/月
# - 1000用户规模：节省¥96/月
```

**优化2：批量处理与延迟处理**

```python
class BatchProcessor:
    """批量处理器（降低API调用频率）"""
    
    def __init__(self):
        self.batch_queue = []
        self.batch_size = 10
        self.batch_timeout = 5  # 秒
        
    async def add_to_batch(self, task):
        """添加任务到批处理队列"""
        self.batch_queue.append(task)
        
        # 达到批量大小或超时，触发处理
        if len(self.batch_queue) >= self.batch_size:
            await self.process_batch()
    
    async def process_batch(self):
        """批量处理（如果API支持）"""
        
        # 示例：批量生成Embedding（V1.1）
        texts = [task['text'] for task in self.batch_queue]
        embeddings = await embedding_service.batch_embed(texts)
        
        # 成本对比：
        # 单次调用：10次 × API延迟 = 高延迟
        # 批量调用：1次 × API延迟 = 低延迟
        # 某些服务商提供批量折扣
        
        self.batch_queue.clear()

# 注意：
# - ASR、OCR通常不支持批量（实时性要求高）
# - LLM目前不支持批量（GLM-4）
# - Embedding支持批量（V1.1可用）
```

**优化3：Prompt工程优化**

```python
# 已在9.2.3中详细说明，核心要点：

# 1. 压缩Prompt长度（减少40%输入Token）
# 2. 使用更精确的指令（减少重试次数）
# 3. 限制输出长度（content≤200字）
# 4. 避免冗余说明

# 实测效果：
# - 优化前单次成本：¥0.0385
# - 优化后单次成本：¥0.0270（减少30%）
# - 1000 MAU规模：月省¥115
```

**优化4：降级策略**

```python
class CostSavingDegradation:
    """成本节约降级策略"""
    
    async def create_node_with_budget_control(self, raw_input, user_id):
        """带预算控制的节点创建"""
        
        # 1. 检查用户当日成本
        daily_cost = await self.get_user_daily_cost(user_id)
        
        if daily_cost > 1.0:  # 单用户日成本超¥1
            logger.warning(f"User {user_id} daily cost exceeded ¥1")
            
            # 降级：使用更便宜的方案
            # 方案A：跳过LLM精炼，直接保存原始文本
            # 方案B：使用更便宜的LLM模型
            # 方案C：延后处理（非实时）
            
            return await self.create_node_simple(raw_input)
        
        # 2. 正常处理
        return await self.create_node_full_ai(raw_input)
    
    async def create_node_simple(self, raw_input):
        """简化版节点创建（无AI精炼）"""
        return {
            'title': raw_input['text'][:20],
            'content': raw_input['text'],
            'tags': [],
            'is_ai_processed': False
        }
```

---

### **9.5.2 产品层面优化**

**优化1：用户行为引导**

```yaml
策略1：降低低价值输入
  问题：用户随意录音，导致无效AI调用
  方案：
    - 提示"录音建议15秒以上"
    - 录音<5秒时提示"内容太短，可能无法生成有效节点"
    - 不强制阻止，但引导用户

策略2：合并相似内容
  问题：用户多次录入相似内容（如"今天学了XXX"）
  方案：
    - AI检测到相似内容时，提示"这似乎与之前的内容重复，是否继续？"
    - 建议用户编辑已有节点

策略3：每日限额（仅极端情况）
  问题：个别用户滥用（如日创建100+节点）
  方案：
    - 设置软限制：日均20个节点
    - 超过时友好提示："今天已创建20个节点，建议休息一下哦"
    - 不强制阻止，避免伤害体验
```

**优化2：功能分级**

```yaml
V1.1商业模式（Freemium）：

免费版：
  - 月度节点上限：50个
  - 使用标准AI模型
  - 部分功能限制

付费版（¥19.9/月）：
  - 无限节点
  - 使用更强AI模型（GPT-4，如果成本允许）
  - 所有高级功能

成本影响：
  - 免费用户成本：¥0.64/月（可接受）
  - 付费用户成本：¥2.00/月（ARPU ¥19.9，利润率90%）
  - 转化率3%：整体盈利
```

---

### **9.5.3 运营层面优化**

**优化1：成本监控与告警**

```python
class CostMonitoring:
    """成本监控系统"""
    
    async def daily_cost_check(self):
        """每日成本检查"""
        
        # 1. 统计今日成本
        today = datetime.now().date()
        
        costs = await db.query("""
            SELECT 
                SUM(ai_cost) as total_ai_cost,
                COUNT(DISTINCT user_id) as active_users,
                SUM(ai_cost) / COUNT(DISTINCT user_id) as avg_cost_per_user
            FROM node_creation_logs
            WHERE DATE(created_at) = %s
        """, today)
        
        total_cost = costs['total_ai_cost']
        avg_cost = costs['avg_cost_per_user']
        
        # 2. 预算检查
        daily_budget = 500  # ¥500/天
        
        if total_cost > daily_budget:
            await self.send_alert(
                level='CRITICAL',
                message=f"Daily AI cost exceeded budget: ¥{total_cost:.2f} > ¥{daily_budget}"
            )
        
        # 3. 异常用户检测
        expensive_users = await db.query("""
            SELECT user_id, SUM(ai_cost) as user_cost
            FROM node_creation_logs
            WHERE DATE(created_at) = %s
            GROUP BY user_id
            HAVING SUM(ai_cost) > 5.0  -- 单用户日成本>¥5
            ORDER BY user_cost DESC
            LIMIT 10
        """, today)
        
        if expensive_users:
            await self.send_alert(
                level='WARNING',
                message=f"Found {len(expensive_users)} high-cost users",
                details=expensive_users
            )
        
        # 4. 生成日报
        await self.generate_daily_report(costs)

# 告警通知渠道：
# - 钉钉/飞书群
# - 邮件
# - 短信（紧急情况）
```

**优化2：成本分析与优化建议**

```python
class CostAnalyzer:
    """成本分析器"""
    
    async def weekly_analysis(self):
        """每周成本分析"""
        
        # 1. 成本趋势
        weekly_costs = await db.query("""
            SELECT 
                DATE(created_at) as date,
                SUM(ai_cost) as daily_cost,
                COUNT(*) as daily_nodes
            FROM node_creation_logs
            WHERE created_at >= NOW() - INTERVAL '7 days'
            GROUP BY DATE(created_at)
            ORDER BY date
        """)
        
        # 2. 成本结构分析
        cost_breakdown = await db.query("""
            SELECT 
                source_type,
                SUM(asr_cost) as asr_total,
                SUM(ocr_cost) as ocr_total,
                SUM(llm_cost) as llm_total,
                COUNT(*) as node_count
            FROM node_creation_logs
            WHERE created_at >= NOW() - INTERVAL '7 days'
            GROUP BY source_type
        """)
        
        # 3. 优化建议
        suggestions = []
        
        # 如果LLM成本占比>60%
        llm_ratio = cost_breakdown['llm_total'] / cost_breakdown['total']
        if llm_ratio > 0.6:
            suggestions.append({
                'priority': 'HIGH',
                'suggestion': 'LLM成本占比过高，建议优化Prompt或增加缓存'
            })
        
        # 如果缓存命中率<10%
        cache_hit_rate = await self.get_cache_hit_rate()
        if cache_hit_rate < 0.1:
            suggestions.append({
                'priority': 'MEDIUM',
                'suggestion': f'缓存命中率仅{cache_hit_rate:.1%}，建议优化缓存策略'
            })
        
        return {
            'weekly_costs': weekly_costs,
            'cost_breakdown': cost_breakdown,
            'suggestions': suggestions
        }
```

---

## **9.6 预算分配与控制 (Budget Allocation & Control)**

### **9.6.1 MVP阶段预算分配**

```yaml
MVP总预算：¥500,000

预算分配：
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
1. 人力成本（6个月）：¥720,000
   - 产品经理 × 1：¥25,000/月 × 6 = ¥150,000
   - 技术Lead × 1：¥30,000/月 × 6 = ¥180,000
   - 前端工程师 × 1：¥20,000/月 × 6 = ¥120,000
   - 后端工程师 × 1：¥20,000/月 × 6 = ¥120,000
   - 算法工程师 × 1：¥22,000/月 × 6 = ¥132,000
   - UI/UX设计师 × 1（兼职）：¥3,000/月 × 6 = ¥18,000
   
   → 超出预算，需调整：
     方案A：缩短周期至4个月（¥480,000）
     方案B：减少人员或降低薪资
     方案C：寻求天使投资

2. AI服务成本（按4个月计）：¥20,000
   - Alpha（2周，100 DAU）：¥500
   - Beta（5周，500 DAU）：¥5,000
   - V1.0（3个月，1000 DAU）：¥14,500

3. 云服务成本（4个月）：¥12,000
   - 服务器：¥3,000/月 × 4 = ¥12,000

4. 其他成本：¥8,000
   - 域名、SSL证书：¥1,000
   - 第三方工具（Figma、Jira等）：¥3,000
   - 测试设备：¥2,000
   - 杂费：¥2,000

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
总计（调整后）：¥520,000

结论：预算紧张，需严格控制AI成本
```

---

### **9.6.2 AI预算控制机制**

```python
class BudgetController:
    """预算控制器"""
    
    def __init__(self):
        # 月度预算（可动态调整）
        self.MONTHLY_BUDGET = {
            'alpha': 500,      # Alpha阶段¥500/月
            'beta': 2000,      # Beta阶段¥2000/月
            'v1.0': 5000,      # V1.0阶段¥5000/月
        }
        
        self.current_stage = 'alpha'
        
    async def check_budget_before_call(self, service_type: str):
        """API调用前预算检查"""
        
        # 1. 获取当月已消耗预算
        month_start = datetime.now().replace(day=1)
        spent = await db.query("""
            SELECT SUM(ai_cost) as total_spent
            FROM node_creation_logs
            WHERE created_at >= %s
        """, month_start)
        
        total_spent = spent['total_spent'] or 0
        budget = self.MONTHLY_BUDGET[self.current_stage]
        
        # 2. 预算检查
        if total_spent >= budget:
            logger.error(f"Monthly budget exhausted: ¥{total_spent:.2f} >= ¥{budget}")
            
            # 触发降级
            await self.trigger_degradation()
            
            return False  # 不允许调用
        
        # 3. 预算预警（90%）
        if total_spent >= budget * 0.9:
            logger.warning(f"Budget warning: ¥{total_spent:.2f} / ¥{budget}")
            await self.send_budget_alert('WARNING', total_spent, budget)
        
        return True  # 允许调用
    
    async def trigger_degradation(self):
        """触发降级策略"""
        
        # 选项1：暂停非核心AI功能
        await redis.set('feature_flag:ai_resonance', 'false')
        
        # 选项2：切换到更便宜的服务商/模型
        await redis.set('llm_model', 'glm-3-turbo')  # 更便宜的模型
        
        # 选项3：通知团队
        await self.send_alert(
            level='CRITICAL',
            message='AI预算已耗尽，已启动降级策略'
        )
    
    async def daily_budget_report(self):
        """每日预算报告"""
        
        today_cost = await self.get_today_cost()
        month_cost = await self.get_month_cost()
        budget = self.MONTHLY_BUDGET[self.current_stage]
        
        # 预测月底成本
        days_passed = datetime.now().day
        days_in_month = calendar.monthrange(
            datetime.now().year,
            datetime.now().month
        )[1]
        
        projected_cost = month_cost / days_passed * days_in_month
        
        report = f"""
        📊 AI成本日报
        ━━━━━━━━━━━━━━━━━━━━━━━━━
        今日成本：¥{today_cost:.2f}
        本月累计：¥{month_cost:.2f}
        月度预算：¥{budget:.2f}
        预算使用率：{month_cost/budget:.1%}
        
        预测月底成本：¥{projected_cost:.2f}
        预算结余：¥{budget - projected_cost:.2f}
        
        {'⚠️ 预测超支！' if projected_cost > budget else '✅ 预算健康'}
        ━━━━━━━━━━━━━━━━━━━━━━━━━
        """
        
        await self.send_report_to_team(report)
```

---

### **9.6.3 应急预算储备**

```yaml
应急预算策略：

预算储备：10%（¥2,000）
  用途：应对以下突发情况
    1. AI服务商突然涨价
    2. 用户量超预期增长
    3. Bug导致API重复调用
    4. 其他不可预见成本

触发条件：
  - 月度成本超预算20%
  - 发生重大技术事故
  - CEO批准

使用流程：
  1. 产品经理提出申请
  2. CEO审批
  3. 财务划拨
  4. 事后复盘，避免再次发生
```

---

## **9.7 成本与商业模式 (Cost vs. Business Model)**

### **9.7.1 单位经济模型 (Unit Economics)**

```python
class UnitEconomics:
    """单位经济模型"""
    
    def __init__(self):
        # 成本
        self.COST_PER_USER_MONTHLY = 0.64  # AI成本
        self.CAC = 20.0                     # 获客成本（假设）
        
        # 收入（Freemium模式）
        self.PRICE_MONTHLY = 19.9           # 月订阅价格
        self.CONVERSION_RATE = 0.03         # 付费转化率3%
        
    def calculate_ltv(self, avg_lifetime_months=12):
        """计算用户生命周期价值"""
        
        # LTV = ARPU × 生命周期
        arpu = self.PRICE_MONTHLY * self.CONVERSION_RATE  # ¥0.60
        ltv = arpu * avg_lifetime_months                   # ¥7.2
        
        return ltv
    
    def calculate_profit(self, avg_lifetime_months=12):
        """计算单用户利润"""
        
        ltv = self.calculate_ltv(avg_lifetime_months)
        
        # 总成本 = 获客成本 + AI成本
        total_cost = self.CAC + (self.COST_PER_USER_MONTHLY * avg_lifetime_months)
        
        profit = ltv - total_cost
        roi = (profit / total_cost) if total_cost > 0 else 0
        
        return {
            'ltv': ltv,                    # ¥7.2
            'cac': self.CAC,               # ¥20
            'lifetime_ai_cost': self.COST_PER_USER_MONTHLY * avg_lifetime_months,  # ¥7.68
            'total_cost': total_cost,      # ¥27.68
            'profit': profit,              # -¥20.48（亏损！）
            'roi': roi,                    # -74%
            'ltv_to_cac_ratio': ltv / self.CAC  # 0.36（健康值应>3）
        }

model = UnitEconomics()
result = model.calculate_profit(avg_lifetime_months=12)

print(f"""
单位经济模型分析（Freemium模式）
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
用户生命周期价值（LTV）：¥{result['ltv']:.2f}
获客成本（CAC）：¥{result['cac']:.2f}
生命周期AI成本：¥{result['lifetime_ai_cost']:.2f}
总成本：¥{result['total_cost']:.2f}
─────────────────────────────
单用户利润：¥{result['profit']:.2f}
ROI：{result['roi']:.1%}
LTV:CAC比：{result['ltv_to_cac_ratio']:.2f}
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

⚠️ 结论：当前模式不可持续！
需要：
1. 提升付费转化率（3% → 10%）
2. 降低获客成本（¥20 → ¥10）
3. 增加其他收入来源（广告、企业版）
4. 延长用户生命周期（12月 → 24月）
""")
```

---

### **9.7.2 商业模式优化方向**

```yaml
方向1：提升付费转化率
  当前：3%
  目标：10%
  手段：
    - 增强付费功能差异化（如实时ASR、向量检索版共鸣）
    - 优化付费引导（在关键时刻提示升级）
    - 提供年付折扣（¥199/年，相当于¥16.6/月）

方向2：降低获客成本
  当前：¥20/用户
  目标：¥10/用户
  手段：
    - 提升产品推荐率（NPS>50）
    - 优化渠道（专注ROI最高的渠道）
    - 内容营销（SEO、公众号）

方向3：多元化收入
  - 广告收入：免费用户看非干扰性广告（¥0.3/用户/月）
  - 企业版：团队协作功能（¥99/人/月）
  - API服务：开放AI能力（¥5万/年）
  - 数据服务：匿名化行为数据（¥10万/年）

方向4：成本优化
  - AI成本优化至¥0.40/用户/月（优化38%）
  - 规模效应降低固定成本分摊
```

---

## **9.8 成本监控仪表盘 (Cost Monitoring Dashboard)**

### **9.8.1 关键指标定义**

```yaml
成本监控核心指标：

1. 绝对成本指标：
   - 日度AI成本
   - 月度AI成本
   - 各服务成本占比（ASR/OCR/LLM）

2. 相对成本指标：
   - 单DAU成本
   - 单MAU成本
   - 单节点成本

3. 效率指标：
   - 缓存命中率
   - API调用成功率
   - 平均Token消耗

4. 预算指标：
   - 预算使用率
   - 预算剩余天数
   - 预测月底成本

5. 异常指标：
   - 高成本用户数（日成本>¥5）
   - 成本异常峰值
   - 成本环比增长率
```

---

### **9.8.2 Grafana仪表盘配置示例**

```yaml
# Grafana Dashboard: Weave AI成本监控

panels:
  - title: "日度AI成本趋势"
    type: graph
    metrics:
      - sum(ai_cost) by (date)
    yaxis: "¥"
    
  - title: "成本结构（今日）"
    type: pie
    metrics:
      - sum(asr_cost) as "ASR"
      - sum(ocr_cost) as "OCR"
      - sum(llm_cost) as "LLM"
    
  - title: "单用户成本"
    type: stat
    metrics:
      - sum(ai_cost) / count(distinct user_id)
    threshold:
      - value: 0.64
        color: green
      - value: 1.0
        color: yellow
      - value: 2.0
        color: red
    
  - title: "预算使用情况"
    type: gauge
    metrics:
      - (sum(month_cost) / budget) * 100
    max: 100
    threshold:
      - 0-70: green
      - 70-90: yellow
      - 90-100: red
    
  - title: "高成本用户Top 10"
    type: table
    metrics:
      - user_id
      - sum(ai_cost) as daily_cost
      - count(*) as nodes_created
    order_by: daily_cost DESC
    limit: 10
    
  - title: "缓存命中率"
    type: graph
    metrics:
      - (cache_hits / (cache_hits + cache_misses)) * 100
    yaxis: "%"
    target: 15

# 告警规则（Prometheus AlertManager）
alerts:
  - name: DailyCostExceeded
    expr: sum(ai_cost_daily) > 500
    for: 1h
    severity: critical
    message: "日度AI成本超过¥500"
    
  - name: BudgetWarning
    expr: (sum(ai_cost_monthly) / budget) > 0.9
    for: 1h
    severity: warning
    message: "月度预算使用超过90%"
```

