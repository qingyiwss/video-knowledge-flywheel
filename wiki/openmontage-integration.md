---
title: OpenMontage 集成指南
created: 2026-06-17
updated: 2026-06-17
type: entity
tags: [openmontage, claude-code, automation, agent, integration]
confidence: high
sources: [OpenMontage GitHub, 部署实战]
---

# OpenMontage 集成指南

> **OpenMontage 已部署在 `/root/code/OpenMontage`，与 NΞXUS 的 Claude Code 集成。**

---

## 一、已部署状态

| 组件 | 状态 |
|------|------|
| Python 依赖 | ✅ 已安装 |
| Remotion (React 渲染引擎) | ✅ 已安装 |
| Piper TTS (离线配音) | ✅ 已安装 |
| 12 条 Pipeline 定义 | ✅ 就绪 |
| 20+ 技能文件 | ✅ 就绪 |
| 4 套视觉风格 | ✅ 就绪 |
| Demo 渲染 | ⚠️ 服务器 4GB 内存不足，本地机器可正常渲染 |

---

## 二、使用方法

### 2.1 最简单的使用方式

打开 Claude Code，进入 OpenMontage 目录，用自然语言发指令：

```bash
cd /root/code/OpenMontage
claude
```

然后说：

```
"做一个 60 秒的动画科普视频，解释神经网络如何学习"
```

Claude Code 会自动：
1. 读取 AGENT_GUIDE.md 的调度规则
2. 选择对应 Pipeline（如 `animated-explainer`）
3. 调用工具链（搜资料→写脚本→生图→配音→合成）
4. 输出 MP4

### 2.2 12 条可用 Pipeline

| Pipeline | 中文 | 适用场景 |
|----------|------|---------|
| `animated-explainer` | 动画科普 | 知识科普、产品介绍 |
| `cinematic` | 电影级短片 | 品牌宣传、故事短片 |
| `documentary-montage` | 纪录片蒙太奇 | 真实素材剪辑 |
| `talking-head` | 口播视频 | 单人讲解 |
| `animation` | Ghibli 风动画 | 艺术短片 |
| `character-animation` | 角色动画 | SVG 角色动画 |
| `clip-factory` | 片段工厂 | 批量短片段 |
| `podcast-repurpose` | 播客转视频 | 长内容拆短视频 |
| `screen-demo` | 屏幕演示 | 产品 Demo |
| `localization-dub` | 多语配音 | 翻译+配音 |
| `avatar-spokesperson` | 数字人播报 | 虚拟主播 |
| `hybrid` | 混合模式 | 自定义组合 |

### 2.3 4 套视觉风格

| 风格 | 文件 | 特点 |
|------|------|------|
| `clean-professional` | `styles/clean-professional.yaml` | 专业商务风 |
| `flat-motion-graphics` | `styles/flat-motion-graphics.yaml` | 扁平 MG 动画 |
| `minimalist-diagram` | `styles/minimalist-diagram.yaml` | 极简图解 |
| `anime-ghibli` | `styles/anime-ghibli.yaml` | 吉卜力风 |

### 2.4 零 API Key 可用功能

```bash
# 不需任何 API Key 就能用的：
✅ Piper TTS（离线配音）
✅ Remotion 动画组件（图表/文字/数据可视化）
✅ 免版权素材搜索
✅ FFmpeg 合成 + 字幕烧录

# 加了 API Key 能用的：
🔑 FAL_KEY → FLUX 生图 / Kling 视频 / Veo 视频
🔑 PEXELS_API_KEY → Pexels 实拍素材
🔑 ELEVENLABS_API_KEY → 高级 TTS
🔑 SUNO_API_KEY → AI 音乐生成
```

---

## 三、与我们的飞轮库协同

| 我们的强项 | OpenMontage 补足 |
|-----------|-----------------|
| 悬疑/甜宠/逆袭/搞笑 4 题材模板 | 自动搜索+脚本生成 Agent |
| 中文可灵生态 | Remotion 动画 + 离线 TTS |
| B 站运营策略 | 多平台多格式导出 |
| 角色一致性方法论 | 参考视频自动拆解分析 |
| 完整分镜模板 | 自动化质检（ffprobe） |

### 推荐工作流

```
1. 手动用飞轮库方法论 → 选题材、建角色、写剧本（我们的优势）
2. 剧本喂给 OpenMontage   → Agent 自动出分镜+提示词+配音+合成
3. 人工审核              → 用飞轮库验收清单
4. B 站发布              → 用飞轮库运营策略 + 数据反馈循环
```

---

## 四、常见指令

```bash
# 零 Key 测试
cd /root/code/OpenMontage
python -c "
from tools.tool_registry import registry
import json
registry.discover()
print(json.dumps(registry.provider_menu(), indent=2))
"

# 查看所有 Pipeline
ls pipeline_defs/

# 查看所有技能
cat skills/INDEX.md

# 重新安装（如果 npm 问题）
cd remotion-composer && rm -rf node_modules package-lock.json && npm install && cd ..
```

---

## 五、已知限制

| 限制 | 原因 | 解决 |
|------|------|------|
| 服务器渲染内存不足 | Chromium 需要 > 4GB | 本地机器运行，或加 swap |
| 零 Key 模式下无 AI 图片 | 纯 Remotion 动画组件 | 加 `FAL_KEY` |
| 纯英文生态 | 设计面向英文用户 | 我们用 Edge-TTS 做中文配音 |

---

## 详见
- [[production-pipeline]] — 我们的端到端生产流水线
- [[tool-chain]] — 工具链对比
- [OpenMontage GitHub](https://github.com/calesthio/OpenMontage)
