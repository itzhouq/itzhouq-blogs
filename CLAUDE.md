# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 项目概述

这是一个静态博客网站（风飞扬itzhouq博客），无构建工具、无框架、无依赖，直接用浏览器打开 HTML 文件即可预览。

## 文件结构

- `index.html` — 博客首页，列出文章列表和精选内容，引用外部 `styles.css`
- `styles.css` — 全局样式，供 `index.html` 使用；使用 CSS 变量定义颜色、字体、间距系统
- `mimo-v2-ppt.html` — Xiaomi MiMo-V2 发布主题演示文稿（自包含，内联样式）
- `superpowers-ppt.html` — Superpowers AI 技能系统演示文稿（自包含，内联样式）
- `openclaw-wechat-ppt.html` — OpenClaw 微信插件发布主题演示文稿（自包含，内联样式）
- `ads.txt` — 广告投放配置文件
- `视频号.jpg` — 微信视频号二维码图片

## 架构约定

**演示文稿文件（`*-ppt.html`）：**
- 全部样式内联于 `<style>` 标签内，不依赖外部 CSS
- 使用 `.slide` / `.slide.active` 实现幻灯片切换，`display: none` 隐藏，`display: flex` 展示
- 通过键盘（左右方向键）和按钮控制翻页，JavaScript 内联于页面底部
- `overflow: hidden; height: 100vh` 使页面固定为全屏

**博客首页（`index.html` + `styles.css`）：**
- CSS 变量定义在 `:root` 中，颜色系统、字体、间距统一管理
- 容器最大宽度 `--container-max: 800px`，适配阅读体验
- 使用 Google Fonts（Inter 和 JetBrains Mono）

## 开发与预览

直接用浏览器打开对应 HTML 文件：

```bash
open index.html
open mimo-v2-ppt.html
open superpowers-ppt.html
open openclaw-wechat-ppt.html
```

新增文章时：在 `index.html` 的文章列表区域（`.articles` section）添加 `<article class="article-item">` 条目，并在 `index.html` 的精选区域（`.featured` section）更新精选卡片。

新增演示文稿时：参考现有 `*-ppt.html` 文件，使用内联 `<style>` 和 `<script>`，通过 `.slide` / `.slide.active` 类实现幻灯片切换。
