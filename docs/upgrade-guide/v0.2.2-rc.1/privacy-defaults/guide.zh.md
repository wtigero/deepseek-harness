---
kind: upgrade-guide
description: "会话上传、桌面分析和网络工具现在默认禁用。"
---

# 隐私默认值

[English](guide.md) | 中文

## 变更

发送至 DeepSeek API 的会话日志贡献默认禁用。基础 profile 的反馈遥测默认使用 `DISABLED`。桌面产品分析、插件清单元数据、网络搜索和网络抓取默认禁用。现有 profile、home 或命令行覆盖仍可启用这些功能。模型提供商仍可配置，远程提供商请求会离开计算机。这些设置不限制子进程或插件的网络访问。

Auto review 移除和重载现在使用 `fallbackPreset`，默认是 `workspace-write` 与 `ask` 审批。自定义后备预设必须限制写入并要求审批。

## 迁移

Windows 请使用 Node.js 24.x 中的 24.20.0 或更新版本。Node.js 24.16.0 可能在网络关闭期间崩溃；[24.20.0 发布说明](https://nodejs.org/en/blog/release/v24.20.0)包含 task-runner 修复。

1. 要启用 DeepSeek 会话日志贡献，请打开 **设置 → 通用 → 在使用官方模型 API 时上传 Session Log**。启用前请阅读会话日志包参考。
2. 要启用反馈遥测，请在启动前设置 `DSH_TELEMETRY_MODE=FEEDBACK_ONLY`。反馈可能上传先前的会话上下文。
3. 要启用网络工具，请在 profile 或 agent preset 的 `tool-web` 条目中设置 `search: true` 和/或 `fetch: true`。启用的抓取工具可以访问本地及私有网络地址。
4. 要启用桌面分析，请在 Desktop profile 的 `product-analytics` 条目中设置 `enabled: true`。
5. 检查当前 profile 和覆盖，并在隔离环境中验证行为。现有覆盖优先于这些默认值。
