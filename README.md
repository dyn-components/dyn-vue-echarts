# dyn-vue-echarts

[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)

## 目录

- [介绍](#介绍)
- [安装](#安装)
- [快速开始](#快速开始)
- [属性说明](#属性说明)
- [事件](#事件)
- [方法](#方法)
- [自定义样式](#自定义样式)
- [示例](#示例)
- [发布](#发布)
- [贡献指南](#贡献指南)
- [维护者](#维护者)
- [许可证](#许可证)
- [致谢](#致谢)

## 介绍

简要介绍该组件的功能和用途。

## 安装

安装依赖

```bash
pnpm add echarts
```


```bash
pnpm add unplugin-vue-components dyn-components --save-dev
```

修改 vite.config.js

```ts
import { defineConfig } from "vite";
import vue from "@vitejs/plugin-vue";
import Components from "unplugin-vue-components/vite";
import DynComponents, { unpluginDynVueComponentsResolver } from "dyn-components";

// https://vitejs.dev/config/
export default defineConfig({
  plugins: [
    vue(),
    Components({
      resolvers: [unpluginDynVueComponentsResolver()],
    }),
    DynComponents(),
  ],
  resolve: {
    alias: {
      dyn_components: "/dyn_components",
    },
  },
});
```

## 快速开始

```ts
// global import theme.css
import "dyn-components/theme.css";
```

```vue
<template>
  <dyn-vue-echarts :options="options"></dyn-vue-echarts>
</template>
```

## 属性说明

## 属性（Props）

| 属性名  | 类型                | 默认值 | 必填 | 描述         |
| ------- | ------------------- | ------ | ---- | ------------ |
| options | `EChartsCoreOption` | `{}`   | N    | echarts 配置 |

### 详细说明

- **options**

  - 类型: `EChartsCoreOption`
  - 默认值: `{}`
  - 描述: echarts 属性配置

## 发布

```bash
dyn-components publish
```
