# 微信小程序电子相册 · 构建思路

项目目录：`~/Desktop/Wechat mini programe/`

**第一阶段需求：** [`requirements/phase1-requirements.md`](./requirements/phase1-requirements.md)（§0 已决议；NAS=`/Volumes/home/Dudu`；本阶段不加载像素）  
**变更日志：** [`changes/CHANGELOG.md`](./changes/CHANGELOG.md)（每次改动先读再追加）

## 核心思路（一句话）

小程序只做 UI 与鉴权入口；**NAS / 百度网盘一律经自有 HTTPS 相册 API（复用现有阿里云 ECS）** 访问；列表用缩略图，原图按需拉取且**不改写**存储侧原文件。

## 参与者

| 角色 | 职责 |
|------|------|
| 微信小程序 | 网格、预览、登录；只请求已备案合法域名 |
| 相册 API | 会话、目录索引、thumb 缓存、原图代理、百度 OAuth |
| NAS | `/mnt/nas_download/` 只读片库/相册根 |
| 百度开放平台 | OAuth、`imagelist`、`filemetas`/`dlink` |

## 时序图

- 可编辑源：[`diagrams/album-e2e-sequence.mmd`](./diagrams/album-e2e-sequence.mmd)
- 导出图：[`diagrams/album-e2e-sequence.png`](./diagrams/album-e2e-sequence.png)

### 重导 PNG

在本仓库 `docs/diagrams` 下执行：

```bash
cd "/Users/tangzhenghan/Desktop/Wechat mini programe/docs/diagrams"
npx -y @mermaid-js/mermaid-cli@11.4.2 -i album-e2e-sequence.mmd -o album-e2e-sequence.png -b transparent
```

## 阶段划分（与时序图一致）

1. **阶段 A 接入**：AppID、ECS 部署 API、合法域名、百度应用、NAS 根目录约定  
2. **阶段 B 登录/授权**：`wx.login` → 自有 session；可选百度 OAuth（token 仅服务端）  
3. **阶段 C 列表**：NAS 列目录 / 百度 `imagelist` → 本域 `thumbUrl`  
4. **阶段 D 原图**：NAS 流式读 / 百度 `dlink` 代理 → 预览或保存到手机  

## 后续代码落盘建议

```text
Wechat mini programe/
  docs/                 # 本文档与时序图
  miniprogram/          # 微信原生小程序（待建）
  album-api/            # 相册后端（待建，可部署到现有 ECS）
```

Cursor 调研 Skill（Agent 仓库）：`.cursor/skills/wechat-miniprogram-photo-album/`
