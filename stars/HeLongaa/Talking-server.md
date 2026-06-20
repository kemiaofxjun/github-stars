---
project: Talking-server
stars: 5
description: |-
    现代化的社交动态管理服务，基于 Cloudflare Workers，支持 Markdown、图片上传、标签管理。
url: https://github.com/HeLongaa/Talking-server
---

# Talking-server

![Cloudflare Workers](https://img.shields.io/badge/Cloudflare%20Workers-2025-orange.svg)
![JavaScript](https://img.shields.io/badge/JavaScript-ES2022-blue.svg)
![KV](https://img.shields.io/badge/Cloudflare%20KV-Storage-purple.svg)
![R2](https://img.shields.io/badge/Cloudflare%20R2-Storage-green.svg)
![Markdown](https://img.shields.io/badge/Markdown-Support-lightgrey.svg)
![License](https://img.shields.io/badge/License-MIT-red.svg)

> 现代化的社交动态管理服务，基于 Cloudflare Workers，支持 Markdown、图片上传、标签管理。

## 功能特性
- 管理员登录（GitHub OAuth）
- 发布、编辑、删除动态（支持 Markdown 内容、标签、图片上传）
- 动态内容存储于 Cloudflare KV，图片存储于 R2
- 响应式美观 UI，支持移动端
- Markdown 渲染，图片自动插入

## 目录结构
   ```
   wrangler.toml         # Cloudflare Workers 配置
   src/
     admin.js           # 管理后台主逻辑
     api.js             # API 路由
     auth.js            # 认证逻辑
     index.js           # 入口
     public.js          # 公共页面
     utils.js           # 工具函数
   ```

## 快速开始

### 1. 配置 GitHub OAuth 应用

在部署之前，需要先在 GitHub 上创建 OAuth 应用：

1. 访问 GitHub Settings → Developer settings → OAuth Apps → New OAuth App
2. 填写应用信息：
   - **Application name**: 填写应用名称（如：Talking-server）
   - **Homepage URL**: 填写你的部署域名（如：`https://your-domain.com`）
   - **Authorization callback URL**: **重要！** 填写 `https://your-domain.com/auth/callback`
     - ⚠️ 确保这个 URL 与你实际部署的域名完全一致
     - 本地开发时使用：`http://localhost:8787/auth/callback`
3. 创建后，保存 **Client ID** 和 **Client Secret**，后续配置需要使用

### 2. 创建 Cloudflare 资源

1. 在 Cloudflare 控制台创建 KV 命名空间（用于存储动态数据）
2. 创建 R2 存储桶（用于存储图片）
3. 记录它们的 ID 和名称

### 3. 配置 `wrangler.toml`

在项目根目录创建 `wrangler.toml` 文件：

```toml
name = "social-moments"
main = "src/index.js"
compatibility_date = "2025-07-21"

[[kv_namespaces]]
binding = "POSTS_KV"
id = "你的KV命名空间ID"

[[r2_buckets]]
binding = "POST_BUCKET"
bucket_name = "你的R2存储桶名称"

[vars]
GITHUB_CLIENT_ID = "你的GitHub Client ID"
GITHUB_CLIENT_SECRET = "你的GitHub Client Secret"
ADMIN_USERS = '["你的GitHub用户名"]'
```

**重要提示**：
- 将 `ADMIN_USERS` 中的值替换为你的 GitHub 用户名（JSON 数组格式）
- 支持多个管理员：`'["user1", "user2"]'`

### 4. 安装依赖

```bash
pnpm install
# 或
npm install
```

### 5. 本地开发

```bash
wrangler dev
```

本地开发时，OAuth 回调地址为：`http://localhost:8787/auth/callback`

### 6. 部署到 Cloudflare Workers

```bash
wrangler deploy
```

### 7. 配置自定义域名（推荐）

1. 在 Cloudflare Workers 控制台中，为你的 Worker 绑定自定义域名
2. **确保绑定的域名与 GitHub OAuth 应用中配置的域名一致**
3. 更新 GitHub OAuth 应用的回调 URL 为：`https://your-domain.com/auth/callback`

## 常见问题

### OAuth 授权失败

如果遇到 OAuth 授权失败，请检查：

1. **GitHub OAuth 应用的回调 URL 是否正确**
   - 必须完全匹配你的部署域名
   - 格式：`https://your-domain.com/auth/callback`
   - 注意：不要有多余的斜杠或路径

2. **Cloudflare Workers 绑定的域名**
   - 确保已在 Workers 设置中绑定自定义域名
   - Workers 的域名必须与 OAuth 应用中填写的域名一致

3. **环境变量配置**
   - 检查 `wrangler.toml` 中的 `GITHUB_CLIENT_ID` 和 `GITHUB_CLIENT_SECRET` 是否正确
   - 检查 `ADMIN_USERS` 中是否包含你的 GitHub 用户名

### 无权限访问

如果显示"无权限访问"，请确认：
- 你的 GitHub 用户名已添加到 `wrangler.toml` 的 `ADMIN_USERS` 列表中
- 用户名拼写正确（区分大小写）

## 依赖环境
- Cloudflare Workers
- Cloudflare KV & R2
- Node.js 18+
- Wrangler CLI

## License
MIT

