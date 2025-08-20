---
project: nav
stars: 2
description: |-
    A Vitepress-based navigation website.
url: https://github.com/everfu/nav
---

# 导航网站

基于 VitePress 构建的现代化导航网站，采用 shadcn/ui 设计风格。

## ✨ 特性

- 🎨 现代化 UI 设计，支持深色/浅色模式切换
- 🔍 多搜索引擎支持（百度、谷歌、必应等）
- 📱 完全响应式设计，适配各种设备
- ⚡ 基于 Vue 3 + VitePress，性能优异
- 🎯 组件化架构，易于维护和扩展
- 🌐 支持 PWA，可离线访问

## 🚀 在线访问

访问地址：[https://everfu.github.io/nav/](https://everfu.github.io/nav/)

## 🛠️ 本地开发

### 环境要求

- Node.js 18+
- pnpm (推荐) 或 npm

### 安装依赖

```bash
# 使用 pnpm (推荐)
pnpm install

# 或使用 npm
npm install
```

### 开发服务器

```bash
# 启动开发服务器
pnpm dev

# 或
npm run dev
```

### 构建部署

```bash
# 构建生产版本
pnpm build

# 预览构建结果
pnpm preview
```

## 📁 项目结构

```
.
├── .github/workflows/     # GitHub Actions 自动部署配置
├── .vitepress/
│   ├── components/        # Vue 组件
│   │   ├── AppLayout.vue          # 主应用布局
│   │   ├── SiteHeader.vue         # 网站头部
│   │   ├── SearchSection.vue      # 搜索区域
│   │   ├── CategorySection.vue    # 分类区域
│   │   ├── NavigationCard.vue     # 导航卡片
│   │   ├── SiteFooter.vue         # 网站页脚
│   │   ├── ThemeToggle.vue        # 主题切换
│   │   └── SearchEngineSelector.vue # 搜索引擎选择器
│   ├── config/           # 配置文件
│   │   └── navigation.js # 导航数据配置
│   ├── theme/            # 主题配置
│   │   ├── index.js      # 主题入口
│   │   └── custom.css    # 自定义样式
│   ├── utils/            # 工具函数
│   └── config.js         # VitePress 配置
├── public/               # 静态资源
└── index.md             # 首页
```

## ⚙️ 配置说明

### 修改网站信息

编辑 `.vitepress/config/navigation.js` 文件：

```javascript
export const getSiteInfo = () => ({
  title: '您的网站标题',
  subtitle: '您的网站副标题',
  favicon: '/favicon.ico'
})
```

### 添加导航分类

在 `.vitepress/config/navigation.js` 中的 `categories` 数组添加新分类：

```javascript
{
  id: 'new-category',
  name: '新分类',
  items: [
    {
      id: 'item-1',
      name: '网站名称',
      description: '网站描述',
      url: 'https://example.com',
      icon: {
        light: '/icons/light-icon.png',
        dark: '/icons/dark-icon.png'
      }
    }
  ]
}
```

### 自定义搜索引擎

在 `searchEngines` 数组中添加新的搜索引擎：

```javascript
{
  id: 'custom-search',
  name: '自定义搜索',
  icon: 'custom-icon',
  color: '#ff6b6b',
  url: 'https://example.com/search?q={query}',
  placeholder: '搜索...'
}
```

## 🎨 主题定制

### CSS 变量

项目使用 CSS 变量进行主题定制，主要变量定义在 `.vitepress/theme/custom.css`：

```css
:root {
  --primary: 262 83% 58%;
  --background: 0 0% 100%;
  --foreground: 224 71% 4%;
  /* ... 更多变量 */
}

[data-theme="dark"] {
  --background: 224 71% 4%;
  --foreground: 213 31% 91%;
  /* ... 深色模式变量 */
}
```

### 组件样式

每个组件都有独立的样式文件，可以单独定制：

- 卡片样式：`NavigationCard.vue`
- 搜索框样式：`SearchSection.vue`
- 主题切换按钮：`ThemeToggle.vue`

## 🚀 部署

### GitHub Pages 自动部署

项目已配置 GitHub Actions 自动部署，推送到 `main` 分支即可自动部署到 GitHub Pages。

### 手动部署

```bash
# 构建
pnpm build

# 部署到您的服务器
# 将 .vitepress/dist 目录的内容上传到服务器
```

## 🤝 贡献

欢迎提交 Issue 和 Pull Request！

## 📄 许可证

[MIT License](LICENSE)
