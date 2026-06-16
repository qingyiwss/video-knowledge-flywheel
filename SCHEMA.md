# Video Knowledge Flywheel — Schema

## Domain
AI 短视频创作全链路知识体系：剧本创作、提示词工程、角色一致性管理、工具链选型、平台运营、变现路径。

## Conventions
- 文件名：小写连字符，如 `character-consistency.md`
- 每个 wiki 页面带 YAML frontmatter
- 使用 `[[wikilinks]]` 互相链接，每页至少 2 个出链
- 更新页面必须更新 `updated` 日期
- 新页面必须添加到 `index.md` 对应分类
- 每次操作记录到 `growth-log.md`
- 含 3+ 来源的页面，段落末尾加来源标记

## Frontmatter
```yaml
---
title: 页面标题
created: YYYY-MM-DD
updated: YYYY-MM-DD
type: entity | concept | comparison | query | summary
tags: [见下方分类]
sources: [url-or-reference]
confidence: high | medium | low
---
```

## Tag Taxonomy

### 创作
- `script` — 剧本创作
- `storyboard` — 分镜设计
- `prompt` — 提示词工程

### 技术
- `character` — 角色一致
- `tool` — 工具链
- `workflow` — 生产流程
- `automation` — 自动化

### 平台
- `bilibili` — B 站运营
- `platform` — 平台规则

### 商业
- `monetization` — 变现
- `cost` — 成本核算

### 元
- `meta` — 知识库元信息
- `comparison` — 对比分析
