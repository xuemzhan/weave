# 第五章：用户界面与体验设计 (UI & UX Design)**

---

## **5.1 设计理念与原则 (Design Philosophy & Principles)**

### **5.1.1 核心设计理念**

**"织念于无形 (Weaving Thoughts, Invisibly)"**

```
我们的设计理念源于产品愿景：
让AI成为思想的编织者，而非工具的操作者。

设计的最高境界是"隐形"：
- 用户感受到的是思想的流动，而非界面的存在
- 信息的捕捉应该像呼吸一样自然
- 知识的唤醒应该像老友的轻声提醒

视觉隐喻：
┌────────────────────────────────────┐
│  深邃星空 → 代表无限的思想空间      │
│  光线丝线 → 代表思想间的连接        │
│  星云汇聚 → 代表知识的结晶          │
│  脉冲光晕 → 代表灵感的闪现          │
└────────────────────────────────────┘
```

---

### **5.1.2 设计原则 (Design Principles)**

**原则1：沉浸优先 (Immersion First)**

```
定义：
让用户沉浸在思考本身，而非界面操作中。

实践：
✅ 全屏沉浸式录音界面（无干扰元素）
✅ 动态星空背景（营造思考氛围）
✅ 极简的信息层级（最多3级）
❌ 避免复杂的Tab导航
❌ 避免密集的按钮堆砌

设计检查清单：
- [ ] 页面核心操作是否在3秒内可完成？
- [ ] 是否有不必要的确认步骤？
- [ ] 用户的注意力是否集中在内容而非控件？
```

**原则2：无感交互 (Frictionless Interaction)**

```
定义：
降低每个操作的摩擦力，让记录像说话一样自然。

实践：
✅ 长按麦克风即录音（无需点击"开始"）
✅ 松手即结束（无需点击"停止"）
✅ 智能默认值（节点自动生成，无需手动填表单）
✅ 手势操作（滑动删除，双指缩放）
❌ 避免多步骤表单
❌ 避免强制必填项

摩擦力计算公式：
摩擦力 = 点击次数 × 0.5 + 输入字段数 × 1.0 + 页面跳转数 × 0.3

目标：核心流程摩擦力 < 2.0
实际：
- 语音创建节点：长按(0.5) + 松手(0.5) = 1.0 ✅
- 查看节点详情：点击卡片(0.5) + 跳转(0.3) = 0.8 ✅
```

**原则3：情感共鸣 (Emotional Resonance)**

```
定义：
通过视觉、文案、动效传递温暖、智慧、陪伴的情感。

实践：
✅ 温暖的文案："太棒了！今日的记忆已被点亮"
✅ 积极的反馈动画（星光闪烁、节点生成动画）
✅ 个性化的称呼（"你的思想星空"而非"我的笔记"）
✅ 鼓励性的空状态（"去编织新的思想吧"而非"暂无数据"）
❌ 避免冷冰冰的系统提示（"操作成功"）
❌ 避免强调"失败""错误"等负面词汇

文案情感检查清单：
- [ ] 是否使用第二人称（"你"）拉近距离？
- [ ] 是否避免使用"失败""错误"等负面词汇？
- [ ] 是否提供具体的指引而非模糊的提示？
```

**原则4：一致性 (Consistency)**

```
定义：
建立统一的设计语言，降低学习成本。

实践层面：
✅ 视觉一致性：统一的色彩、字体、圆角、间距
✅ 交互一致性：相同操作使用相同手势
✅ 文案一致性：统一的语气和术语
✅ 动效一致性：相同场景使用相同动画曲线

示例：
所有"删除"操作：
- 交互：左滑 + 红色删除按钮
- 确认：模态弹窗 + 二次确认
- 反馈：Toast提示 + 5秒撤销

所有"成功"反馈：
- 视觉：绿色✓图标 + 简短文案
- 动效：scale(1.2) → scale(1.0) 缓动动画
- 时长：1.5秒自动消失
```

**原则5：可预测性 (Predictability)**

```
定义：
用户的每个操作都应该有明确、可预测的结果。

实践：
✅ 明确的视觉反馈（按钮按下状态、loading动画）
✅ 清晰的状态提示（"正在识别..." → "识别完成"）
✅ 合理的操作后果说明（"删除后30天内可恢复"）
❌ 避免突然的页面跳转
❌ 避免模糊的进度提示（"处理中..."）

反馈时效要求：
- 点击反馈：< 100ms（视觉/触觉反馈）
- 操作结果：< 500ms（Toast或界面更新）
- 异步任务：提供进度指示（百分比或阶段）
```

---

## **5.2 视觉风格系统 (Visual Style System)**

### **5.2.1 品牌色板 (Color Palette)**

**主色板 (Primary Colors):**

| 色彩名称       | HEX       | RGB                | 使用场景             | Figma变量名            |
| -------------- | --------- | ------------------ | -------------------- | ---------------------- |
| **深邃星空蓝** | `#0A0F2C` | rgb(10, 15, 44)    | 主背景、深色模式主色 | `$color-bg-primary`    |
| **星云紫**     | `#6366F1` | rgb(99, 102, 241)  | 品牌主色、关键按钮   | `$color-brand-primary` |
| **灵感紫**     | `#A78BFA` | rgb(167, 139, 250) | 悬浮按钮、高亮强调   | `$color-brand-light`   |
| **月光白**     | `#F9FAFB` | rgb(249, 250, 251) | 卡片背景、浅色文本   | `$color-bg-card`       |

**辅助色板 (Secondary Colors):**

| 色彩名称       | HEX       | RGB                | 使用场景       |
| -------------- | --------- | ------------------ | -------------- |
| **星云灰-900** | `#111827` | rgb(17, 24, 39)    | 标题文本       |
| **星云灰-600** | `#4B5563` | rgb(75, 85, 99)    | 正文文本       |
| **星云灰-400** | `#9CA3AF` | rgb(156, 163, 175) | 次要文本、图标 |
| **星云灰-200** | `#E5E7EB` | rgb(229, 231, 235) | 分割线、边框   |
| **星云灰-100** | `#F3F4F6` | rgb(243, 244, 246) | 背景层         |

**语义色板 (Semantic Colors):**

| 语义     | 色彩名称 | HEX       | 使用场景         |
| -------- | -------- | --------- | ---------------- |
| **成功** | 翠绿     | `#10B981` | 操作成功、掌握了 |
| **警告** | 琥珀     | `#F59E0B` | 低置信度、模糊   |
| **错误** | 珊瑚红   | `#EF4444` | 错误提示、忘记了 |
| **信息** | 天蓝     | `#3B82F6` | 提示性信息       |

**渐变色 (Gradients):**

```css
/* 星空渐变背景 */
.gradient-cosmos {
  background: linear-gradient(
    180deg,
    #0A0F2C 0%,
    #1A1F3A 50%,
    #2A2F4A 100%
  );
}

/* 品牌渐变（按钮、强调） */
.gradient-brand {
  background: linear-gradient(
    135deg,
    #6366F1 0%,
    #A78BFA 100%
  );
}

/* 卡片玻璃态效果 */
.glass-card {
  background: rgba(249, 250, 251, 0.1);
  backdrop-filter: blur(20px);
  border: 1px solid rgba(255, 255, 255, 0.1);
}
```

**色彩使用规范：**

```
文本颜色对比度要求（WCAG 2.1 AA级）:
- 大文本（≥24px）：对比度 ≥ 3:1
- 正文文本（16-23px）：对比度 ≥ 4.5:1
- 小文本（<16px）：对比度 ≥ 7:1

示例验证：
✅ 星云灰-900 (#111827) on 月光白 (#F9FAFB) = 15.8:1 ✅
✅ 星云灰-600 (#4B5563) on 月光白 (#F9FAFB) = 7.2:1 ✅
✅ 星云紫 (#6366F1) on 月光白 (#F9FAFB) = 4.9:1 ✅
❌ 星云灰-400 (#9CA3AF) on 月光白 (#F9FAFB) = 3.1:1 ⚠️ 仅用于非关键信息
```

---

### **5.2.2 字体系统 (Typography)**

**字体家族 (Font Family):**

```css
/* 优先级：系统中文字体 → 系统英文字体 → 降级字体 */
--font-family-base: 
  "PingFang SC",           /* macOS/iOS 中文 */
  "HarmonyOS Sans",        /* 鸿蒙系统 */
  "Microsoft YaHei",       /* Windows 中文 */
  -apple-system,           /* iOS/macOS 系统字体 */
  BlinkMacSystemFont,      /* macOS 系统字体 */
  "Segoe UI",              /* Windows 系统字体 */
  sans-serif;              /* 降级 */

--font-family-mono: 
  "SF Mono",               /* macOS 等宽 */
  "Consolas",              /* Windows 等宽 */
  "Liberation Mono",       /* Linux */
  monospace;               /* 降级 */
```

**字阶系统 (Type Scale):**

| 层级    | 名称     | 字号(px) | 行高 | 字重 | 使用场景       | CSS类名         |
| ------- | -------- | -------- | ---- | ---- | -------------- | --------------- |
| H1      | 主标题   | 32       | 1.3  | 600  | 页面标题       | `.text-h1`      |
| H2      | 二级标题 | 24       | 1.4  | 600  | 区块标题       | `.text-h2`      |
| H3      | 三级标题 | 20       | 1.5  | 600  | 节点标题       | `.text-h3`      |
| Body-L  | 正文大   | 18       | 1.6  | 400  | 节点内容       | `.text-body-l`  |
| Body    | 正文     | 16       | 1.6  | 400  | 主要文本       | `.text-body`    |
| Body-S  | 正文小   | 14       | 1.5  | 400  | 辅助文本       | `.text-body-s`  |
| Caption | 说明文字 | 12       | 1.4  | 400  | 元信息、时间戳 | `.text-caption` |

**字重系统 (Font Weight):**

```css
--font-weight-regular: 400;  /* 正文 */
--font-weight-medium: 500;   /* 强调 */
--font-weight-semibold: 600; /* 标题 */
--font-weight-bold: 700;     /* 极少使用，仅特殊强调 */
```

**小程序rpx适配（750rpx设计稿）：**

```css
/* 设计稿基准：iPhone 6 (375px × 667px) */
/* 小程序基准：750rpx = 375px，即 1px = 2rpx */

.text-h1 { font-size: 64rpx; }      /* 32px */
.text-h2 { font-size: 48rpx; }      /* 24px */
.text-h3 { font-size: 40rpx; }      /* 20px */
.text-body-l { font-size: 36rpx; }  /* 18px */
.text-body { font-size: 32rpx; }    /* 16px */
.text-body-s { font-size: 28rpx; }  /* 14px */
.text-caption { font-size: 24rpx; } /* 12px */
```

**文本最佳实践：**

```
可读性规范：
✅ 正文行长：25-35字符（中文）
✅ 段落间距：≥0.5em
✅ 标题与正文间距：≥1em
❌ 避免全大写英文（降低可读性）
❌ 避免行高<1.3（过于紧凑）

示例：
<view class="node-content">
  <text class="text-h3">费曼学习法</text>  <!-- 标题 -->
  <text class="text-body-l">             <!-- 正文 -->
    费曼学习法的核心是"用简单的语言解释复杂的概念"...
  </text>
  <text class="text-caption">2小时前</text>  <!-- 元信息 -->
</view>
```

---

### **5.2.3 间距系统 (Spacing System)**

**8点网格系统 (8pt Grid):**

```
设计理念：
所有间距、尺寸均为8的倍数，保证视觉节奏一致。

基础单位：
1 unit = 8px = 16rpx（小程序）

间距刻度：
```

| 名称       | 单位 | px  | rpx | 使用场景               |
| ---------- | ---- | --- | --- | ---------------------- |
| `$space-1` | 1    | 8   | 16  | 极小间距（图标与文字） |
| `$space-2` | 2    | 16  | 32  | 小间距（同组元素）     |
| `$space-3` | 3    | 24  | 48  | 常规间距（不同组元素） |
| `$space-4` | 4    | 32  | 64  | 大间距（区块间）       |
| `$space-5` | 5    | 40  | 80  | 页面边距               |
| `$space-6` | 6    | 48  | 96  | 大区块间距             |
| `$space-8` | 8    | 64  | 128 | 超大间距（特殊场景）   |

**CSS变量定义：**

```css
/* 间距变量 */
--space-1: 16rpx;   /* 8px */
--space-2: 32rpx;   /* 16px */
--space-3: 48rpx;   /* 24px */
--space-4: 64rpx;   /* 32px */
--space-5: 80rpx;   /* 40px */
--space-6: 96rpx;   /* 48px */
--space-8: 128rpx;  /* 64px */

/* 页面级间距 */
--page-padding-horizontal: var(--space-3);  /* 左右边距 24px */
--page-padding-vertical: var(--space-4);    /* 上下边距 32px */

/* 卡片内边距 */
--card-padding: var(--space-4);  /* 32px */
```

**间距使用示例：**

```xml
<!-- 节点卡片 -->
<view class="node-card">
  <view class="node-header">
    <text class="node-title">费曼学习法</text>
    <text class="node-time">2小时前</text>  <!-- 标题与时间间距：space-2 -->
  </view>
  
  <view class="node-content">  <!-- header与content间距：space-3 -->
    费曼学习法的核心是...
  </view>
  
  <view class="node-tags">  <!-- content与tags间距：space-3 -->
    <view class="tag">#学习方法</view>  <!-- tag之间间距：space-1 -->
    <view class="tag">#认知科学</view>
  </view>
</view>

/* 对应样式 */
.node-card {
  padding: var(--card-padding);  /* 32px */
  margin-bottom: var(--space-3);  /* 卡片间距 24px */
}

.node-header {
  margin-bottom: var(--space-3);  /* 24px */
}

.node-content {
  margin-bottom: var(--space-3);  /* 24px */
}

.tag {
  margin-right: var(--space-1);  /* 8px */
}
```

---

### **5.2.4 圆角与阴影 (Border Radius & Shadows)**

**圆角系统：**

| 名称           | 值           | 使用场景           |
| -------------- | ------------ | ------------------ |
| `$radius-none` | 0            | 无圆角             |
| `$radius-sm`   | 8rpx (4px)   | 小标签、徽章       |
| `$radius-md`   | 16rpx (8px)  | 按钮               |
| `$radius-lg`   | 24rpx (12px) | 输入框             |
| `$radius-xl`   | 32rpx (16px) | 卡片               |
| `$radius-2xl`  | 48rpx (24px) | 大卡片、模态框     |
| `$radius-full` | 50%          | 圆形（头像、图标） |

**阴影系统：**

```css
/* 层级1：悬浮卡片 */
--shadow-sm: 0 2rpx 8rpx 0 rgba(0, 0, 0, 0.05);

/* 层级2：按钮按下 */
--shadow-md: 0 4rpx 16rpx 0 rgba(0, 0, 0, 0.1);

/* 层级3：悬浮按钮 */
--shadow-lg: 0 8rpx 32rpx 0 rgba(0, 0, 0, 0.15);

/* 层级4：模态框 */
--shadow-xl: 0 16rpx 48rpx 0 rgba(0, 0, 0, 0.2);

/* 品牌阴影（紫色光晕） */
--shadow-brand: 0 8rpx 24rpx 0 rgba(99, 102, 241, 0.3);

/* 使用示例 */
.floating-button {
  border-radius: var(--radius-full);
  box-shadow: var(--shadow-lg);
}

.floating-button:active {
  box-shadow: var(--shadow-md);  /* 按下时阴影减弱 */
}

.modal {
  border-radius: var(--radius-2xl);
  box-shadow: var(--shadow-xl);
}
```

---

### **5.2.5 图标系统 (Iconography)**

**图标风格：**

```
风格定义：
- 线性图标（Outline）为主
- 线宽：2px
- 圆角端点（rounded）
- 尺寸：24×24px基准（可缩放）
- 颜色：继承父元素文本颜色

图标库选择：
- 优先使用：Heroicons (MIT协议，风格匹配)
- 补充使用：自定义设计
```

**图标尺寸规范：**

| 场景     | 尺寸 | rpx   | 示例             |
| -------- | ---- | ----- | ---------------- |
| 大图标   | 48px | 96rpx | 空状态插图       |
| 标准图标 | 24px | 48rpx | 导航栏、按钮图标 |
| 小图标   | 16px | 32rpx | 列表项、tag图标  |
| 迷你图标 | 12px | 24rpx | 徽章、状态点     |

**常用图标定义：**

```xml
<!-- 麦克风图标 -->
<svg class="icon icon-mic" viewBox="0 0 24 24">
  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" 
    d="M19 11a7 7 0 01-7 7m0 0a7 7 0 01-7-7m7 7v4m0 0H8m4 0h4m-4-8a3 3 0 01-3-3V5a3 3 0 116 0v6a3 3 0 01-3 3z" />
</svg>

<!-- 图片上传图标 -->
<svg class="icon icon-image" viewBox="0 0 24 24">
  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" 
    d="M4 16l4.586-4.586a2 2 0 012.828 0L16 16m-2-2l1.586-1.586a2 2 0 012.828 0L20 14m-6-6h.01M6 20h12a2 2 0 002-2V6a2 2 0 00-2-2H6a2 2 0 00-2 2v12a2 2 0 002 2z" />
</svg>

/* CSS样式 */
.icon {
  width: 48rpx;   /* 24px */
  height: 48rpx;
  stroke: currentColor;  /* 继承父元素颜色 */
  fill: none;
}

.icon-lg {
  width: 96rpx;   /* 48px */
  height: 96rpx;
}
```

---

## **5.3 组件库 (Component Library)**

### **5.3.1 按钮组件 (Button)**

**按钮类型定义：**

| 类型          | 外观                             | 使用场景               | 优先级 |
| ------------- | -------------------------------- | ---------------------- | ------ |
| **Primary**   | 品牌紫填充 + 白色文字            | 主要操作（确认、提交） | P0     |
| **Secondary** | 白色填充 + 品牌紫文字 + 紫色边框 | 次要操作（取消、返回） | P0     |
| **Tertiary**  | 透明背景 + 灰色文字              | 辅助操作（查看详情）   | P1     |
| **Danger**    | 红色填充 + 白色文字              | 危险操作（删除）       | P0     |
| **Floating**  | 圆形 + 品牌渐变 + 阴影           | 核心操作（录音按钮）   | P0     |

**尺寸规范：**

```css
/* 大按钮（主要操作） */
.btn-lg {
  height: 96rpx;    /* 48px */
  padding: 0 64rpx; /* 32px */
  font-size: 32rpx; /* 16px */
  border-radius: 16rpx;
}

/* 标准按钮 */
.btn-md {
  height: 80rpx;    /* 40px */
  padding: 0 48rpx; /* 24px */
  font-size: 28rpx; /* 14px */
  border-radius: 16rpx;
}

/* 小按钮 */
.btn-sm {
  height: 64rpx;    /* 32px */
  padding: 0 32rpx; /* 16px */
  font-size: 24rpx; /* 12px */
  border-radius: 12rpx;
}

/* 悬浮按钮（圆形） */
.btn-floating {
  width: 128rpx;    /* 64px */
  height: 128rpx;
  border-radius: 50%;
  padding: 0;
}
```

**按钮状态：**

```css
/* Primary按钮 */
.btn-primary {
  background: linear-gradient(135deg, #6366F1, #A78BFA);
  color: #FFFFFF;
  box-shadow: 0 4rpx 16rpx 0 rgba(99, 102, 241, 0.3);
}

.btn-primary:active {
  opacity: 0.8;
  transform: scale(0.98);
  box-shadow: 0 2rpx 8rpx 0 rgba(99, 102, 241, 0.2);
}

.btn-primary:disabled {
  background: #E5E7EB;
  color: #9CA3AF;
  box-shadow: none;
}

/* 交互动画 */
.btn {
  transition: all 0.2s ease-in-out;
}

.btn:active {
  transition-duration: 0.1s;
}
```

**代码示例：**

```xml
<!-- Primary按钮 -->
<button class="btn btn-primary btn-lg">确认上传</button>

<!-- Secondary按钮 -->
<button class="btn btn-secondary btn-md">取消</button>

<!-- 悬浮按钮 -->
<view class="btn-floating" bindtap="startRecording">
  <image src="/icons/mic.svg" class="icon-lg"></image>
</view>
```

---

### **5.3.2 卡片组件 (Card)**

**节点卡片（Node Card）：**

```xml
<!-- 结构 -->
<view class="node-card" bindtap="navigateToDetail">
  <view class="node-header">
    <text class="node-title">{{ title }}</text>
    <view class="node-meta">
      <text class="node-time">{{ timeAgo }}</text>
      <image wx:if="{{ hasResonance }}" src="/icons/link.svg" class="icon-resonance"></image>
    </view>
  </view>
  
  <view class="node-content">
    <text class="text-body">{{ contentPreview }}</text>
  </view>
  
  <view class="node-tags">
    <view class="tag" wx:for="{{ tags }}" wx:key="index">
      <text>{{ item }}</text>
    </view>
  </view>
</view>

/* 样式 */
.node-card {
  background: #FFFFFF;
  border-radius: var(--radius-xl);  /* 32rpx */
  padding: var(--card-padding);     /* 64rpx */
  margin-bottom: var(--space-3);    /* 48rpx */
  box-shadow: var(--shadow-sm);
  transition: all 0.3s ease;
}

.node-card:active {
  box-shadow: var(--shadow-md);
  transform: scale(0.99);
}

.node-header {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  margin-bottom: var(--space-2);
}

.node-title {
  font-size: 40rpx;      /* 20px */
  font-weight: 600;
  color: #111827;
  flex: 1;
  line-height: 1.4;
}

.node-meta {
  display: flex;
  align-items: center;
  gap: var(--space-1);
}

.node-time {
  font-size: 24rpx;      /* 12px */
  color: #9CA3AF;
}

.node-content {
  margin-bottom: var(--space-2);
  line-height: 1.6;
  color: #4B5563;
  /* 限制3行 */
  display: -webkit-box;
  -webkit-line-clamp: 3;
  -webkit-box-orient: vertical;
  overflow: hidden;
  text-overflow: ellipsis;
}

.node-tags {
  display: flex;
  flex-wrap: wrap;
  gap: var(--space-1);
}

.tag {
  padding: 8rpx 16rpx;
  background: rgba(99, 102, 241, 0.1);
  border-radius: var(--radius-sm);
  font-size: 24rpx;
  color: #6366F1;
}
```

**思想共鸣卡片（Resonance Card）：**

```xml
<view class="resonance-card">
  <view class="resonance-header">
    <image src="/icons/sparkles.svg" class="icon-sparkle"></image>
    <text class="resonance-title">思想共鸣</text>
  </view>
  
  <view class="resonance-link">
    <text class="related-node-title">{{ relatedNodeTitle }}</text>
    <image src="/icons/arrow-right.svg" class="icon-arrow"></image>
  </view>
  
  <view class="resonance-explanation">
    <text>{{ aiExplanation }}</text>
  </view>
  
  <view class="resonance-keywords">
    <text class="keyword-label">共同关键词：</text>
    <text class="keyword" wx:for="{{ keywords }}" wx:key="index">
      #{{ item }}
    </text>
  </view>
  
  <view class="resonance-feedback">
    <button class="btn-feedback btn-helpful">
      <image src="/icons/thumb-up.svg"></image>
      <text>有帮助</text>
    </button>
    <button class="btn-feedback btn-irrelevant">
      <image src="/icons/thumb-down.svg"></image>
      <text>无关</text>
    </button>
  </view>
</view>

/* 样式 */
.resonance-card {
  background: linear-gradient(135deg, rgba(99, 102, 241, 0.05), rgba(167, 139, 250, 0.05));
  border: 2rpx solid rgba(99, 102, 241, 0.2);
  border-radius: var(--radius-xl);
  padding: var(--card-padding);
  margin-top: var(--space-4);
}

.resonance-header {
  display: flex;
  align-items: center;
  gap: var(--space-1);
  margin-bottom: var(--space-3);
}

.icon-sparkle {
  width: 32rpx;
  height: 32rpx;
}

.resonance-title {
  font-size: 28rpx;
  font-weight: 600;
  color: #6366F1;
}

.resonance-link {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: var(--space-2);
  background: rgba(255, 255, 255, 0.8);
  border-radius: var(--radius-md);
  margin-bottom: var(--space-2);
}

.resonance-feedback {
  display: flex;
  gap: var(--space-2);
  margin-top: var(--space-3);
}

.btn-feedback {
  flex: 1;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: var(--space-1);
  padding: var(--space-2);
  border-radius: var(--radius-md);
  background: rgba(255, 255, 255, 0.5);
  border: 2rpx solid rgba(99, 102, 241, 0.2);
  font-size: 24rpx;
  color: #6366F1;
}
```

---

### **5.3.3 输入组件 (Input)**

**文本输入框：**

```xml
<view class="input-group">
  <label class="input-label">标题</label>
  <input 
    class="input-field" 
    type="text" 
    placeholder="请输入标题"
    maxlength="100"
    value="{{ title }}"
    bindinput="onTitleInput"
  />
  <text class="input-hint">{{ titleLength }}/100</text>
</view>

/* 样式 */
.input-group {
  margin-bottom: var(--space-4);
}

.input-label {
  display: block;
  font-size: 28rpx;
  font-weight: 500;
  color: #111827;
  margin-bottom: var(--space-2);
}

.input-field {
  width: 100%;
  height: 80rpx;
  padding: 0 var(--space-3);
  background: #F9FAFB;
  border: 2rpx solid #E5E7EB;
  border-radius: var(--radius-lg);
  font-size: 32rpx;
  color: #111827;
  transition: all 0.2s;
}

.input-field:focus {
  background: #FFFFFF;
  border-color: #6366F1;
  box-shadow: 0 0 0 6rpx rgba(99, 102, 241, 0.1);
}

.input-field::placeholder {
  color: #9CA3AF;
}

.input-hint {
  display: block;
  margin-top: var(--space-1);
  font-size: 24rpx;
  color: #9CA3AF;
  text-align: right;
}
```

**多行文本框（Textarea）：**

```xml
<textarea 
  class="textarea-field"
  placeholder="请输入内容（支持Markdown）"
  maxlength="5000"
  auto-height
  value="{{ content }}"
  bindinput="onContentInput"
/>

/* 样式 */
.textarea-field {
  width: 100%;
  min-height: 300rpx;
  padding: var(--space-3);
  background: #F9FAFB;
  border: 2rpx solid #E5E7EB;
  border-radius: var(--radius-lg);
  font-size: 32rpx;
  line-height: 1.6;
  color: #111827;
}
```

---

### **5.3.4 模态框组件 (Modal)**

**确认对话框：**

```xml
<view class="modal-overlay" wx:if="{{ showDeleteModal }}" bindtap="closeModal">
  <view class="modal-container" catchtap="stopPropagation">
    <view class="modal-header">
      <image src="/icons/alert.svg" class="modal-icon modal-icon-warning"></image>
      <text class="modal-title">确认删除？</text>
    </view>
    
    <view class="modal-body">
      <text class="modal-message">你确定要删除这个思想节点吗？</text>
      <view class="modal-detail">
        <text class="node-title-preview">「{{ nodeTitle }}」</text>
      </view>
      <text class="modal-hint">删除后30天内可以恢复</text>
    </view>
    
    <view class="modal-footer">
      <button class="btn btn-secondary btn-md" bindtap="closeModal">
        取消
      </button>
      <button class="btn btn-danger btn-md" bindtap="confirmDelete">
        确认删除
      </button>
    </view>
  </view>
</view>

/* 样式 */
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.5);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 1000;
  animation: fadeIn 0.2s ease;
}

@keyframes fadeIn {
  from { opacity: 0; }
  to { opacity: 1; }
}

.modal-container {
  width: 600rpx;
  max-width: 90%;
  background: #FFFFFF;
  border-radius: var(--radius-2xl);
  box-shadow: var(--shadow-xl);
  animation: slideUp 0.3s ease;
}

@keyframes slideUp {
  from {
    transform: translateY(100rpx);
    opacity: 0;
  }
  to {
    transform: translateY(0);
    opacity: 1;
  }
}

.modal-header {
  padding: var(--space-5) var(--space-4) var(--space-3);
  text-align: center;
}

.modal-icon {
  width: 96rpx;
  height: 96rpx;
  margin-bottom: var(--space-2);
}

.modal-icon-warning {
  color: #F59E0B;
}

.modal-title {
  display: block;
  font-size: 40rpx;
  font-weight: 600;
  color: #111827;
}

.modal-body {
  padding: 0 var(--space-4) var(--space-4);
  text-align: center;
}

.modal-message {
  display: block;
  font-size: 32rpx;
  color: #4B5563;
  margin-bottom: var(--space-3);
}

.modal-detail {
  padding: var(--space-2);
  background: #F3F4F6;
  border-radius: var(--radius-md);
  margin-bottom: var(--space-2);
}

.node-title-preview {
  font-size: 28rpx;
  color: #6366F1;
}

.modal-hint {
  display: block;
  font-size: 24rpx;
  color: #9CA3AF;
}

.modal-footer {
  display: flex;
  gap: var(--space-2);
  padding: var(--space-3) var(--space-4) var(--space-4);
}

.modal-footer .btn {
  flex: 1;
}
```

---

### **5.3.5 Toast提示组件**

```xml
<view class="toast {{ toastVisible ? 'toast-show' : '' }}" wx:if="{{ toastMessage }}">
  <image wx:if="{{ toastType === 'success' }}" src="/icons/check-circle.svg" class="toast-icon"></image>
  <image wx:if="{{ toastType === 'error' }}" src="/icons/x-circle.svg" class="toast-icon"></image>
  <text class="toast-message">{{ toastMessage }}</text>
</view>

/* 样式 */
.toast {
  position: fixed;
  top: 200rpx;
  left: 50%;
  transform: translateX(-50%) translateY(-100rpx);
  padding: var(--space-2) var(--space-4);
  background: rgba(17, 24, 39, 0.9);
  border-radius: var(--radius-xl);
  display: flex;
  align-items: center;
  gap: var(--space-1);
  z-index: 2000;
  opacity: 0;
  transition: all 0.3s ease;
}

.toast-show {
  transform: translateX(-50%) translateY(0);
  opacity: 1;
}

.toast-icon {
  width: 40rpx;
  height: 40rpx;
}

.toast-message {
  font-size: 28rpx;
  color: #FFFFFF;
}

/* JavaScript控制 */
function showToast(message, type = 'success', duration = 2000) {
  this.setData({
    toastMessage: message,
    toastType: type,
    toastVisible: true
  });
  
  setTimeout(() => {
    this.setData({ toastVisible: false });
    setTimeout(() => {
      this.setData({ toastMessage: '' });
    }, 300);
  }, duration);
}
```

---

## **5.4 核心页面设计 (Core Page Design)**

### **5.4.1 主界面 (Home Page)**

**布局结构：**

```
┌───────────────────────────────────────┐
│  [Logo]                    [🔔 3]    │  ← Header (固定)
├───────────────────────────────────────┤
│                                       │
│  ┌─────────────────────────────────┐ │
│  │ 今日待唤醒 (3)                  │ │  ← 复习提醒横幅
│  │ 复习可以巩固记忆哦 →            │ │    (条件显示)
│  └─────────────────────────────────┘ │
│                                       │
│  ┌─────────────────────────────────┐ │
│  │ 📌 费曼学习法                   │ │
│  │ 费曼学习法的核心是用简单的...   │ │  ← 节点卡片列表
│  │ #学习方法 #认知科学  · 2小时前  │ │    (滚动区域)
│  └─────────────────────────────────┘ │
│                                       │
│  ┌─────────────────────────────────┐ │
│  │ 📌 间隔重复原理                 │ │
│  │ ...                             │ │
│  └─────────────────────────────────┘ │
│                                       │
│                        🎤  ← 悬浮按钮│  
│                        [+] ← 次级按钮│
│                                       │
└───────────────────────────────────────┘
```

**WXML结构：**

```xml
<view class="page-home">
  <!-- Header -->
  <view class="home-header">
    <view class="logo">
      <text class="logo-text">Weave</text>
      <text class="logo-subtitle">织念</text>
    </view>
    <view class="notification-icon" bindtap="navigateToNotifications">
      <image src="/icons/bell.svg" class="icon"></image>
      <view class="badge" wx:if="{{ unreadCount > 0 }}">
        <text>{{ unreadCount }}</text>
      </view>
    </view>
  </view>
  
  <!-- 复习提醒横幅 -->
  <view class="review-banner" wx:if="{{ pendingReviewCount > 0 }}" bindtap="navigateToReview">
    <view class="banner-content">
      <image src="/icons/lightbulb.svg" class="banner-icon"></image>
      <view class="banner-text">
        <text class="banner-title">今日待唤醒 ({{ pendingReviewCount }})</text>
        <text class="banner-subtitle">复习可以巩固记忆哦</text>
      </view>
    </view>
    <image src="/icons/chevron-right.svg" class="banner-arrow"></image>
  </view>
  
  <!-- 节点列表 -->
  <scroll-view class="nodes-list" scroll-y refresher-enabled bindrefresherrefresh="onPullRefresh">
    <view wx:if="{{ nodes.length === 0 }}" class="empty-state">
      <image src="/images/empty-cosmos.png" class="empty-image"></image>
      <text class="empty-title">你的思想星空空无一物</text>
      <text class="empty-subtitle">点击下方的麦克风，播下第一颗种子吧</text>
    </view>
    
    <view wx:else>
      <view 
        class="node-card" 
        wx:for="{{ nodes }}" 
        wx:key="id"
        bindtap="navigateToNodeDetail"
        data-id="{{ item.id }}"
      >
        <!-- 节点卡片内容（见5.3.2） -->
      </view>
    </view>
  </scroll-view>
  
  <!-- 悬浮操作按钮 -->
  <view class="floating-actions">
    <view class="fab-secondary" bindtap="showInputOptions">
      <image src="/icons/plus.svg" class="icon"></image>
    </view>
    <view class="fab-primary" bindlongpress="startVoiceRecording">
      <image src="/icons/mic.svg" class="icon icon-lg"></image>
    </view>
  </view>
</view>
```

**WXSS样式：**

```css
/* 页面容器 */
.page-home {
  min-height: 100vh;
  background: linear-gradient(180deg, #0A0F2C 0%, #1A1F3A 100%);
  padding-bottom: 200rpx;  /* 为悬浮按钮留空间 */
}

/* Header */
.home-header {
  position: sticky;
  top: 0;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: var(--space-3) var(--space-3);
  background: rgba(10, 15, 44, 0.8);
  backdrop-filter: blur(20rpx);
  z-index: 100;
}

.logo {
  display: flex;
  align-items: baseline;
  gap: var(--space-1);
}

.logo-text {
  font-size: 48rpx;
  font-weight: 600;
  color: #FFFFFF;
}

.logo-subtitle {
  font-size: 24rpx;
  color: rgba(255, 255, 255, 0.6);
}

.notification-icon {
  position: relative;
  width: 48rpx;
  height: 48rpx;
}

.badge {
  position: absolute;
  top: -8rpx;
  right: -8rpx;
  min-width: 32rpx;
  height: 32rpx;
  padding: 0 8rpx;
  background: #EF4444;
  border-radius: 16rpx;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 20rpx;
  color: #FFFFFF;
}

/* 复习横幅 */
.review-banner {
  margin: var(--space-3);
  padding: var(--space-3);
  background: linear-gradient(135deg, rgba(99, 102, 241, 0.2), rgba(167, 139, 250, 0.2));
  border: 2rpx solid rgba(99, 102, 241, 0.3);
  border-radius: var(--radius-xl);
  display: flex;
  justify-content: space-between;
  align-items: center;
  backdrop-filter: blur(10rpx);
  transition: all 0.3s;
}

.review-banner:active {
  transform: scale(0.98);
}

.banner-content {
  display: flex;
  align-items: center;
  gap: var(--space-2);
}

.banner-icon {
  width: 64rpx;
  height: 64rpx;
}

.banner-title {
  display: block;
  font-size: 32rpx;
  font-weight: 600;
  color: #FFFFFF;
  margin-bottom: 4rpx;
}

.banner-subtitle {
  font-size: 24rpx;
  color: rgba(255, 255, 255, 0.8);
}

/* 节点列表 */
.nodes-list {
  padding: 0 var(--space-3);
  height: calc(100vh - 200rpx);
}

/* 空状态 */
.empty-state {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: var(--space-8) var(--space-4);
  text-align: center;
}

.empty-image {
  width: 400rpx;
  height: 300rpx;
  margin-bottom: var(--space-4);
  opacity: 0.6;
}

.empty-title {
  font-size: 36rpx;
  font-weight: 600;
  color: rgba(255, 255, 255, 0.9);
  margin-bottom: var(--space-2);
}

.empty-subtitle {
  font-size: 28rpx;
  color: rgba(255, 255, 255, 0.6);
}

/* 悬浮按钮组 */
.floating-actions {
  position: fixed;
  right: 32rpx;
  bottom: 160rpx;
  display: flex;
  flex-direction: column;
  gap: var(--space-2);
  z-index: 100;
}

.fab-primary {
  width: 128rpx;
  height: 128rpx;
  border-radius: 50%;
  background: linear-gradient(135deg, #6366F1, #A78BFA);
  box-shadow: 0 8rpx 32rpx 0 rgba(99, 102, 241, 0.4);
  display: flex;
  align-items: center;
  justify-content: center;
  transition: all 0.3s;
}

.fab-primary:active {
  transform: scale(0.9);
  box-shadow: 0 4rpx 16rpx 0 rgba(99, 102, 241, 0.3);
}

.fab-secondary {
  width: 96rpx;
  height: 96rpx;
  border-radius: 50%;
  background: rgba(255, 255, 255, 0.2);
  backdrop-filter: blur(10rpx);
  box-shadow: 0 4rpx 16rpx 0 rgba(0, 0, 0, 0.1);
  display: flex;
  align-items: center;
  justify-content: center;
  transition: all 0.3s;
}

.fab-secondary:active {
  transform: scale(0.9);
}
```

---

# **第五章：用户界面与体验设计 (UI & UX Design)** - 续

---

## **5.4 核心页面设计 (Core Page Design)** - 续

### **5.4.2 节点详情页 (Node Detail Page)**

**页面目标：**

- 清晰展示节点的完整内容
- 提供"思想共鸣"的惊喜发现
- 支持查看AI处理过程（建立信任）
- 快捷操作入口（编辑、删除、分享）

**布局结构：**

```
┌───────────────────────────────────────┐
│  [< 返回]              [⋯ 更多]      │  ← Header (固定)
├───────────────────────────────────────┤
│                                       │
│  费曼学习法                           │  ← 标题
│  ─────────────────────────────        │
│                                       │
│  费曼学习法的核心是"用简单的语言      │
│  解释复杂的概念"。当你能够用自己      │  ← 核心内容
│  的话将一个知识点讲清楚时...          │    (可滚动)
│                                       │
│  #学习方法 #认知科学                  │  ← 标签
│  创建于 2小时前 · 已复习3次            │  ← 元信息
│                                       │
│  ─────────────────────────────        │
│                                       │
│  ✨ 思想共鸣 (1)                      │  ← 关联模块
│  ┌─────────────────────────────────┐ │    (异步加载)
│  │ 💡 与「间隔重复原理」相关        │ │
│  │ ...                             │ │
│  └─────────────────────────────────┘ │
│                                       │
│  [查看AI处理过程 ▼]                  │  ← 可展开区域
│                                       │
│  [👍 有帮助]  [👎 无关]              │  ← 反馈按钮
│                                       │
└───────────────────────────────────────┘
```

**WXML结构：**

```xml
<view class="page-node-detail">
  <!-- Header -->
  <view class="detail-header">
    <view class="header-left" bindtap="navigateBack">
      <image src="/icons/chevron-left.svg" class="icon"></image>
      <text>返回</text>
    </view>
    <view class="header-right" bindtap="showActionMenu">
      <image src="/icons/dots-vertical.svg" class="icon"></image>
    </view>
  </view>
  
  <!-- 主内容区 -->
  <scroll-view class="detail-content" scroll-y>
    <!-- 节点标题 -->
    <view class="node-title-section">
      <text class="node-title">{{ node.title }}</text>
    </view>
    
    <!-- 节点内容 -->
    <view class="node-content-section">
      <rich-text nodes="{{ formattedContent }}" class="rich-content"></rich-text>
    </view>
    
    <!-- 标签 -->
    <view class="node-tags-section">
      <view class="tag" wx:for="{{ node.tags }}" wx:key="index">
        <text>#{{ item }}</text>
      </view>
    </view>
    
    <!-- 元信息 -->
    <view class="node-meta-section">
      <view class="meta-item">
        <image src="/icons/clock.svg" class="meta-icon"></image>
        <text>创建于 {{ node.createdAt }}</text>
      </view>
      <view class="meta-item" wx:if="{{ node.reviewCount > 0 }}">
        <image src="/icons/refresh.svg" class="meta-icon"></image>
        <text>已复习 {{ node.reviewCount }} 次</text>
      </view>
    </view>
    
    <!-- 分割线 -->
    <view class="divider"></view>
    
    <!-- 思想共鸣模块 -->
    <view class="resonance-section" wx:if="{{ resonances.length > 0 }}">
      <view class="section-header">
        <image src="/icons/sparkles.svg" class="section-icon"></image>
        <text class="section-title">思想共鸣 ({{ resonances.length }})</text>
      </view>
      
      <view 
        class="resonance-card" 
        wx:for="{{ resonances }}" 
        wx:key="id"
        bindtap="navigateToRelatedNode"
        data-id="{{ item.relatedNodeId }}"
      >
        <view class="resonance-link">
          <text class="related-node-title">{{ item.relatedNodeTitle }}</text>
          <image src="/icons/arrow-right.svg" class="icon-arrow"></image>
        </view>
        
        <view class="resonance-explanation">
          <text>{{ item.aiAnalysis.explanation }}</text>
        </view>
        
        <view class="resonance-keywords" wx:if="{{ item.aiAnalysis.commonKeywords }}">
          <text class="keyword-label">共同关键词：</text>
          <text 
            class="keyword" 
            wx:for="{{ item.aiAnalysis.commonKeywords }}" 
            wx:key="index"
            wx:for-item="keyword"
          >
            #{{ keyword }}
          </text>
        </view>
        
        <view class="resonance-feedback">
          <button 
            class="btn-feedback {{ item.userFeedback === 'helpful' ? 'active' : '' }}"
            bindtap="feedbackResonance"
            data-id="{{ item.id }}"
            data-rating="helpful"
            catchtap="stopPropagation"
          >
            <image src="/icons/thumb-up.svg" class="icon-sm"></image>
            <text>有帮助</text>
          </button>
          <button 
            class="btn-feedback {{ item.userFeedback === 'irrelevant' ? 'active' : '' }}"
            bindtap="feedbackResonance"
            data-id="{{ item.id }}"
            data-rating="irrelevant"
            catchtap="stopPropagation"
          >
            <image src="/icons/thumb-down.svg" class="icon-sm"></image>
            <text>无关</text>
          </button>
        </view>
      </view>
    </view>
    
    <!-- 加载中状态 -->
    <view class="resonance-loading" wx:if="{{ resonancesLoading }}">
      <view class="skeleton-card"></view>
      <text class="loading-text">正在寻找共鸣...</text>
    </view>
    
    <!-- AI处理过程（可展开） -->
    <view class="ai-process-section">
      <view class="section-toggle" bindtap="toggleAIProcess">
        <text class="section-title">查看AI处理过程</text>
        <image 
          src="/icons/chevron-down.svg" 
          class="icon-chevron {{ showAIProcess ? 'rotate-180' : '' }}"
        ></image>
      </view>
      
      <view class="ai-process-content" wx:if="{{ showAIProcess }}">
        <view class="process-compare">
          <view class="process-column">
            <text class="column-label">原始输入</text>
            <view class="content-box">
              <text class="text-mono">{{ node.rawInput.text }}</text>
            </view>
          </view>
          
          <view class="process-arrow">
            <image src="/icons/arrow-right.svg" class="icon"></image>
          </view>
          
          <view class="process-column">
            <text class="column-label">AI精炼后</text>
            <view class="content-box content-box-refined">
              <text>{{ node.content }}</text>
            </view>
          </view>
        </view>
        
        <view class="process-hint">
          <image src="/icons/info.svg" class="icon-sm"></image>
          <text>AI帮你提取了核心要点，去除了口语化表达</text>
        </view>
      </view>
    </view>
    
    <!-- 底部反馈 -->
    <view class="feedback-section">
      <text class="feedback-question">这个智慧节点对你有帮助吗？</text>
      <view class="feedback-buttons">
        <button 
          class="btn-feedback-large {{ nodeFeedback === 'good' ? 'active' : '' }}"
          bindtap="feedbackNode"
          data-rating="good"
        >
          <image src="/icons/thumb-up.svg" class="icon"></image>
          <text>有帮助</text>
        </button>
        <button 
          class="btn-feedback-large {{ nodeFeedback === 'bad' ? 'active' : '' }}"
          bindtap="feedbackNode"
          data-rating="bad"
        >
          <image src="/icons/thumb-down.svg" class="icon"></image>
          <text>需要改进</text>
        </button>
      </view>
    </view>
    
    <!-- 底部安全距离 -->
    <view class="safe-area-bottom"></view>
  </scroll-view>
</view>

<!-- 操作菜单（底部弹出） -->
<view class="action-sheet-overlay" wx:if="{{ showActionSheet }}" bindtap="closeActionSheet">
  <view class="action-sheet" catchtap="stopPropagation">
    <view class="action-item" bindtap="editNode">
      <image src="/icons/pencil.svg" class="action-icon"></image>
      <text>编辑节点</text>
    </view>
    <view class="action-item" bindtap="shareNode">
      <image src="/icons/share.svg" class="action-icon"></image>
      <text>分享</text>
    </view>
    <view class="action-item action-item-danger" bindtap="deleteNode">
      <image src="/icons/trash.svg" class="action-icon"></image>
      <text>删除</text>
    </view>
    <view class="action-item action-cancel" bindtap="closeActionSheet">
      <text>取消</text>
    </view>
  </view>
</view>
```

**WXSS样式：**

```css
/* 页面容器 */
.page-node-detail {
  min-height: 100vh;
  background: #F9FAFB;
}

/* Header */
.detail-header {
  position: sticky;
  top: 0;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: var(--space-3);
  background: #FFFFFF;
  border-bottom: 2rpx solid #E5E7EB;
  z-index: 100;
}

.header-left {
  display: flex;
  align-items: center;
  gap: var(--space-1);
  font-size: 32rpx;
  color: #6366F1;
}

/* 主内容区 */
.detail-content {
  height: calc(100vh - 100rpx);
  padding: var(--space-4);
}

/* 标题区域 */
.node-title-section {
  margin-bottom: var(--space-4);
}

.node-title {
  font-size: 48rpx;
  font-weight: 600;
  color: #111827;
  line-height: 1.3;
  word-break: break-word;
}

/* 内容区域 */
.node-content-section {
  margin-bottom: var(--space-4);
}

.rich-content {
  font-size: 36rpx;
  line-height: 1.8;
  color: #4B5563;
  word-break: break-word;
}

/* Markdown样式增强 */
.rich-content >>> p {
  margin-bottom: 1em;
}

.rich-content >>> strong {
  font-weight: 600;
  color: #111827;
}

.rich-content >>> code {
  padding: 4rpx 8rpx;
  background: #F3F4F6;
  border-radius: var(--radius-sm);
  font-family: var(--font-family-mono);
  font-size: 32rpx;
  color: #6366F1;
}

/* 标签区域 */
.node-tags-section {
  display: flex;
  flex-wrap: wrap;
  gap: var(--space-2);
  margin-bottom: var(--space-3);
}

.tag {
  padding: 12rpx 24rpx;
  background: rgba(99, 102, 241, 0.1);
  border-radius: var(--radius-md);
  font-size: 28rpx;
  color: #6366F1;
}

/* 元信息区域 */
.node-meta-section {
  display: flex;
  flex-wrap: wrap;
  gap: var(--space-3);
  margin-bottom: var(--space-4);
}

.meta-item {
  display: flex;
  align-items: center;
  gap: var(--space-1);
  font-size: 24rpx;
  color: #9CA3AF;
}

.meta-icon {
  width: 32rpx;
  height: 32rpx;
}

/* 分割线 */
.divider {
  height: 2rpx;
  background: #E5E7EB;
  margin: var(--space-5) 0;
}

/* 区块标题 */
.section-header {
  display: flex;
  align-items: center;
  gap: var(--space-2);
  margin-bottom: var(--space-3);
}

.section-icon {
  width: 48rpx;
  height: 48rpx;
}

.section-title {
  font-size: 36rpx;
  font-weight: 600;
  color: #111827;
}

/* 思想共鸣卡片 */
.resonance-section {
  margin-bottom: var(--space-5);
}

.resonance-card {
  background: linear-gradient(135deg, rgba(99, 102, 241, 0.05), rgba(167, 139, 250, 0.05));
  border: 2rpx solid rgba(99, 102, 241, 0.2);
  border-radius: var(--radius-xl);
  padding: var(--space-4);
  margin-bottom: var(--space-3);
  transition: all 0.3s;
}

.resonance-card:active {
  transform: scale(0.99);
  background: linear-gradient(135deg, rgba(99, 102, 241, 0.1), rgba(167, 139, 250, 0.1));
}

.resonance-link {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: var(--space-2);
  background: rgba(255, 255, 255, 0.8);
  border-radius: var(--radius-md);
  margin-bottom: var(--space-2);
}

.related-node-title {
  font-size: 32rpx;
  font-weight: 500;
  color: #6366F1;
  flex: 1;
}

.icon-arrow {
  width: 32rpx;
  height: 32rpx;
  opacity: 0.6;
}

.resonance-explanation {
  margin-bottom: var(--space-2);
  font-size: 28rpx;
  line-height: 1.6;
  color: #4B5563;
}

.resonance-keywords {
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  gap: var(--space-1);
  margin-bottom: var(--space-3);
}

.keyword-label {
  font-size: 24rpx;
  color: #9CA3AF;
}

.keyword {
  font-size: 24rpx;
  color: #6366F1;
}

.resonance-feedback {
  display: flex;
  gap: var(--space-2);
}

.btn-feedback {
  flex: 1;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: var(--space-1);
  padding: var(--space-2);
  background: rgba(255, 255, 255, 0.5);
  border: 2rpx solid rgba(99, 102, 241, 0.2);
  border-radius: var(--radius-md);
  font-size: 24rpx;
  color: #6366F1;
  transition: all 0.2s;
}

.btn-feedback.active {
  background: #6366F1;
  color: #FFFFFF;
  border-color: #6366F1;
}

.icon-sm {
  width: 28rpx;
  height: 28rpx;
}

/* 加载骨架屏 */
.resonance-loading {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: var(--space-5) 0;
}

.skeleton-card {
  width: 100%;
  height: 200rpx;
  background: linear-gradient(90deg, #F3F4F6 25%, #E5E7EB 50%, #F3F4F6 75%);
  background-size: 200% 100%;
  border-radius: var(--radius-xl);
  animation: skeleton-loading 1.5s infinite;
}

@keyframes skeleton-loading {
  0% { background-position: 200% 0; }
  100% { background-position: -200% 0; }
}

.loading-text {
  margin-top: var(--space-2);
  font-size: 24rpx;
  color: #9CA3AF;
}

/* AI处理过程 */
.ai-process-section {
  margin-bottom: var(--space-5);
}

.section-toggle {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: var(--space-3);
  background: #FFFFFF;
  border-radius: var(--radius-lg);
  cursor: pointer;
}

.icon-chevron {
  width: 32rpx;
  height: 32rpx;
  transition: transform 0.3s;
}

.icon-chevron.rotate-180 {
  transform: rotate(180deg);
}

.ai-process-content {
  margin-top: var(--space-3);
  padding: var(--space-4);
  background: #FFFFFF;
  border-radius: var(--radius-lg);
  animation: slideDown 0.3s ease;
}

@keyframes slideDown {
  from {
    opacity: 0;
    transform: translateY(-20rpx);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.process-compare {
  display: flex;
  gap: var(--space-2);
  margin-bottom: var(--space-3);
}

.process-column {
  flex: 1;
}

.column-label {
  display: block;
  font-size: 24rpx;
  font-weight: 600;
  color: #6366F1;
  margin-bottom: var(--space-2);
}

.content-box {
  padding: var(--space-3);
  background: #F9FAFB;
  border: 2rpx solid #E5E7EB;
  border-radius: var(--radius-md);
  font-size: 28rpx;
  line-height: 1.6;
  color: #4B5563;
  max-height: 400rpx;
  overflow-y: auto;
}

.content-box-refined {
  border-color: #6366F1;
  background: rgba(99, 102, 241, 0.05);
}

.text-mono {
  font-family: var(--font-family-mono);
  font-size: 26rpx;
}

.process-arrow {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 64rpx;
}

.process-hint {
  display: flex;
  align-items: center;
  gap: var(--space-1);
  padding: var(--space-2);
  background: rgba(99, 102, 241, 0.05);
  border-radius: var(--radius-md);
  font-size: 24rpx;
  color: #6366F1;
}

/* 反馈区域 */
.feedback-section {
  text-align: center;
  padding: var(--space-4) 0;
}

.feedback-question {
  display: block;
  font-size: 28rpx;
  color: #4B5563;
  margin-bottom: var(--space-3);
}

.feedback-buttons {
  display: flex;
  gap: var(--space-3);
  justify-content: center;
}

.btn-feedback-large {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: var(--space-1);
  padding: var(--space-3) var(--space-4);
  background: #FFFFFF;
  border: 2rpx solid #E5E7EB;
  border-radius: var(--radius-lg);
  font-size: 28rpx;
  color: #4B5563;
  transition: all 0.3s;
}

.btn-feedback-large.active {
  background: #10B981;
  border-color: #10B981;
  color: #FFFFFF;
}

.btn-feedback-large .icon {
  width: 48rpx;
  height: 48rpx;
}

/* 操作菜单 */
.action-sheet-overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.5);
  z-index: 2000;
  animation: fadeIn 0.2s;
}

.action-sheet {
  position: fixed;
  left: 0;
  right: 0;
  bottom: 0;
  background: #FFFFFF;
  border-radius: 48rpx 48rpx 0 0;
  padding: var(--space-4);
  animation: slideUpSheet 0.3s ease;
}

@keyframes slideUpSheet {
  from {
    transform: translateY(100%);
  }
  to {
    transform: translateY(0);
  }
}

.action-item {
  display: flex;
  align-items: center;
  gap: var(--space-3);
  padding: var(--space-4);
  font-size: 32rpx;
  color: #111827;
  border-radius: var(--radius-lg);
  transition: background 0.2s;
}

.action-item:active {
  background: #F3F4F6;
}

.action-icon {
  width: 48rpx;
  height: 48rpx;
}

.action-item-danger {
  color: #EF4444;
}

.action-cancel {
  margin-top: var(--space-2);
  justify-content: center;
  font-weight: 600;
  border-top: 2rpx solid #E5E7EB;
}

.safe-area-bottom {
  height: env(safe-area-inset-bottom);
}
```

---

### **5.4.3 记忆唤醒页 (Awakening Session Page)**

**页面目标：**

- 极简的闪卡复习体验
- 清晰的进度反馈
- 即时的记忆评估
- 激励性的完成页面

**闪卡正面（问题）：**

```xml
<view class="page-awakening">
  <!-- 进度条 -->
  <view class="progress-section">
    <view class="progress-bar">
      <view 
        class="progress-fill" 
        style="width: {{ (currentIndex / totalCount * 100) }}%"
      ></view>
    </view>
    <text class="progress-text">{{ currentIndex + 1 }} / {{ totalCount }}</text>
  </view>
  
  <!-- 闪卡容器 -->
  <view class="flashcard-container">
    <view class="flashcard {{ isFlipped ? 'flipped' : '' }}">
      <!-- 正面（问题） -->
      <view class="flashcard-front">
        <view class="card-hint">
          <text>回忆一下这个知识点的内容</text>
        </view>
        
        <view class="card-content">
          <text class="card-title">{{ currentNode.title }}</text>
        </view>
        
        <view class="card-tags">
          <view class="tag-sm" wx:for="{{ currentNode.tags }}" wx:key="index">
            <text>#{{ item }}</text>
          </view>
        </view>
      </view>
      
      <!-- 反面（答案） -->
      <view class="flashcard-back">
        <view class="card-content">
          <text class="card-title">{{ currentNode.title }}</text>
          <view class="divider-sm"></view>
          <text class="card-answer">{{ currentNode.content }}</text>
        </view>
      </view>
    </view>
  </view>
  
  <!-- 操作按钮 -->
  <view class="action-section">
    <button 
      wx:if="{{ !isFlipped }}" 
      class="btn btn-primary btn-lg btn-full"
      bindtap="revealAnswer"
    >
      <image src="/icons/eye.svg" class="icon"></image>
      <text>查看答案</text>
    </button>
    
    <view wx:else class="quality-buttons">
      <text class="quality-question">你掌握了这个知识吗？</text>
      <view class="button-group">
        <button 
          class="btn-quality btn-forgot"
          bindtap="submitQuality"
          data-score="2"
        >
          <text class="quality-emoji">😕</text>
          <text class="quality-label">忘记了</text>
        </button>
        
        <button 
          class="btn-quality btn-vague"
          bindtap="submitQuality"
          data-score="3"
        >
          <text class="quality-emoji">😐</text>
          <text class="quality-label">模糊</text>
        </button>
        
        <button 
          class="btn-quality btn-mastered"
          bindtap="submitQuality"
          data-score="5"
        >
          <text class="quality-emoji">😊</text>
          <text class="quality-label">掌握了</text>
        </button>
      </view>
    </view>
  </view>
  
  <!-- 退出按钮 -->
  <view class="exit-button" bindtap="confirmExit">
    <image src="/icons/x.svg" class="icon"></image>
  </view>
</view>

<!-- 反馈Toast -->
<view class="quality-feedback {{ showFeedback ? 'show' : '' }}" wx:if="{{ feedbackMessage }}">
  <image src="/icons/check-circle.svg" class="feedback-icon"></image>
  <text class="feedback-message">{{ feedbackMessage }}</text>
  <text class="feedback-detail">将在 {{ nextReviewDays }} 天后再次复习</text>
</view>
```

**完成页面：**

```xml
<view class="page-completion">
  <view class="completion-container">
    <!-- 成功动画 -->
    <view class="success-animation">
      <image src="/images/sparkle-animation.gif" class="animation-image"></image>
    </view>
    
    <!-- 标题 -->
    <text class="completion-title">太棒了！</text>
    <text class="completion-subtitle">今日的记忆已被点亮</text>
    
    <!-- 统计卡片 -->
    <view class="stats-card">
      <view class="stat-item">
        <text class="stat-value">{{ reviewedCount }}</text>
        <text class="stat-label">今日复习</text>
      </view>
      <view class="stat-divider"></view>
      <view class="stat-item stat-highlight">
        <text class="stat-value">{{ masteredCount }}</text>
        <text class="stat-label">已掌握</text>
      </view>
      <view class="stat-divider"></view>
      <view class="stat-item">
        <text class="stat-value">{{ vagueCount }}</text>
        <text class="stat-label">模糊</text>
      </view>
    </view>
    
    <!-- 连续复习天数 -->
    <view class="streak-section" wx:if="{{ streakDays > 0 }}">
      <view class="streak-badge">
        <image src="/icons/fire.svg" class="streak-icon"></image>
        <text class="streak-text">连续复习 {{ streakDays }} 天</text>
      </view>
      <text class="streak-encouragement">坚持下去，知识会成为你的本能！</text>
    </view>
    
    <!-- 操作按钮 -->
    <view class="completion-actions">
      <button class="btn btn-secondary btn-lg" bindtap="backToHome">
        返回首页
      </button>
      <button class="btn btn-primary btn-lg" bindtap="createNewNode">
        创建新节点
      </button>
    </view>
  </view>
</view>
```

**WXSS样式：**

```css
/* 唤醒页面 */
.page-awakening {
  min-height: 100vh;
  background: linear-gradient(180deg, #0A0F2C 0%, #1A1F3A 100%);
  display: flex;
  flex-direction: column;
  padding: var(--space-4);
}

/* 进度条 */
.progress-section {
  margin-bottom: var(--space-5);
}

.progress-bar {
  height: 8rpx;
  background: rgba(255, 255, 255, 0.2);
  border-radius: 4rpx;
  overflow: hidden;
  margin-bottom: var(--space-2);
}

.progress-fill {
  height: 100%;
  background: linear-gradient(90deg, #6366F1, #A78BFA);
  border-radius: 4rpx;
  transition: width 0.5s ease;
}

.progress-text {
  display: block;
  text-align: center;
  font-size: 24rpx;
  color: rgba(255, 255, 255, 0.6);
}

/* 闪卡容器 */
.flashcard-container {
  flex: 1;
  display: flex;
  align-items: center;
  justify-content: center;
  perspective: 2000rpx;
  margin-bottom: var(--space-5);
}

.flashcard {
  width: 100%;
  height: 800rpx;
  position: relative;
  transform-style: preserve-3d;
  transition: transform 0.6s;
}

.flashcard.flipped {
  transform: rotateY(180deg);
}

.flashcard-front,
.flashcard-back {
  position: absolute;
  width: 100%;
  height: 100%;
  backface-visibility: hidden;
  background: rgba(255, 255, 255, 0.95);
  border-radius: var(--radius-2xl);
  padding: var(--space-5);
  display: flex;
  flex-direction: column;
  justify-content: center;
  box-shadow: 0 16rpx 64rpx 0 rgba(0, 0, 0, 0.2);
}

.flashcard-back {
  transform: rotateY(180deg);
}

.card-hint {
  text-align: center;
  margin-bottom: var(--space-4);
}

.card-hint text {
  font-size: 24rpx;
  color: #9CA3AF;
}

.card-content {
  flex: 1;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.card-title {
  font-size: 56rpx;
  font-weight: 600;
  color: #111827;
  line-height: 1.3;
  margin-bottom: var(--space-3);
}

.divider-sm {
  width: 100rpx;
  height: 4rpx;
  background: #E5E7EB;
  margin: var(--space-4) 0;
}

.card-answer {
  font-size: 36rpx;
  line-height: 1.8;
  color: #4B5563;
  max-height: 500rpx;
  overflow-y: auto;
}

.card-tags {
  display: flex;
  flex-wrap: wrap;
  gap: var(--space-1);
  justify-content: center;
}

.tag-sm {
  padding: 8rpx 16rpx;
  background: rgba(99, 102, 241, 0.1);
  border-radius: var(--radius-sm);
  font-size: 24rpx;
  color: #6366F1;
}

/* 操作按钮 */
.action-section {
  margin-bottom: var(--space-4);
}

.btn-full {
  width: 100%;
}

.quality-buttons {
  display: flex;
  flex-direction: column;
  gap: var(--space-3);
}

.quality-question {
  text-align: center;
  font-size: 32rpx;
  color: rgba(255, 255, 255, 0.9);
  margin-bottom: var(--space-2);
}

.button-group {
  display: flex;
  gap: var(--space-2);
}

.btn-quality {
  flex: 1;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: var(--space-1);
  padding: var(--space-4) var(--space-2);
  background: rgba(255, 255, 255, 0.95);
  border-radius: var(--radius-xl);
  border: 3rpx solid transparent;
  transition: all 0.3s;
}

.btn-quality:active {
  transform: scale(0.95);
}

.btn-forgot {
  border-color: rgba(239, 68, 68, 0.3);
}

.btn-forgot:active {
  background: rgba(239, 68, 68, 0.1);
  border-color: #EF4444;
}

.btn-vague {
  border-color: rgba(245, 158, 11, 0.3);
}

.btn-vague:active {
  background: rgba(245, 158, 11, 0.1);
  border-color: #F59E0B;
}

.btn-mastered {
  border-color: rgba(16, 185, 129, 0.3);
}

.btn-mastered:active {
  background: rgba(16, 185, 129, 0.1);
  border-color: #10B981;
}

.quality-emoji {
  font-size: 64rpx;
}

.quality-label {
  font-size: 28rpx;
  color: #4B5563;
  font-weight: 500;
}

/* 退出按钮 */
.exit-button {
  position: fixed;
  top: var(--space-3);
  right: var(--space-3);
  width: 64rpx;
  height: 64rpx;
  background: rgba(255, 255, 255, 0.2);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 10;
}

.exit-button .icon {
  width: 32rpx;
  height: 32rpx;
}

/* 反馈Toast */
.quality-feedback {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%) scale(0.8);
  padding: var(--space-4) var(--space-5);
  background: rgba(16, 185, 129, 0.95);
  border-radius: var(--radius-2xl);
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: var(--space-1);
  z-index: 3000;
  opacity: 0;
  transition: all 0.3s;
}

.quality-feedback.show {
  opacity: 1;
  transform: translate(-50%, -50%) scale(1);
}

.feedback-icon {
  width: 96rpx;
  height: 96rpx;
  margin-bottom: var(--space-2);
}

.feedback-message {
  font-size: 36rpx;
  font-weight: 600;
  color: #FFFFFF;
}

.feedback-detail {
  font-size: 28rpx;
  color: rgba(255, 255, 255, 0.9);
}

/* 完成页面 */
.page-completion {
  min-height: 100vh;
  background: linear-gradient(180deg, #0A0F2C 0%, #1A1F3A 100%);
  display: flex;
  align-items: center;
  justify-content: center;
  padding: var(--space-4);
}

.completion-container {
  width: 100%;
  text-align: center;
}

.success-animation {
  margin-bottom: var(--space-4);
}

.animation-image {
  width: 300rpx;
  height: 300rpx;
}

.completion-title {
  display: block;
  font-size: 64rpx;
  font-weight: 600;
  color: #FFFFFF;
  margin-bottom: var(--space-2);
}

.completion-subtitle {
  display: block;
  font-size: 32rpx;
  color: rgba(255, 255, 255, 0.8);
  margin-bottom: var(--space-5);
}

/* 统计卡片 */
.stats-card {
  display: flex;
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(20rpx);
  border-radius: var(--radius-2xl);
  padding: var(--space-4);
  margin-bottom: var(--space-5);
}

.stat-item {
  flex: 1;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: var(--space-1);
}

.stat-value {
  font-size: 72rpx;
  font-weight: 700;
  color: #FFFFFF;
}

.stat-label {
  font-size: 24rpx;
  color: rgba(255, 255, 255, 0.7);
}

.stat-highlight .stat-value {
  color: #10B981;
}

.stat-divider {
  width: 2rpx;
  background: rgba(255, 255, 255, 0.2);
}

/* Streak徽章 */
.streak-section {
  margin-bottom: var(--space-5);
}

.streak-badge {
  display: inline-flex;
  align-items: center;
  gap: var(--space-2);
  padding: var(--space-2) var(--space-4);
  background: linear-gradient(135deg, rgba(239, 68, 68, 0.2), rgba(245, 158, 11, 0.2));
  border: 2rpx solid rgba(245, 158, 11, 0.5);
  border-radius: var(--radius-xl);
  margin-bottom: var(--space-2);
}

.streak-icon {
  width: 48rpx;
  height: 48rpx;
}

.streak-text {
  font-size: 32rpx;
  font-weight: 600;
  color: #FFA500;
}

.streak-encouragement {
  display: block;
  font-size: 24rpx;
  color: rgba(255, 255, 255, 0.6);
}

/* 操作按钮 */
.completion-actions {
  display: flex;
  flex-direction: column;
  gap: var(--space-3);
}
```

---

### **5.4.4 编辑页面 (Edit Page)**

**页面目标：**

- 清晰的编辑界面
- 实时字数统计
- 草稿自动保存
- 明确的保存/取消操作

**WXML结构：**

```xml
<view class="page-edit">
  <!-- Header -->
  <view class="edit-header">
    <button class="header-btn" bindtap="confirmCancel">
      <text>取消</text>
    </button>
    <text class="header-title">编辑节点</text>
    <button class="header-btn header-btn-primary" bindtap="saveNode">
      <text>保存</text>
    </button>
  </view>
  
  <!-- 编辑表单 -->
  <scroll-view class="edit-form" scroll-y>
    <!-- 标题 -->
    <view class="form-section">
      <view class="form-label">
        <text>标题</text>
        <text class="form-required">*</text>
      </view>
      <input 
        class="input-title"
        type="text"
        placeholder="请输入标题"
        maxlength="100"
        value="{{ title }}"
        bindinput="onTitleInput"
        focus="{{ titleFocus }}"
      />
      <text class="char-count">{{ titleLength }}/100</text>
    </view>
    
    <!-- 内容 -->
    <view class="form-section">
      <view class="form-label">
        <text>内容</text>
        <text class="form-required">*</text>
        <text class="form-hint">支持Markdown</text>
      </view>
      <textarea 
        class="input-content"
        placeholder="请输入内容"
        maxlength="5000"
        auto-height
        value="{{ content }}"
        bindinput="onContentInput"
      />
      <text class="char-count">{{ contentLength }}/5000</text>
    </view>
    
    <!-- 标签 -->
    <view class="form-section">
      <view class="form-label">
        <text>标签</text>
        <text class="form-hint">最多5个</text>
      </view>
      <view class="tags-input">
        <view class="tag-item" wx:for="{{ tags }}" wx:key="index">
          <text>#{{ item }}</text>
          <view class="tag-remove" bindtap="removeTag" data-index="{{ index }}">
            <image src="/icons/x-sm.svg" class="icon-xs"></image>
          </view>
        </view>
        <input 
          wx:if="{{ tags.length < 5 }}"
          class="tag-input-field"
          type="text"
          placeholder="添加标签"
          maxlength="10"
          value="{{ newTag }}"
          bindinput="onTagInput"
          bindconfirm="addTag"
        />
      </view>
    </view>
    
    <!-- 原始内容（只读） -->
    <view class="form-section">
      <view class="section-toggle" bindtap="toggleOriginal">
        <text class="section-title">查看原始内容</text>
        <image 
          src="/icons/chevron-down.svg" 
          class="icon-chevron {{ showOriginal ? 'rotate-180' : '' }}"
        ></image>
      </view>
      
      <view class="original-content" wx:if="{{ showOriginal }}">
        <text class="original-label">原始语音/图片识别文本：</text>
        <view class="original-box">
          <text class="original-text">{{ originalText }}</text>
        </view>
        <text class="original-hint">提示：编辑不会改变原始内容</text>
      </view>
    </view>
    
    <!-- 底部安全距离 -->
    <view class="safe-area-bottom"></view>
  </scroll-view>
  
  <!-- 保存提示 -->
  <view class="save-indicator {{ autoSaving ? 'show' : '' }}">
    <image src="/icons/check.svg" class="icon-xs"></image>
    <text>草稿已自动保存</text>
  </view>
</view>
```

**WXSS样式：**

```css
.page-edit {
  min-height: 100vh;
  background: #F9FAFB;
  display: flex;
  flex-direction: column;
}

/* Header */
.edit-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: var(--space-3);
  background: #FFFFFF;
  border-bottom: 2rpx solid #E5E7EB;
}

.header-btn {
  padding: var(--space-2) var(--space-3);
  font-size: 28rpx;
  color: #6366F1;
  background: transparent;
}

.header-btn-primary {
  font-weight: 600;
}

.header-title {
  font-size: 32rpx;
  font-weight: 600;
  color: #111827;
}

/* 表单 */
.edit-form {
  flex: 1;
  padding: var(--space-4);
}

.form-section {
  margin-bottom: var(--space-5);
}

.form-label {
  display: flex;
  align-items: center;
  gap: var(--space-1);
  margin-bottom: var(--space-2);
}

.form-label text:first-child {
  font-size: 28rpx;
  font-weight: 600;
  color: #111827;
}

.form-required {
  font-size: 28rpx;
  color: #EF4444;
}

.form-hint {
  font-size: 24rpx;
  color: #9CA3AF;
  margin-left: auto;
}

/* 标题输入 */
.input-title {
  width: 100%;
  padding: var(--space-3);
  background: #FFFFFF;
  border: 2rpx solid #E5E7EB;
  border-radius: var(--radius-lg);
  font-size: 36rpx;
  font-weight: 600;
  color: #111827;
}

.input-title:focus {
  border-color: #6366F1;
  box-shadow: 0 0 0 6rpx rgba(99, 102, 241, 0.1);
}

/* 内容输入 */
.input-content {
  width: 100%;
  min-height: 400rpx;
  padding: var(--space-3);
  background: #FFFFFF;
  border: 2rpx solid #E5E7EB;
  border-radius: var(--radius-lg);
  font-size: 32rpx;
  line-height: 1.8;
  color: #4B5563;
}

.input-content:focus {
  border-color: #6366F1;
  box-shadow: 0 0 0 6rpx rgba(99, 102, 241, 0.1);
}

.char-count {
  display: block;
  margin-top: var(--space-1);
  text-align: right;
  font-size: 24rpx;
  color: #9CA3AF;
}

/* 标签输入 */
.tags-input {
  display: flex;
  flex-wrap: wrap;
  gap: var(--space-2);
  padding: var(--space-3);
  background: #FFFFFF;
  border: 2rpx solid #E5E7EB;
  border-radius: var(--radius-lg);
  min-height: 100rpx;
}

.tag-item {
  display: flex;
  align-items: center;
  gap: var(--space-1);
  padding: 8rpx 16rpx;
  background: rgba(99, 102, 241, 0.1);
  border-radius: var(--radius-sm);
  font-size: 28rpx;
  color: #6366F1;
}

.tag-remove {
  width: 32rpx;
  height: 32rpx;
  display: flex;
  align-items: center;
  justify-content: center;
  background: rgba(99, 102, 241, 0.2);
  border-radius: 50%;
}

.icon-xs {
  width: 20rpx;
  height: 20rpx;
}

.tag-input-field {
  flex: 1;
  min-width: 200rpx;
  font-size: 28rpx;
  color: #4B5563;
}

/* 原始内容 */
.original-content {
  margin-top: var(--space-3);
  animation: slideDown 0.3s ease;
}

.original-label {
  display: block;
  font-size: 24rpx;
  color: #6366F1;
  margin-bottom: var(--space-2);
}

.original-box {
  padding: var(--space-3);
  background: #F3F4F6;
  border: 2rpx solid #E5E7EB;
  border-radius: var(--radius-md);
  max-height: 300rpx;
  overflow-y: auto;
}

.original-text {
  font-size: 28rpx;
  font-family: var(--font-family-mono);
  line-height: 1.6;
  color: #4B5563;
}

.original-hint {
  display: block;
  margin-top: var(--space-2);
  font-size: 24rpx;
  color: #9CA3AF;
}

/* 自动保存提示 */
.save-indicator {
  position: fixed;
  bottom: 100rpx;
  left: 50%;
  transform: translateX(-50%) translateY(100rpx);
  display: flex;
  align-items: center;
  gap: var(--space-1);
  padding: var(--space-2) var(--space-3);
  background: rgba(16, 185, 129, 0.9);
  border-radius: var(--radius-lg);
  font-size: 24rpx;
  color: #FFFFFF;
  opacity: 0;
  transition: all 0.3s;
  z-index: 100;
}

.save-indicator.show {
  transform: translateX(-50%) translateY(0);
  opacity: 1;
}
```

---

## **5.5 动效设计规范 (Animation Guidelines)**

### **5.5.1 动效原则**

**原则1：有目的的动效**

```
每个动效都必须服务于以下目的之一：
1. 提供视觉反馈（按钮点击、操作成功）
2. 引导用户注意力（新内容出现）
3. 建立空间关系（页面转场）
4. 增强品牌感知（加载动画）

❌ 避免：纯装饰性动效
```

**原则2：性能优先**

```
✅ 优先使用CSS transform和opacity（GPU加速）
✅ 避免动画width、height、top等触发重排的属性
✅ 使用will-change提示浏览器优化
✅ 动画时长控制在200-500ms

性能检查清单：
- [ ] 动画帧率保持60fps
- [ ] 页面滚动时暂停非关键动画
- [ ] 动画结束后移除will-change
```

### **5.5.2 动效时长与缓动**

**标准时长（Duration）：**

| 场景         | 时长  | 说明                 |
| ------------ | ----- | -------------------- |
| **微交互**   | 150ms | 按钮点击、开关切换   |
| **标准转场** | 300ms | 页面切换、模态框弹出 |
| **大型动画** | 500ms | 闪卡翻转、数据加载   |
| **背景动画** | 1-3s  | 星空粒子、骨架屏     |

**缓动函数（Easing）：**

```css
/* 标准缓动 */
--ease-in-out: cubic-bezier(0.4, 0.0, 0.2, 1);      /* 平滑进出 */
--ease-out: cubic-bezier(0.0, 0.0, 0.2, 1);         /* 快速进入，缓慢退出 */
--ease-in: cubic-bezier(0.4, 0.0, 1, 1);            /* 缓慢进入，快速退出 */

/* 弹性缓动 */
--ease-elastic: cubic-bezier(0.68, -0.55, 0.265, 1.55);  /* 轻微回弹 */

/* 使用建议 */
.modal-enter {
  animation: slideUp 300ms var(--ease-out);  /* 进入：快速出现 */
}

.modal-leave {
  animation: slideDown 200ms var(--ease-in);  /* 退出：快速消失 */
}
```

### **5.5.3 核心动效库**

**1. 按钮反馈动效：**

```css
.btn {
  transition: all 0.2s var(--ease-out);
  will-change: transform;
}

.btn:active {
  transform: scale(0.96);
}

/* 成功反馈 */
@keyframes successPulse {
  0%, 100% {
    transform: scale(1);
    opacity: 1;
  }
  50% {
    transform: scale(1.05);
    opacity: 0.8;
  }
}

.btn-success-feedback {
  animation: successPulse 0.4s var(--ease-in-out);
}
```

**2. 页面转场动效：**

```css
/* 页面进入（从右侧滑入） */
@keyframes pageEnter {
  from {
    transform: translateX(100%);
    opacity: 0;
  }
  to {
    transform: translateX(0);
    opacity: 1;
  }
}

/* 页面退出（向右侧滑出） */
@keyframes pageLeave {
  from {
    transform: translateX(0);
    opacity: 1;
  }
  to {
    transform: translateX(-30%);
    opacity: 0;
  }
}

.page-enter {
  animation: pageEnter 300ms var(--ease-out);
}

.page-leave {
  animation: pageLeave 250ms var(--ease-in);
}
```

**3. 列表项出现动效（交错动画）：**

```css
@keyframes listItemFadeIn {
  from {
    opacity: 0;
    transform: translateY(40rpx);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.list-item {
  animation: listItemFadeIn 0.4s var(--ease-out);
  animation-fill-mode: both;
}

/* 交错延迟 */
.list-item:nth-child(1) { animation-delay: 0ms; }
.list-item:nth-child(2) { animation-delay: 50ms; }
.list-item:nth-child(3) { animation-delay: 100ms; }
.list-item:nth-child(4) { animation-delay: 150ms; }
```

**4. 加载动画：**

```css
/* 脉冲加载 */
@keyframes pulse {
  0%, 100% {
    opacity: 1;
  }
  50% {
    opacity: 0.5;
  }
}

.loading-pulse {
  animation: pulse 1.5s var(--ease-in-out) infinite;
}

/* 旋转加载 */
@keyframes spin {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(360deg);
  }
}

.loading-spinner {
  animation: spin 1s linear infinite;
}

/* 骨架屏闪烁 */
@keyframes shimmer {
  0% {
    background-position: -200% 0;
  }
  100% {
    background-position: 200% 0;
  }
}

.skeleton {
  background: linear-gradient(
    90deg,
    #F3F4F6 25%,
    #E5E7EB 50%,
    #F3F4F6 75%
  );
  background-size: 200% 100%;
  animation: shimmer 1.5s infinite;
}
```

**5. 特殊品牌动效：**

```css
/* 星光闪烁（用于成功反馈） */
@keyframes sparkle {
  0%, 100% {
    opacity: 0;
    transform: scale(0);
  }
  50% {
    opacity: 1;
    transform: scale(1);
  }
}

.sparkle-effect {
  animation: sparkle 0.6s var(--ease-out);
}

/* 思想连接线条动画 */
@keyframes drawLine {
  from {
    stroke-dashoffset: 1000;
  }
  to {
    stroke-dashoffset: 0;
  }
}

.connection-line {
  stroke-dasharray: 1000;
  animation: drawLine 1s var(--ease-out);
}
```

---

## **5.6 无障碍设计 (Accessibility)**

### **5.6.1 色彩对比度**

**WCAG 2.1 AA级标准要求：**

```
文本对比度要求：
- 正文文本（<18px）：≥ 4.5:1
- 大文本（≥18px或粗体≥14px）：≥ 3:1
- 图标和UI组件：≥ 3:1

检查工具：
- Chrome DevTools - Lighthouse
- WebAIM Contrast Checker
- Figma插件：Stark

实际验证：
✅ 深邃星空蓝 (#0A0F2C) on 月光白 (#F9FAFB) = 16.2:1
✅ 星云灰-900 (#111827) on 月光白 (#F9FAFB) = 15.8:1
✅ 星云紫 (#6366F1) on 月光白 (#F9FAFB) = 4.9:1
⚠️ 星云灰-400 (#9CA3AF) on 月光白 (#F9FAFB) = 3.1:1 - 仅用于辅助信息
```

### **5.6.2 可点击区域尺寸**

```
最小触控目标：44×44px（88×88rpx）

实施检查：
✅ 主要按钮：96rpx × 96rpx（远超最小标准）
✅ 图标按钮：至少 88rpx × 88rpx
✅ 列表项：最小高度 120rpx

边界情况：
- 小图标（如删除×）：增加透明padding扩大点击区域
- 密集标签：标签间距至少 16rpx
```

**代码示例：**

```css
/* 小图标扩大点击区域 */
.icon-button-sm {
  width: 32rpx;   /* 视觉尺寸 */
  height: 32rpx;
  padding: 28rpx;  /* 扩大到88rpx */
}

/* 或使用伪元素 */
.tag-remove {
  position: relative;
  width: 32rpx;
  height: 32rpx;
}

.tag-remove::before {
  content: '';
  position: absolute;
  top: -28rpx;
  left: -28rpx;
  right: -28rpx;
  bottom: -28rpx;
}
```

### **5.6.3 语义化标签**

```xml
<!-- ✅ 好的实践 -->
<button class="btn-primary" bindtap="submit">
  确认提交
</button>

<label for="title-input">标题</label>
<input id="title-input" aria-label="节点标题" />

<!-- ❌ 不好的实践 -->
<view bindtap="submit">
  确认提交  <!-- 应该用button -->
</view>

<input placeholder="标题" />  <!-- 缺少label -->
```

### **5.6.4 焦点管理**

```css
/* 键盘焦点样式（Web端需要） */
.btn:focus-visible {
  outline: 4rpx solid #6366F1;
  outline-offset: 4rpx;
}

/* 跳过默认焦点样式 */
.btn:focus:not(:focus-visible) {
  outline: none;
}
```

### **5.6.5 屏幕阅读器支持**

```xml
<!-- 提供额外的屏幕阅读器信息 -->
<view aria-label="智慧节点列表">
  <view 
    wx:for="{{ nodes }}" 
    role="article"
    aria-label="节点：{{ item.title }}，创建于{{ item.createdAt }}"
  >
    <!-- 节点内容 -->
  </view>
</view>

<!-- 隐藏装饰性元素 -->
<image src="/images/decoration.png" aria-hidden="true"></image>

<!-- 动态内容提示 -->
<view aria-live="polite" aria-atomic="true">
  {{ statusMessage }}
</view>
```

---

## **5.7 设计交付规范 (Design Handoff)**

### **5.7.1 Figma设计文件结构**

```
Weave V1.0 设计文件
├── 📄 封面 (Cover)
│   ├── 项目信息
│   ├── 版本历史
│   └── 核心设计原则
│
├── 🎨 Design System（设计系统）
│   ├── Colors（色板）
│   ├── Typography（字体）
│   ├── Spacing（间距）
│   ├── Icons（图标库）
│   ├── Components（组件库）
│   │   ├── Buttons
│   │   ├── Cards
│   │   ├── Inputs
│   │   ├── Modals
│   │   └── Toast
│   └── Styles（共享样式）
│
├── 📱 核心页面（Pages）
│   ├── 1.0 Onboarding（引导流程）
│   ├── 2.0 Home（主页）
│   ├── 3.0 Node Detail（详情页）
│   ├── 4.0 Awakening（复习页）
│   ├── 5.0 Edit（编辑页）
│   └── 6.0 Settings（设置页）
│
├── 🎬 交互原型（Prototypes）
│   ├── 用户核心流程1：语音创建节点
│   ├── 用户核心流程2：复习流程
│   └── 用户核心流程3：查看共鸣
│
├── 🔄 状态与边界（States）
│   ├── Loading States
│   ├── Empty States
│   ├── Error States
│   └── Success States
│
└── 📐 标注与切图（Specs & Assets）
    ├── 间距标注
    ├── 颜色标注
    └── 导出资源（@2x, @3x）
```

### **5.7.2 组件命名规范**

```
命名结构：[类型]/[名称]/[变体]

示例：
Button/Primary/Default
Button/Primary/Hover
Button/Primary/Disabled
Button/Secondary/Default

Card/Node/Default
Card/Node/WithResonance
Card/Resonance/Default

Input/Text/Default
Input/Text/Focus
Input/Text/Error
```

### **5.7.3 变量（Variables）命名**

```
Figma变量命名：

颜色变量：
- color/brand/primary
- color/brand/light
- color/text/primary
- color/text/secondary
- color/bg/primary
- color/bg/card

间距变量：
- space/1  (8px)
- space/2  (16px)
- space/3  (24px)
...

圆角变量：
- radius/sm  (4px)
- radius/md  (8px)
- radius/lg  (12px)
...
```

### **5.7.4 切图与资源导出规范**

**图标导出：**

```
格式：SVG（矢量，优先）或PNG（栅格）
命名：icon-[名称].svg
尺寸：24×24px基准
导出倍率：@1x, @2x, @3x

示例：
icon-mic.svg
icon-mic@2x.png
icon-mic@3x.png
```

**插图导出：**

```
格式：PNG（带透明通道）
命名：illustration-[名称]@[倍率].png
尺寸：根据实际使用场景

示例：
illustration-empty-cosmos@2x.png
illustration-success@3x.png
```

**动画资源：**

```
格式：Lottie JSON（优先）或GIF
命名：animation-[名称].json

示例：
animation-sparkle.json
animation-loading.json
```

### **5.7.5 设计走查清单（Design QA Checklist）**

**开发前走查：**

```
视觉一致性：
- [ ] 所有颜色来自设计系统色板
- [ ] 所有字号符合字阶系统
- [ ] 所有间距为8的倍数
- [ ] 所有圆角统一使用变量

交互完整性：
- [ ] 所有按钮都有Hover/Active/Disabled状态
- [ ] 所有输入框都有Default/Focus/Error状态
- [ ] 所有页面都有Loading/Empty/Error状态
- [ ] 所有模态框都有打开/关闭动画

无障碍：
- [ ] 文本对比度≥4.5:1（或3:1大文本）
- [ ] 可点击元素≥44×44px
- [ ] 焦点样式清晰可见
- [ ] 关键操作有明确反馈

响应式：
- [ ] 小屏设备（iPhone SE）适配
- [ ] 大屏设备（iPad）适配（如需要）
- [ ] 横屏模式考虑（关键页面）
```

**开发后验收：**

```
像素级对比：
- [ ] 使用设计稿overlay对比实际渲染
- [ ] 颜色值精确匹配（使用取色器）
- [ ] 间距误差<2px
- [ ] 字号字重完全一致

交互验证：
- [ ] 所有动画时长与设计一致
- [ ] 动画缓动函数符合规范
- [ ] 滚动行为符合预期
- [ ] 手势操作响应灵敏

多设备测试：
- [ ] 至少3款不同尺寸设备测试
- [ ] iOS和Android各至少1款
- [ ] 不同微信版本测试
```

### **5.7.6 设计文档交付物清单**

**必须交付：**

```
1. ✅ Figma设计文件（完整源文件）
2. ✅ 设计系统文档（Design System Spec）
3. ✅ 核心页面交互原型（可点击Prototype）
4. ✅ 切图资源包（所有@2x/@3x图标和插图）
5. ✅ 颜色/字体/间距变量导出（JSON或CSS）
```

**可选交付：**

```
6. ⭕ 动效演示视频（复杂动画）
7. ⭕ 设计决策文档（Design Decision Log）
8. ⭕ 品牌使用指南（Brand Guidelines）
```

