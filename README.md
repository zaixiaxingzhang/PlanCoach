# PlanCoach
# PlanCoach 项目概述

## 项目简介

PlanCoach 是一个基于 HTML、CSS 和 JavaScript 构建的单页应用 (SPA)，旨在帮助用户将复杂任务分解为可管理的子任务，并提供 AI 辅助的建议和时间估算。该应用支持多种 AI 提供商（如 Ollama、OpenAI、Claude 等）。

## 技术栈

- **前端**: HTML5, CSS3, JavaScript (ES6+)
- **本地存储**: localStorage
- **API 通信**: Fetch API
- **打包/部署**: 通过 `manifest.json` 配置，支持打包为移动应用 (Android/iOS)

## 项目结构

```
plancoach/
├── index.html          # 应用入口页面
├── styles.css          # 应用样式
├── script.js           # 应用主逻辑
└── apiModule.js        # AI API 通信模块
```

## 核心功能

1.  **任务管理**:
    *   创建新任务
    *   查看任务列表 (按状态和时间排序)
    *   查看任务详情 (复杂度、时间估算、AI 建议、子任务)
    *   完成/取消完成子任务
    *   删除任务
    *   自动清理 15 天前已完成的任务
2.  **AI 集成**:
    *   支持多种 AI 提供商 (Ollama, SiliconFlow, OpenAI, Claude, Gemini, DeepSeek)
    *   可配置 API 端点和密钥
    *   可选择不同的 AI 模型
    *   AI 用于任务名称生成、复杂度评估、时间估算、子任务分解和提供建议
3.  **用户界面**:
    *   响应式设计，适配移动设备
    *   主视图、任务创建模态框、任务详情视图、设置窗口
    *   自定义下拉选择组件
    *   平滑的动画和过渡效果
4.  **数据存储**:
    *   使用 `localStorage` 进行本地缓存
    *   模拟文件系统将任务数据持久化到 `localStorage` 的特定键中

## 开发约定

- **代码风格**: 使用原生 JavaScript，遵循现代 ES6+ 语法。
- **模块化**: `apiModule.js` 负责所有与 AI API 相关的逻辑，与主应用逻辑 (`script.js`) 分离。
- **状态管理**: 应用状态集中存储在 `appState` 对象中。
- **事件处理**: 主要使用事件委托来处理用户交互。
- **日志记录**: 使用 `logMessage` 函数记录应用运行时的信息、警告和错误，并存储到 `localStorage`。
- **错误处理**: 在关键操作（如 API 调用、DOM 操作）中使用 try-catch 块进行错误捕获和处理。
- **API 通信**: 使用 `fetch` API 进行网络请求，并实现了超时和重试机制。

## 构建和运行

1.  **运行**:
    *   由于这是一个静态网页应用，可以直接在浏览器中打开 `index.html` 文件运行。
    *   为了获得完整的功能（特别是 API 调用），建议通过本地服务器运行，例如使用 VS Code 的 Live Server 插件或 Python 的 `http.server` 模块。
2.  **配置**:
    *   首次运行时，用户需要在设置窗口中配置 AI API 提供商、端点、密钥和模型。
    *   对于本地运行的 Ollama，默认端点为 `http://127.0.0.1:11434`。
    *   对于在线 API (如 OpenAI, Claude)，需要提供有效的 API 密钥。

## 任务存储实现

-   任务数据同时存储在 `localStorage` 中（作为缓存）和模拟的文件系统中（作为持久化存储）。
-   模拟文件系统通过在 `localStorage` 中使用特定的键（如 `plancoach/task/...`）来存储每个任务的文本格式数据。
