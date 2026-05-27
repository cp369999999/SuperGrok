

{
  "extends": "next/core-web-vitals"
}

# dependencies
/node_modules
/.pnp
.pnp.js

# testing
/coverage

# next.js
/.next/
/out/

# production
/build

# misc
.DS_Store
*.pem

# debug
npm-debug.log*
yarn-debug.log*
yarn-error.log*

# local env files
.env*.local
.env

# vercel
.vercel

# typescript
*.tsbuildinfo
next-env.d.ts

/** @type {import('next').NextConfig} */
const nextConfig = {
  reactStrictMode: true,
};

export default nextConfig;

/// <reference types="next" />
/// <reference types="next/image-types/global" />

// NOTE: This file should not be edited
// see https://nextjs.org/docs/app/api-reference/config/typescript for more information.

{
  "name": "supergrok-shop",
  "version": "1.0.0",
  "private": true,
  "scripts": {
    "dev": "next dev",
    "build": "next build",
    "start": "next start",
    "lint": "next lint"
  },
  "dependencies": {
    "next": "14.2.15",
    "react": "18.3.1",
    "react-dom": "18.3.1"
  },
  "devDependencies": {
    "@types/node": "20.14.10",
    "@types/react": "18.3.3",
    "@types/react-dom": "18.3.0",
    "autoprefixer": "10.4.19",
    "eslint": "8.57.0",
    "eslint-config-next": "14.2.15",
    "postcss": "8.4.39",
    "tailwindcss": "3.4.6",
    "typescript": "5.5.3"
  }
}

module.exports = {
  plugins: {
    tailwindcss: {},
    autoprefixer: {},
  },
};

# SuperGrok Shop（supergrok.shop）

SuperGrok / Grok 中文使用教程与会员开通指南单页站。
技术栈：**Next.js 14（App Router）+ TypeScript + Tailwind CSS**，可直接部署到 Vercel。

本站为第三方 AI 工具教程与服务说明站，非官方网站。

---

## 一、文件结构

```
supergrok-shop/
├── package.json              # 依赖与脚本
├── next.config.mjs           # Next.js 配置
├── tsconfig.json             # TypeScript 配置
├── tailwind.config.ts        # 主题色（黑金）与动画
├── postcss.config.js
├── .eslintrc.json
├── .gitignore
├── public/
│   ├── robots.txt            # 搜索引擎抓取规则
│   └── sitemap.xml           # 站点地图
└── src/
    ├── app/
    │   ├── layout.tsx        # 全局 SEO metadata（title/description/OG）
    │   ├── page.tsx          # 首页组装 + 结构化数据(JSON-LD)
    │   └── globals.css       # 全局样式 / 设计变量
    ├── components/
    │   ├── Header.tsx        # 顶部导航（含移动端菜单）
    │   ├── Hero.tsx          # 首屏
    │   ├── WhatIs.tsx        # SuperGrok 是什么
    │   ├── Steps.tsx         # 开通五步教程
    │   ├── Comparison.tsx    # SuperGrok vs Grok 对比表
    │   ├── Audience.tsx      # 适合谁（6 卡片）
    │   ├── DomesticUsage.tsx # 国内使用注意事项
    │   ├── OrderEntry.tsx    # 自助下单入口 + 客服
    │   ├── Faq.tsx           # 常见问题（折叠）
    │   ├── Footer.tsx        # 页脚 + 免责声明
    │   └── icons.tsx         # 内置 SVG 图标（无需第三方图标库）
    └── data/
        └── site.ts           # ⭐ 全站文案与配置（主要改这里）
```

---

## 二、本地启动

需要 Node.js 18.18+（推荐 20+）。

```bash
# 1. 安装依赖
npm install

# 2. 本地开发（默认 http://localhost:3000）
npm run dev

# 3. 生产构建 + 本地预览
npm run build
npm run start
```

---

## 三、部署到 Vercel

方式 A（推荐，最简单）：

1. 把项目推到 GitHub。
2. 打开 https://vercel.com → New Project → 选择该仓库。
3. Framework 会自动识别为 **Next.js**，无需任何额外设置，直接 Deploy。
4. 在 Vercel 项目的 Domains 里绑定 `supergrok.shop`。

方式 B（命令行）：

```bash
npm i -g vercel
vercel        # 首次部署
vercel --prod # 发布到生产环境
```

> 部署后记得在 layout / robots / sitemap 里确认域名是 `https://supergrok.shop`（已默认填好）。

---

## 四、❶ 在哪里改「下单链接」

只改一个地方：**`src/data/site.ts`** 顶部的 `ORDER_URL`。

```ts
export const ORDER_URL = "https://gpt3plus.com"; // 改成你的真实商品链接
```

全站所有「自助下单 / 立即下单 / 购买」按钮都会自动跟着变，无需改组件。

---

## 五、❷ 在哪里改「客服信息」

同样在 **`src/data/site.ts`** 的 `CONTACT`：

```ts
export const CONTACT = {
  telegram: "请联系频道客服",
  telegramUrl: "https://gpt3plus.com",
  wechat: "DCpluspro",          // 微信号
};
```

---

## 六、其它常改位置（都在 `src/data/site.ts`）

| 想改什么 | 改哪个变量 |
| --- | --- |
| 站点标题 / 描述 / 域名 / 关键词（SEO） | `SITE` |
| 顶部导航项 | `NAV` |
| 首屏标签 | `HERO_TAGS` |
| 首屏右侧卡片内容 | `HERO_CARD_ITEMS` |
| 开通步骤 | `STEPS` |
| SuperGrok vs Grok 对比 | `COMPARE` |
| 适合谁（6 卡片） | `AUDIENCE` |
| 国内使用注意事项 | `CHINA_TIPS` |
| 常见问题 FAQ | `FAQ` |

> 改完 `SITE.domain` 后，记得同步修改 `public/robots.txt` 与 `public/sitemap.xml` 里的域名。

---

## 七、SEO 说明

- `title` / `description` / `keywords` / OpenGraph 在 `src/app/layout.tsx` 自动读取 `SITE`。
- 页面只有一个 `<h1>`（首屏主标题），其余均为 `<h2>` 结构。
- `page.tsx` 内置 FAQ + WebSite 的 JSON-LD 结构化数据，利于搜索结果展示。
- `robots.txt`、`sitemap.xml` 已在 `public/` 准备好。

---

## 八、免责声明

本站为第三方 AI 工具教程与服务说明站，非 Grok、xAI、X 官方网站。所有产品名称、商标和品牌归其各自所有者所有。下单前请仔细阅读商品说明与售后规则。

import type { Config } from "tailwindcss";

const config: Config = {
  content: [
    "./src/app/**/*.{ts,tsx}",
    "./src/components/**/*.{ts,tsx}",
  ],
  theme: {
    extend: {
      colors: {
        // 深色暖黑背景
        ink: {
          DEFAULT: "#0a0806",
          2: "#0f0b07",
          3: "#15100a",
        },
        // 卡片表面
        surface: {
          DEFAULT: "#171008",
          2: "#1d150c",
          hi: "#241a0e",
        },
        // 黑金主色
        gold: {
          DEFAULT: "#c9a24b",
          bright: "#e6c878",
          soft: "#d8b86a",
          deep: "#8a6a2c",
        },
        // 文字
        cream: {
          DEFAULT: "#f4ede0",
          muted: "#b6a890",
          dim: "#897c66",
        },
        line: "rgba(201,162,75,0.16)",
      },
      fontFamily: {
        sans: [
          "-apple-system",
          "BlinkMacSystemFont",
          "PingFang SC",
          "Microsoft YaHei",
          "Hiragino Sans GB",
          "Noto Sans SC",
          "Source Han Sans SC",
          "Helvetica Neue",
          "Arial",
          "sans-serif",
        ],
      },
      maxWidth: {
        container: "1200px",
      },
      boxShadow: {
        gold: "0 0 0 1px rgba(201,162,75,0.18), 0 18px 50px -20px rgba(201,162,75,0.25)",
        card: "0 24px 60px -30px rgba(0,0,0,0.8)",
      },
      backgroundImage: {
        "gold-line": "linear-gradient(90deg, transparent, rgba(201,162,75,0.5), transparent)",
        "card-glow": "radial-gradient(120% 120% at 0% 0%, rgba(201,162,75,0.10), transparent 60%)",
      },
      keyframes: {
        "fade-up": {
          "0%": { opacity: "0", transform: "translateY(16px)" },
          "100%": { opacity: "1", transform: "translateY(0)" },
        },
        "glow-pulse": {
          "0%,100%": { opacity: "0.5" },
          "50%": { opacity: "1" },
        },
      },
      animation: {
        "fade-up": "fade-up 0.7s cubic-bezier(0.16,1,0.3,1) both",
        "glow-pulse": "glow-pulse 4s ease-in-out infinite",
      },
    },
  },
  plugins: [],
};

export default config;

{
  "compilerOptions": {
    "lib": ["dom", "dom.iterable", "esnext"],
    "allowJs": true,
    "skipLibCheck": true,
    "strict": true,
    "noEmit": true,
    "esModuleInterop": true,
    "module": "esnext",
    "moduleResolution": "bundler",
    "resolveJsonModule": true,
    "isolatedModules": true,
    "jsx": "preserve",
    "incremental": true,
    "plugins": [{ "name": "next" }],
    "paths": {
      "@/*": ["./src/*"]
    }
  },
  "include": ["next-env.d.ts", "**/*.ts", "**/*.tsx", ".next/types/**/*.ts"],
  "exclude": ["node_modules"]
}
