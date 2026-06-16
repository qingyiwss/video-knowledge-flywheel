---
title: 提示词模板库 v2.0
created: 2026-06-17
updated: 2026-06-17
type: entity
tags: [prompt, character, script, negative-prompt, camera]
confidence: high
sources: [可灵官方文档, Artlist Blog, VIDEOAI.ME, Ambience AI, 实战经验]
---

# 提示词模板库 v2.0

> **核心发现**：加一个聚焦的负面提示词，可用镜头产出率从 23.8% 提升到 55.6%（减少 57% 的重生成次数）。

## 一、提示词工程铁律

| # | 规则 | 为什么 |
|---|------|--------|
| 1 | **风格词全剧统一** | 混入新风格词 = 角色崩脸 |
| 2 | **角色外貌一字不变** | 每次 prompt 复制粘贴角色卡原文 |
| 3 | **动作只选「安全动作」** | 大动作崩脸，小动效稳定 |
| 4 | **负面词 ≤ 8 个** | 5-8 个负面词效果比 20+ 个高 23% |
| 5 | **正面不写"不要XX"** | AI 先理解"XX"再忽略，适得其反 |
| 6 | **无模糊形容词** | 「漂亮」→「下颌线条分明，鼻梁高挺」 |
| 7 | **光照/环境同场景复用** | 同一场景所有镜头用完全相同的光照描述 |
| 8 | **每镜必挂参考图** | 文字描述 + 角色母图 = 双重锚定 |

---

## 二、通用提示词结构

### 2.1 文生图（Text-to-Image）

```
[画质词] [主体描述(角色卡原文)] [脸部细节] [服装细节] [动作] [光照] [景别] [比例]

标准示例：
电影级真实风格。一位28岁亚洲男性，黑色短发，下颌线条分明，深棕色眼睛。
身穿白色衬衫，领口敞开。右手握着咖啡杯，视线望向窗外。
柔和的侧光从左侧打入。半身中景，直视镜头，9:16竖屏构图。
```

### 2.2 图生视频（Image-to-Video）

```
[动作序列] [约束条件] [禁止项]

标准示例：
同一个角色缓慢转头面向镜头，嘴角微微上扬，视线从咖啡杯移向镜头。
保持相同的面部特征、白色衬衫、柔和侧光、电影风格。平滑控制动作。
```

### 2.3 文生视频（Text-to-Video）

```
[Shot type] of [subject] [action/movement], [environment], [camera movement], [lighting], [style]

示例：
Medium close-up of a 28-year-old Asian man, slowly turning his head toward camera, 
modern office at night, camera slowly pushes in, warm overhead light, cinematic realism, 9:16.
```

---

## 三、按类型分类模板

### 3.1 🎭 悬疑/惊悚短剧

**画质词**：`电影级写实 | 暗调电影风格 | 高对比度`
**光照**：`单侧顶光 | 阴影切割面部 | 冷色底光 | 窗外霓虹光渗入`
**镜头偏好**：`中近景 | 特写 | 低角度仰拍 | 缓慢推拉`

```
【悬疑凝视镜头】
电影级写实，暗调高对比。{角色描述}。靠墙站立，背部紧贴墙壁，右眼在阴影中，
左眼被窗外霓虹光照亮。缓慢眨眼，喉结轻微滚动。冷蓝色霓虹光从左窗打入。
面部特写，低角度仰拍，9:16竖屏。

【悬疑场景：走廊】
暗调电影风格。空旷的医院走廊，日光灯忽明忽暗，尽头一扇半开的门。
摄影机缓慢向前推进。冷白色荧光灯闪烁。远景，低角度，9:16竖屏。
```

**负面提示词库（悬疑）**：
```
blur, distort, low quality, jittery eyes, unnatural motion, 
flickering highlights, overexposed, warm lighting
```

> ⚠️ 关键：悬疑片要拒绝「暖色调」和「过曝」，这两项会直接毁掉氛围。

---

### 3.2 💕 甜宠/言情短剧

**画质词**：`柔焦电影风格 | 清新写实 | 柔和色彩`
**光照**：`金色时刻自然光 | 柔光箱正面光 | 暖黄室内光 | 窗户漫射光`
**镜头偏好**：`半身中景 | 双人中景 | 浅景深 | 轻微手持感`

```
【甜宠对视镜头】
柔焦电影风格，清新柔和。{角色A描述}。与{角色B}面对面站立，
距离30厘米，微微低头看着她，嘴角上扬。金色时刻自然光从侧面洒入。
双人中景，浅景深虚化背景，轻微呼吸感手持，9:16竖屏。

【甜宠场景：咖啡馆】
柔焦电影风格。街角咖啡馆靠窗座位，木桌上两杯咖啡冒着热气。
窗外夕阳金色光线漫入。空镜，缓慢向右平移，9:16竖屏。
```

**负面提示词库（甜宠）**：
```
blur, distort, low quality, warping fingers, plastic skin, 
harsh shadows, cold lighting, dark mood
```

> ⚠️ 关键：甜宠片拒绝「硬阴影」「冷色光」「暗调氛围」。

---

### 3.3 🚀 逆袭/爽文短剧

**画质词**：`商业广告级写实 | 高饱和度 | 锐利清晰`
**光照**：`三点布光 | 顶光 + 底反光 | 高调照明 | 轮廓光`
**镜头偏好**：`全身中景 | 低角度仰拍 | 慢动作 | 快速推拉`

```
【逆袭出场镜头】
商业广告级写实，高饱和度。{角色描述}。大步向前走，
西装下摆飘动，视线坚定直视前方。三点布光，轮廓光勾勒肩线。
全身中景，低角度仰拍，慢动作，9:16竖屏。

【逆袭场景：公司大堂】
商业广告级写实。现代企业大堂，大理石地面反光，员工自动让开一条路。
摄影机从地面升起至平视。高调照明，干净无阴影。中景，9:16竖屏。
```

**负面提示词库（逆袭）**：
```
blur, distort, low quality, warping fingers, jittery eyes, 
dim lighting, muted colors, amateur camera
```

> ⚠️ 关键：逆袭片拒绝「暗光」「低饱和」「业余摄影感」。

---

### 3.4 😂 搞笑/吐槽短剧

**画质词**：`明亮写实风格 | 自然饱和度 | 轻喜剧调色`
**光照**：`均匀面光 | 自然日光 | 办公室荧光灯 | 无戏剧化阴影`
**镜头偏好**：`中景 | 特写（表情） | 快速变焦 | 轻微广角畸变`

```
【搞笑反应镜头】
明亮写实风格。{角色描述}。目瞪口呆，嘴巴微张，眉毛上挑，
瞳孔缩小。突然眨了两下眼。均匀白色面光，无阴影。
面部特写，轻微广角畸变增加喜剧感，9:16竖屏。

【搞笑场景：办公室】
明亮写实风格。开放式办公室，同事们齐刷刷转头看向同一个方向，
每人表情夸张各异。自然日光 + 顶灯。中景，缓慢右摇，9:16竖屏。
```

**负面提示词库（搞笑）**：
```
blur, distort, low quality, warping fingers, jittery eyes, 
dark mood, dramatic lighting, realistic tears
```

> ⚠️ 关键：搞笑片拒绝「暗调」「戏剧化光影」「写实眼泪」（眼泪崩了像恐怖片）。

---

## 四、负面提示词完整库

### 4.1 通用基础集（每镜必加）

```
blur, distort, low quality, warping fingers, frozen lips, jittery eyes
```

实测：6 个基础负面词减少约 40% 的可见瑕疵。

### 4.2 按镜头类型添加

| 类型 | 追加负面词 | 适用场景 |
|------|-----------|----------|
| 🎭 近景/特写 | `plastic skin, floating teeth, double chin warping, head shake` | 面部是焦点 |
| 🏃 动作镜头 | `unnatural motion, stuttered movement, flickering highlights, motion blur` | 有显著运动 |
| 👥 多人镜头 | `face swap, character merge, identity drift, extra limbs` | 2+ 人同框 |
| 🏠 场景空镜 | `warping walls, floating furniture, bending doorframes, jittery sky` | 无人物 |
| 🎨 风格化 | `realistic skin, photographic texture, 3D render look` | 动漫/手绘风 |

### 4.3 不同模型适配

**可灵 2.x（主力）**：
```
no camera drift, no handheld movement, no sudden zooms, 
no facial warping, no changing facial features, no flicker, no motion blur
```

> 可灵默认行为偏「电影感」，频繁加 drifting camera / 面部微变。用这 7 个负面词稳定画幅。

**可灵 1.6**：额外加 `no exaggerated motion, no erratic movement`

### 4.4 禁忌

| ❌ 错误做法 | ✅ 正确做法 |
|------------|------------|
| 堆 20+ 负面词 | 5-8 个精准词 |
| `ugly, bad quality, disgusting` | 不用主观评判词 |
| 负面词和正面描述矛盾 | 不写「剧烈运动」又禁止 motion |
| 把负面提示当风格工具 | 负面只防崩，不塑风格 |

---

## 五、摄影机运动指令库

### 5.1 基础运动

| 指令 | 中文说明 | 适用 |
|------|---------|------|
| `slow dolly in` | 摄影机缓慢向前推 | 揭示、强调 |
| `slow dolly out` | 摄影机缓慢向后拉 | 退场、留白 |
| `slow pan right` | 缓慢向右摇 | 跟随视线 |
| `slow pan left` | 缓慢向左摇 | 跟随视线 |
| `slow tilt up` | 缓慢向上摇 | 展示高度 |
| `slow tilt down` | 缓慢向下摇 | 坠落感 |
| `static, no camera movement` | 固定机位 | 对话、表情 |
| `subtle handheld` | 微呼吸感手持 | 增强真实感 |

### 5.2 进阶组合

| 组合 | 效果 | 示例用途 |
|------|------|---------|
| `slow dolly in + tilt down` | 推近 + 向下摇 | 角色低头看手中物品 |
| `slow pan right + dolly out` | 右摇 + 后退 | 揭示更大场景 |
| `slow orbit around subject` | 环绕主体 | 角色内心独白 |

### 5.3 可灵需要避免的镜头

```
❌ fast zoom / sudden zoom    → 画面撕裂
❌ rapid pan                  → 运动模糊
❌ whip pan                   → 完全崩
❌ extreme close-up on face   → 皮肤质感诡异
❌ handheld shake             → 不可控抖动
```

---

## 六、角色一致性提示词策略

### 6.1 角色卡 → 提示词映射

角色卡写好后，**所有分镜的提示词中，角色描述部分直接复制粘贴，一字不改**。

```
【角色卡：林晨】
年龄：28岁
外貌：亚洲男性，黑色短发，下颌线条分明，深棕色眼睛，鼻梁高挺，薄唇
常穿：白色尖领长袖衬衫，银色扣子，黑色西裤
标志物：左手腕银色机械表
```

### 6.2 各景别中的角色描述

| 景别 | 描述重点 | 示例 |
|------|---------|------|
| 特写（脸） | 只写面部 + 光照 | `{角色描述}。面部特写，柔光。` |
| 中景（半身） | 面部 + 服装 + 动作 | `{角色描述}。半身，右手举杯，柔光。` |
| 全景（全身） | 面部 + 全身服装 + 体态 | `{角色描述}。全身站立，双臂自然下垂，柔光。` |
| 背影 | 发型 + 服装 + 体态 | `黑色短发，白色衬衫背影，肩宽背直。` |

### 6.3 多角色同框

```
【双人场景】
{角色A描述}。与{角色B描述}同框。
角色A站在左侧，面向右侧；角色B站在右侧，面向左侧。
距离彼此 50 厘米。双人中景，9:16竖屏。

负面：face swap, character merge, identity drift, extra limbs
```

---

## 七、常见失败模式 & 修复

| 症状 | 错误原因 | 修复提示词 |
|------|---------|-----------|
| 脸变了 | 参考图不够清晰 | 换更清晰母图 + 加大面部特征描写 |
| 嘴不动但配音 | frozen lips 问题 | 加负面词 `frozen lips` |
| 衣服颜色变了 | 描述不够具体 | `白色衬衫` → `白色尖领长袖衬衫，银色扣子` |
| 突然变年轻/老 | 光照改变皮肤质感 | 锁定光照词的顺序和用词 |
| 手部崩坏 | AI 通病 | 近景避免手入画；必须入画时加 `warping fingers` |
| 镜头莫名漂移 | 可灵默认 camera drift | 明确写 `static, no camera movement` |
| 背景元素乱入 | 场景描述模糊 | 加负面 `no extra objects, no background clutter` |
| 风格突然动漫化 | 混入了风格描述 | 删除所有场景描述中可能的风格暗示 |
| 眨眼像抽搐 | jittery eyes | 加负面 `jittery eyes, unnatural blinking` |
| 多人脸互换 | face swap | 加负面 `face swap, character merge` |

---

## 八、温度 / Seed 策略

### 8.1 Seed 管理

| 策略 | 做法 | 适用 |
|------|------|------|
| **锁 Seed** | 同一角色不同镜头用同一 seed | 最大化一致性 |
| **换 Seed** | 不同场景换 seed | 需要场景变化 |
| **随机 Seed** | 不设 seed | 探索性尝试 |

```
建议：角色定妆照确定后，记录该 seed，同角色所有镜头用同一 seed。
不同场景（如家→办公室）换 seed，但同场景内锁定。
```

### 8.2 可灵创作参数建议

| 参数 | 推荐值 | 说明 |
|------|--------|------|
| 时长 | 5 秒 | 10 秒视频崩率显著高于 5 秒 |
| 分辨率 | 1080p | 标准输出，性价比最高 |
| 创意度 | 0.5-0.7 | 不要拉到 1.0（崩率高） |
| 与参考图关联度 | 0.8-0.9 | 角色一致性关键参数 |

---

## 九、完整实战示例

### 悬疑短剧 E01—镜头#03

```
【正面提示词】
电影级写实，暗调高对比。一位28岁亚洲男性，黑色短发，下颌线条分明，
深棕色眼睛，鼻梁高挺，薄唇。身穿白色尖领长袖衬衫，银色扣子。
身体靠在墙上，右眼在阴影中，左眼被窗外霓虹光照亮，喉结轻微滚动。
冷蓝色霓虹光从左侧窗户打入。面部特写，低角度仰拍，缓慢推近，9:16竖屏。

【负面提示词】
blur, distort, low quality, jittery eyes, unnatural motion, 
flickering highlights, warm lighting, overexposed, plastic skin

【参数】
时长: 5秒 | 创意度: 0.6 | 关联度: 0.85 | Seed: 固定角色seed
```

---

## 详见
- [[character-consistency]] — 角色一致性管理
- [[production-standard]] — 全流程规范
- [[script-writing-rules]] — 剧本写作规则
