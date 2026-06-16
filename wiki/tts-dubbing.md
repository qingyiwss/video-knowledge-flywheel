---
title: TTS 配音全链路
created: 2026-06-17
updated: 2026-06-17
type: entity
tags: [tts, audio, voice, production, dubbing]
confidence: high
sources: [Edge-TTS 文档, 火山引擎 TTS API, 剪映官方, CosyVoice 开源项目]
---

# TTS 配音全链路

> **AI 短剧的灵魂在配音。画面可以差一点，声音不行观众秒划走。**

---

## 一、工具选型

### 1.1 4 方案对比

| 方案 | 费用 | 中文质量 | 角色区分 | 情绪控制 | 上手难度 |
|------|------|---------|---------|---------|---------|
| **Edge-TTS** | 免费 | ⭐⭐⭐ | ⭐⭐ | ⭐⭐ | 极低 |
| **剪映内置配音** | 免费 | ⭐⭐⭐ | ⭐ | ⭐ | 极低 |
| **火山引擎 TTS** | ¥0.2/千字 | ⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐ | 低 |
| **CosyVoice 2** | 免费(自部署) | ⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐ | 中高 |

### 1.2 推荐方案

| 阶段 | 用哪个 | 原因 |
|------|--------|------|
| **试水期**（前 3 集） | Edge-TTS | 免费、零配置、中文可选 10+ 音色 |
| **验证期**（数据反馈后） | 火山引擎 | ¥0.2/千字，一集 30 秒约 ¥0.02 |
| **成熟期**（角色固化后） | CosyVoice 2 | 音色克隆 = 角色专属声音 |

### 1.3 Edge-TTS 快速上手

```bash
# 安装
pip install edge-tts

# 列出所有中文音色
edge-tts --list-voices | grep zh-CN

# 生成配音（男声·云希）
echo "你终于来了。" | edge-tts --voice zh-CN-YunxiNeural --write-media line01.mp3

# 生成配音 + 字幕文件
edge-tts --text "你终于来了。" --voice zh-CN-YunxiNeural \
  --write-media line01.mp3 --write-subtitles line01.vtt
```

---

## 二、中文音色选角指南

### 2.1 Edge-TTS 中文音色库

| 音色名 | 性别 | 特质 | 适合角色 |
|--------|------|------|---------|
| `zh-CN-YunxiNeural` | 男 | 沉稳、磁性 | **男主主力**、霸道总裁 |
| `zh-CN-YunjianNeural` | 男 | 清亮、少年 | 年轻男主、学生 |
| `zh-CN-YunyangNeural` | 男 | 播音腔、正式 | 旁白、新闻报道 |
| `zh-CN-YunfengNeural` | 男 | 低沉、成熟 | 中年角色、反派 |
| `zh-CN-XiaoxiaoNeural` | 女 | 温柔、甜美 | **女主主力**、甜宠 |
| `zh-CN-XiaoyiNeural` | 女 | 活泼、清脆 | 少女、闺蜜 |
| `zh-CN-YunxiaNeural` | 女 | 知性、成熟 | 御姐、女强人 |
| `zh-CN-XiaochenNeural` | 女 | 温柔但有距离 | 高冷女主 |

### 2.2 角色→音色匹配规则

| 角色类型 | 性别 | 推荐音色 | 替代 |
|---------|------|---------|------|
| 冷峻男主 | 男 | YunxiNeural（沉稳） | YunfengNeural（低沉） |
| 温柔男主 | 男 | YunjianNeural（清亮） | YunxiNeural |
| 反派/大佬 | 男 | YunfengNeural（低沉） | — |
| 甜美女主 | 女 | XiaoxiaoNeural（温柔） | XiaochenNeural |
| 活泼女配 | 女 | XiaoyiNeural（清脆） | — |
| 御姐/女王 | 女 | YunxiaNeural（成熟） | XiaochenNeural |
| 旁白 | 任意 | YunyangNeural（播音） | — |

> **铁律：每剧 3-5 个音色上限，多了观众分不清。配角可以复用音色但调语速区分。**

---

## 三、配音工作流

### 3.1 从剧本到配音文件

```
01 剧本台词                  02 预处理
┌──────────────────┐        ┌──────────────────┐
│ 林晨：「来不及了」 │  ──→  │ 去角色名 + 情绪标注 │
│ 小雅：「什么？」   │        │ 林晨-01：来不及了   │
└──────────────────┘        │ （低沉，急促）      │
                            │ 小雅-02：什么？     │
                            │ （惊讶，上扬）      │
                            └──────────────────┘

03 逐句生成                  04 文件组织
┌──────────────────┐        ┌──────────────────┐
│ edge-tts ...      │  ──→  │ 04-素材/E01/配音/  │
│ → E01_VO_chen_01  │        │   chen_01.mp3     │
│   edge-tts ...    │        │   xiaoya_02.mp3   │
│ → E01_VO_xiaoya_01│        │   旁白_00.mp3      │
└──────────────────┘        └──────────────────┘
```

### 3.2 命名规范

```
{剧集}_{类型}_{角色}_{序号}.mp3

示例：
E01_VO_chen_01.mp3      # 林晨第1句
E01_VO_chen_02.mp3      # 林晨第2句
E01_VO_xiaoya_01.mp3    # 小雅第1句
E01_VO_narrator_00.mp3  # 旁白
```

### 3.3 参数调节

| 参数 | 范围 | 效果 | 适用 |
|------|------|------|------|
| `--rate` | -50% ~ +50% | 语速 | 紧张 +10%，沉思 -15% |
| `--pitch` | -20Hz ~ +20Hz | 音高 | 区分同音色不同角色 |

```bash
# 紧张场景：语速加快
edge-tts --voice zh-CN-YunxiNeural --rate=+15% \
  --text "来不及了！" --write-media line.mp3

# 沉思场景：语速放慢
edge-tts --voice zh-CN-YunxiNeural --rate=-10% \
  --text "我一直在想一个问题..." --write-media line.mp3
```

---

## 四、情绪配音指南

### 4.1 TTS 情绪控制

TTS 不会自动识别情绪——**必须用文本技巧引导**。

| 想要的效果 | 文本技巧 | 示例 |
|-----------|---------|------|
| 急促/紧张 | 短句 + 感叹号 | 「谁！」→ 不是「是谁在那里」 |
| 缓慢/沉思 | 加省略号 + 逗号 | 「我…一直，在想一个问题…」 |
| 上扬/疑问 | 结尾问号 | 「你说什么？」 |
| 低沉/压抑 | 句号 + 无标点 | 「我知道了。」→ 不是「我知道了！」 |
| 温柔/轻声 | 加括号标注语境 | 「（轻声）别走。」 |

### 4.2 情绪标注格式

```
【剧本台词】→【TTS 输入】

剧本：林晨（愤怒）：「你到底想干什么？」
TTS ：你到底想干什么？
        ↑ 只用标点控制情绪，不加角色名

剧本：小雅（哭泣）：「我以为你不会回来了…」
TTS ：我以为…你不会回来了…
        ↑ 省略号 = 哽咽效果

剧本：林晨（冷笑）：「有意思。」
TTS ：有意思。
        ↑ 句号 + 短句 = 冷淡
```

> ⚠️ 不要在 TTS 输入中加角色名和情绪括号。TTS 会读出来。

---

## 五、多角色配音管理

### 5.1 角色-音色映射表

每部剧配音前先建表：

```markdown
## 《剧名》配音映射表

| 角色 | 音色 | 语速 | 音高 | 备注 |
|------|------|------|------|------|
| 林晨 | zh-CN-YunxiNeural | 0% | 0Hz | 男主，沉稳 |
| 小雅 | zh-CN-XiaoxiaoNeural | +5% | +2Hz | 女主，温柔偏活泼 |
| 老王 | zh-CN-YunfengNeural | -5% | -3Hz | 中年反派 |
| 旁白 | zh-CN-YunyangNeural | -10% | 0Hz | 播音腔 |

规则：
- 男女主角的语速差距 ≥ 5%
- 同性别角色的音高差距 ≥ 3Hz
```

### 5.2 批量生成脚本

```python
#!/usr/bin/env python3
"""批量 TTS 生成"""
import subprocess, json

# 角色配置
VOICES = {
    "chen": {"voice": "zh-CN-YunxiNeural", "rate": "0%"},
    "xiaoya": {"voice": "zh-CN-XiaoxiaoNeural", "rate": "+5%"},
}

# 台词列表
lines = [
    ("chen", "01", "来不及了。"),
    ("xiaoya", "01", "什么来不及？"),
    ("chen", "02", "一切。"),
]

for role, num, text in lines:
    v = VOICES[role]
    out = f"E01_VO_{role}_{num}.mp3"
    cmd = [
        "edge-tts", "--text", text,
        "--voice", v["voice"],
        "--rate", v["rate"],
        "--write-media", out
    ]
    subprocess.run(cmd)
    print(f"✅ {out}")
```

---

## 六、配音质量验收

### 6.1 逐句检查

- [ ] 每个角色音色与映射表一致
- [ ] 语速与场景情绪匹配
- [ ] 没有机器人腔（锯齿感/破碎感）
- [ ] 多角色对话时音色有足够区分度
- [ ] 背景无杂音/电流声

### 6.2 场景级检查

| 检查项 | 标准 |
|--------|------|
| 对话节奏 | 两句间隔 0.3-0.5 秒，不能同时开始 |
| 情绪一致 | 同一场景情绪基调统一 |
| 音量一致 | 所有配音文件响度一致（用 FFmpeg 归一化） |

### 6.3 音量归一化

```bash
# 将所有配音文件归一化到同一响度
for f in E01_VO_*.mp3; do
  ffmpeg -i "$f" -af loudnorm=I=-16:LRA=11:TP=-1.5 "norm_$f" -y
done
```

---

## 七、进阶：火山引擎 TTS

### 7.1 为什么升级

| 对比 | Edge-TTS | 火山引擎 |
|------|----------|---------|
| 音色数 | ~12 中文 | 50+ 中文 |
| 情绪标签 | ❌ 不支持 | ✅ 支持 `happy/sad/angry` |
| 语速范围 | -50%~+50% | 0.25x-4.0x |
| 角色克隆 | ❌ | ✅ 音色复刻 |
| 费用 | 免费 | ¥0.2/千字 |

### 7.2 火山引擎情绪参数

```json
{
  "text": "你终于来了。",
  "voice_type": "zh_male_qingrun",
  "emotion": "cold",      // happy/sad/angry/fear/cold/gentle
  "speed_ratio": 0.9,
  "volume_ratio": 1.0,
  "pitch_ratio": 0.0
}
```

> 火山引擎接入示例见 `concepts/AI_VIDEO_STANDARD.md` 第七章。

---

## 详见
- [[production-standard]] — 全流程规范（含目录结构）
- [[script-writing-rules]] — 对白 TTS 约束规则
- [[tool-chain]] — 工具链选型
