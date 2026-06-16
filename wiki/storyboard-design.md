---
title: 分镜设计方法论
created: 2026-06-17
updated: 2026-06-17
type: entity
tags: [storyboard, shot-design, cinematography, composition, visual-grammar]
confidence: high
sources: [StudioBinder, StoryboardCanvas, 电影摄影原理, AI短视频实战]
---

# 分镜设计方法论

> **分镜不是「把剧本画出来」。分镜是用镜头语言重新讲述故事——每一镜的景别、角度、运动都承载叙事意图。**

---

## 一、AI 短视频分镜铁律

| # | 规则 | 原因 |
|---|------|------|
| 1 | **一镜一意** | 一个镜头只传达一个信息点 |
| 2 | **景别必须有变化** | 连续 3 镜同一景别 = 视觉疲劳 |
| 3 | **跳轴禁止** | 跨 180° 线会让角色位置混乱 |
| 4 | **AI 优先固定机位** | 运动镜头崩率是固定镜头的 3-5 倍 |
| 5 | **特写镜头 ≤ 总量 30%** | AI 面部特写崩率最高 |
| 6 | **9:16 竖屏构图优先** | 从第一镜就按竖屏设计 |

---

## 二、景别体系

### 2.1 7 级景别

```
特写 ←─────────────────────────────→ 远景
 EC      C       MC      M       MW      W       EW
(极特)  (近景)  (中近)  (中景)  (中全)  (全景)  (极全)
```

### 2.2 每级功能

| 景别 | AI 提示词 | 叙事功能 | 崩率 |
|------|----------|---------|------|
| **EC 极特写** | `extreme close-up` | 强调关键细节（眼睛/手上的物品/手机屏幕） | ⚠️ 高 |
| **CU 近景** | `close-up` | 表情变化、情绪爆发、关键台词 | ⚠️ 中高 |
| **MC 中近景** | `medium close-up` | 对话场景主力、微表情+半身肢体 | ✅ 低 |
| **MS 中景** | `medium shot` | 双人对话、角色动作、场景交互 | ✅ 极低 |
| **MW 中全景** | `medium wide shot` | 角色入场、体态展示 | ✅ 极低 |
| **WS 全景** | `wide shot` | 建立场景、展示空间关系 | ✅ 极低 |
| **EW 极全景** | `extreme wide shot` | 开场定调、孤独感、史诗感 | ✅ 极低 |

> **AI 短视频黄金比例**：MC（30%）+ MS（30%）+ MW（20%）+ CU（15%）+ WS（5%）

### 2.3 AI 景别速查

| 中文 | 英文提示词 | 画面范围 |
|------|-----------|---------|
| 极特写 | `extreme close-up, face only` | 只拍眼睛/嘴唇/一只手 |
| 近景 | `close-up, face filling frame` | 肩以上，面部为主 |
| 中近景 | `medium close-up, chest up` | 胸部以上 |
| 中景 | `medium shot, waist up` | 腰部以上 |
| 中全景 | `medium wide shot, full body in frame` | 全身，少量环境 |
| 全景 | `wide shot, full figure with environment` | 全身+完整环境 |
| 极全景 | `extreme wide shot, tiny figure in landscape` | 角色只是画面中的小点 |

---

## 三、摄影机角度

### 3.1 6 种角度 & 叙事含义

| 角度 | AI 提示词 | 角色传达 | 使用场景 |
|------|----------|---------|---------|
| **平视** | `eye level` | 平等、自然、代入 | 对话、日常（主力） |
| **俯角** | `high angle, looking down` | 弱小、被压制、脆弱 | 角色受挫、反派俯视 |
| **仰角** | `low angle, looking up` | 强大、权威、威胁 | 角色崛起、boss 出场 |
| **斜角** | `dutch angle, tilted horizon` | 不安、混乱、失常 | 悬疑转折、精神崩溃 |
| **鸟瞰** | `bird's eye view, directly above` | 命运感、渺小、宿命 | 开场/结尾定调 |
| **过肩** | `over the shoulder shot` | 代入视角、对话关系 | 双人对话主力 |

### 3.2 AI 角度提示词

```
【平视】eye level, camera at subject's eye height
【俯角】high angle shot, camera looking down at subject, 
        45 degree downward
【仰角】low angle shot, camera looking up at subject, 
        30 degree upward
【斜角】dutch angle, camera tilted 15 degrees, 
        diagonal horizon line
【鸟瞰】bird's eye view, camera directly above subject
【过肩】over the shoulder, behind one character's shoulder,
        focusing on the other character
```

---

## 四、构图规则

### 4.1 三分法（基础）

```
┌─────────┬─────────┬─────────┐
│         │         │         │
│   左    │   中    │   右    │
│  1/3    │  1/3    │  1/3    │
│         │  👤     │         │
├─────────┼─────────┼─────────┤
│         │         │         │
│         │         │         │
├─────────┼─────────┼─────────┤
│         │         │         │
│         │         │         │
└─────────┴─────────┴─────────┘

角色放在 1/3 线交点上（👤位置），视线方向留空。
AI 提示词：「subject positioned on left third, 
            looking right into open space」
```

### 4.2 空间深度

| 类型 | 描述 | 适合 |
|------|------|------|
| **深空间** | 前景清晰→中景角色→远景模糊 | 戏剧性、悬疑、情绪张力 |
| **浅空间** | 角色贴背景，无中间层 | 喜剧、日常、对话 |

**AI 提示词**：
```
深空间：「shallow depth of field, subject in mid-ground sharp, 
         foreground blurred, background out of focus」

浅空间：「flat composition, subject close to background, 
         minimal depth」
```

### 4.3 视线引导

| 技巧 | 效果 | AI 实现 |
|------|------|---------|
| 引导线 | 观众视线被引到角色 | 走廊/栏杆/道路在背景中指向角色 |
| 框架构图 | 通过门框/窗框看角色 | 「framed by doorway, subject visible through door frame」 |
| 留白 | 角色视线方向留空间 | 「subject on right third, negative space on left」 |

---

## 五、180° 轴线法则

### 5.1 什么是轴线

```
        角色A ←───视线───→ 角色B
          │                  │
    机位1 (左侧)      机位2 (右侧) ← 跳轴！
          │                  │
    机位3 (左侧)      机位4 (右侧) ← 跳轴！
```

**规则：所有机位必须在轴线的同一侧。** 一旦跨过轴线，观众会以为角色位置互换了。

### 5.2 AI 短视频轴线攻略

```
设定第一镜机位后：
  ✅ 后续所有镜头都在同一侧的 180° 范围内
  ✅ 需要换侧时，先插一个中性镜头（空镜/特写/正对镜头）
  ❌ 禁止直接跳轴

示例：
  镜1：角色A左侧看B右侧（机位在A左肩后）
  镜2：B面部特写（中性镜头，可安全切换）
  镜3：角色B左侧看A右侧（机位换到B左肩后）← 已安全跨轴
```

---

## 六、镜头运动（AI 安全版）

### 6.1 安全运动

| 运动 | AI 提示词 | 崩率 | 用途 |
|------|----------|------|------|
| 静止 | `static, no camera movement` | 极低 | 主力镜头 |
| 缓推 | `slow push in, dolly forward slowly` | 低 | 情绪渐进 |
| 缓拉 | `slow pull out, dolly back slowly` | 低 | 揭示环境 |
| 缓摇 | `slow pan right/left` | 低 | 跟随视线 |
| 微呼吸 | `subtle handheld, slight natural shake` | 中 | 真实感 |

### 6.2 危险运动（AI 避免）

| 运动 | 问题 |
|------|------|
| 快速变焦 | 画面撕裂 |
| 剧烈手持 | 不可控抖动 |
| 环绕 + 推近组合 | 变形率高 |
| 跟拍行走 | 角色步态崩 |

> **AI 短视频原则：80% 镜头用固定机位，20% 用缓推/缓拉。**

---

## 七、镜头衔接规则

### 7.1 景别变化律

```
❌ 中景 → 中景（跳切感）
✅ 中景 → 近景 → 中景（有变化）

❌ 全景 → 极特写（跳跃太大）
✅ 全景 → 中景 → 近景 → 极特写（渐进）
```

### 7.2 30 秒短剧镜序模板

```
01  💥 钩子（CU/MC，1镜，3秒）
02  🌍 建立场景（WS/MW，1镜，2秒）
03  👤 角色登场（MS，1镜，2秒）
04  🎭 展开冲突（MC-MS交替，2-3镜，8秒）
05  🔄 第一次反转（CU，1镜，3秒）
06  ⚡ 高潮（MC-CU，2镜，6秒）
07  🚪 留白结尾（WS/MW，1镜，3秒）

总计：约 9-11 镜，30 秒
```

### 7.3 转场规则

| 转场 | 效果 | 使用 |
|------|------|------|
| 硬切 | 直接跳下一镜 | 主力（90%） |
| 淡入淡出 | 场景/时间切换 | 场景变化 |
| 匹配剪辑 | 同构图跳不同内容 | 对比/时间流逝 |
| 闪白 | 短暂白屏 | 回忆/震惊 |

---

## 八、AI 竖屏构图要点

### 8.1 9:16 竖屏特殊规则

```
竖屏黄金区：
┌──────────┐
│  安全区  │ ← 标题/字幕不要超出
│ ┌──────┐ │
│ │ 核心  │ │ ← 角色面部在这个区域
│ │ 画面  │ │
│ └──────┘ │
│  安全区  │
└──────────┘
```

| 规则 | 说明 |
|------|------|
| 角色面部在画面**上 1/3** | 下方留给字幕 |
| 双人对话用**对角构图** | 左上角色A ← → 右下角色B |
| 避免角色在画面正中 | 用三分法偏移 |
| 远景留天留地 | 天空占上 1/3，地面占下 1/3 |

---

## 详见
- [[script-writing-rules]] — 剧本→分镜翻译链路
- [[prompt-templates]] — 摄影机运动提示词
- [[production-standard]] — 全流程规范
