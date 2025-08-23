---
project: MeowNocode
stars: 190
description: |-
    memos类开源高颜值便签应用
url: https://github.com/y-shi23/MeowNocode
---

# Meow App
![meow.png](https://pic.oneloved.top/2025-08/meow_1754197450654.png)
Meow App 是一个简洁的笔记应用，支持本地存储和云端同步。你可以使用Supabase或Cloudflare D1作为云端数据库。
## 功能亮点：
- 画布模式，便于整理思绪
- 热力图数据统计，满满成就感
- 模糊语法，适用于记忆场景
- 每日回顾，温故而知新
- AI对话，你问它答
....

## 特别感谢
- 使用nocode<https://nocode.cn>制作。
- 部分组件代码源于网络。

## demo
不含D1数据库（麻烦帮我冲一下UV和PV，球球了）：https://flomo.nocode.host/
含D1数据库：https://memo.oneloved.top/
D1公共实例的登录密钥是：`meow`。请勿上传不良信息和个人信息。

## 本地开发
### 安装依赖
```
npm install
```

### 启动开发服务器
```
npm run dev
```

## 部署

### 1. 静态网页托管+Supabase部署

#### 配置Supabase
1. 在 [Supabase](https://supabase.com) 创建一个新项目
2. 获取项目的URL和anon key
3. 在项目根目录创建`.env`文件，添加以下内容：
   ```
   VITE_SUPABASE_URL=你的Supabase项目URL
   VITE_SUPABASE_ANON_KEY=你的Supabase anon key

   PASSWORD= #配置后，访问前端页面需要密码。可选
   ```

#### 初始化数据库
1. 在Supabase控制台的SQL编辑器中运行`supabase-schema.sql`文件
2. 这将创建所需的表和索引

#### 部署应用
你可以将应用部署到任何支持静态网站托管的服务，如Vercel、Netlify等。

### 2. 使用Cloudflare Workers/Pages和D1数据库部署

#### 准备工作
1. 安装Wrangler CLI：
   ```
   npm install -g wrangler
   ```
2. 登录Cloudflare账户：
   ```
   wrangler login
   ```

#### 创建D1数据库
1. 创建一个新的D1数据库：
   ```
   wrangler d1 create meow-app-db
   ```
2. 记下输出的database_id

#### 设置访问密钥
1. 生成一个安全的密钥（可以使用以下命令）：
   ```
   openssl rand -base64 32
   ```
   或者使用在线工具生成一个随机字符串。
2. 在Cloudflare Pages设置中，添加环境变量：
   - 变量名：`PASSWORD`
   - 变量值：你生成的密钥
3. 这个密钥将用于保护你的应用，防止未授权访问。

#### 配置wrangler.toml
1. 编辑`wrangler.toml`文件，将`your-database-id`替换为上一步获取的database_id

#### 初始化D1数据库
1. 执行以下命令初始化数据库：
   ```
   wrangler d1 execute meow-app-db --file=./d1-schema.sql --remote
   ```

#### 部署到Cloudflare Pages
1. 将你的代码推送到GitHub仓库
2. 在Cloudflare控制台中连接你的GitHub仓库
3. 配置构建设置：
   - 构建命令：`npm run build`
   - 构建输出目录：`build`
4. 在Pages设置中，添加D1数据库绑定：
   - 变量名：`DB`
   - 数据库：选择你创建的D1数据库

## 使用指南

### 云端同步
1. 在应用中打开设置
2. 在"数据"标签页中，启用"云端数据同步"
3. 选择你想要使用的云服务提供商（Supabase或Cloudflare D1）
4. 如果使用Supabase，需要先登录GitHub账号
5. 如果使用Cloudflare D1，需要先输入D1鉴权密钥进行验证
   - 密钥可以通过左侧栏中的密钥图标按钮输入
   - 也可以在设置界面中的D1选项卡中输入
6. 点击"备份到云端"或"从云端恢复"按钮进行数据同步

### 本地数据管理
1. 在设置中的"数据"标签页，你可以导出和导入本地数据
2. 导出的数据是JSON格式，包含所有想法、标签和设置

## 项目结构
- `src/` - 源代码
  - `components/` - React组件
  - `context/` - React Context
  - `lib/` - 工具库和数据库服务
- `supabase-schema.sql` - Supabase数据库架构
- `d1-schema.sql` - D1数据库架构
- `worker.js` - Cloudflare Worker代码
- `wrangler.toml` - Cloudflare Workers配置

# 其他
## 数据库初始化与迁移

本项目支持两套后端存储：Cloudflare D1 与 Supabase。以下指引用于「全新初始化」与「更新既有数据库」。


### 更新既有数据库（迁移）

若你已有数据库，但表结构缺少新增字段，可按下面执行简单迁移。

- Cloudflare D1（SQLite）

```sql
-- 如缺少头像字段
ALTER TABLE user_settings ADD COLUMN avatar_config TEXT DEFAULT '{"imageUrl":""}';

-- 如缺少画布配置字段
ALTER TABLE user_settings ADD COLUMN canvas_config TEXT;

-- 如缺少双链数据
ALTER TABLE memos ADD COLUMN backlinks TEXT DEFAULT '[]';

-- 如缺少 memos.created_at 索引
CREATE INDEX IF NOT EXISTS idx_memos_created_at ON memos(created_at);
```

- Supabase（Postgres）

```sql
-- 如缺少头像字段
ALTER TABLE user_settings ADD COLUMN IF NOT EXISTS avatar_config JSONB DEFAULT '{"imageUrl":""}'::jsonb;

-- 如缺少画布配置字段
ALTER TABLE user_settings ADD COLUMN IF NOT EXISTS canvas_config JSONB;

-- 如缺少双链数据
ALTER TABLE memos ADD COLUMN IF NOT EXISTS backlinks JSONB DEFAULT '[]'::jsonb;

-- 如缺少 memos.created_at 索引
CREATE INDEX IF NOT EXISTS idx_memos_created_at ON memos(created_at);
```

执行后即可使用设置页面的“同步到云端/从云端恢复”。

