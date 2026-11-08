# 电子相册 · 变更日志

每次对小程序 / 相册 API / 本项目文档的实质性修改，**先读需求再改，改完在本文件顶部追加一条**（最新在上）。

格式：

```text
## YYYY-MM-DD — 简短标题
- 需求依据：phase1-requirements.md §x / 决议 Rx
- 改动：…
- 未做 / 边界：…
```

---

## 2026-11-08 — 同步至 GitHub

- 需求依据：用户要求将小程序相关代码同步到 GitHub
- 改动：初始化 git；仓库 https://github.com/JasonTang123/wechat-miniprogram-photo-album ；`main` 已推送（首提交含 miniprogram 壳、Phase 1 需求、CHANGELOG、Cursor 规则）
- 未做：未包含 Agent 仓库内 Skill/规则副本（仍在 `Desktop/Agent`）

## 2026-11-08 — 需求 v0.2：写入已决议 + 改前回顾流程

- 需求依据：用户确认建议方案；要求 Cursor 每次改小程序前回顾需求与上次修改
- 改动：
  - `docs/requirements/phase1-requirements.md` → v0.2，新增 §0 决议 R1–R7
  - 新增本 CHANGELOG
  - 新增 `.cursor/rules/wechat-miniprogram-req-first.mdc`（项目内）
  - Agent 仓库同步规则 + Skill 提示
- 未做：尚未实现 home/层级页与本机索引 API（下一迭代）

## 2026-11-08 — 需求 v0.1 + 基础框架预览成功

- 需求依据：第一阶段五条需求梳理
- 改动：首版需求文档；`miniprogram` 占位首页；测试号 AppID `wx038558ae61ab4757`；开发者工具预览成功
- 未做：NAS 树、层级导航、图片加载
