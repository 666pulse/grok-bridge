# grok-bridge Chrome 版

基于 Google Chrome 的 Grok Bridge，与 Safari 版功能完全一致。

## 前置条件

- macOS with Google Chrome
- 登录 [grok.com](https://grok.com)（免费或 SuperGrok）
- Chrome > View > Developer > Allow JavaScript from Apple Events ✓

## 启动

```bash
python3 scripts/grok_bridge_chrome.py --port 29998
```

默认端口 `29998`（Safari 版为 `19998`，互不冲突，可同时运行）。

## API

| Method | Path | Description |
|--------|------|-------------|
| POST | `/chat` | 发送 prompt，等待 Grok 回复 |
| POST | `/new` | 重置对话（重新加载 grok.com） |
| GET | `/health` | 健康检查（Chrome URL、Grok 状态） |
| GET | `/history` | 读取当前页面对话内容 |

## 用法

```bash
# 发送问题
curl -X POST http://localhost:29998/chat \
  -d '{"prompt":"最近1天科技行业发生了什么重要的事"}'

# 健康检查
curl http://localhost:29998/health

# 查看当前对话
curl http://localhost:29998/history

```

```sh
# 重置对话后再问
curl -X POST http://localhost:29998/new
curl -X POST http://localhost:29998/chat \
  -d '{"prompt":"最近1天 AI行业发生了什么重要的事"}'
```

## 与 Safari 版的区别

| | Safari 版 | Chrome 版 |
|---|---|---|
| 脚本 | `grok_bridge.py` | `grok_bridge_chrome.py` |
| 默认端口 | 19998 | 29998 |
| JS 执行 | `do JavaScript ... in current tab` | `execute active tab ... javascript` |
| 前置设置 | Safari > 开发 > 允许来自 Apple Events 的 JavaScript | Chrome > View > Developer > Allow JavaScript from Apple Events |

两个版本可以同时运行，分别控制 Safari 和 Chrome 窗口。
