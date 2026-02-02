# OpenClaw-Docker-CN-IM

> 🚀 **推荐搭配**：OpenClaw 功能强大但 Token 消耗较大，推荐配合 [AIClient-2-API](https://github.com/justlovemaki/AIClient-2-API) 项目使用，将各大 AI 客户端转换为标准 API 接口，实现无限 Token 调用，彻底解决 Token 焦虑！本项目已支持 OpenAI 和 Claude 两种协议，可直接对接 AIClient-2-API 服务。

**OpenClaw 中国IM插件整合版 Docker 镜像**

本项目是 OpenClaw 的中国IM平台整合Docker版本，预装并配置了飞书、钉钉、QQ机器人、企业微信等主流中国IM软件的插件，让您可以快速部署一个支持多个中国IM平台的 AI 机器人网关。

## Docker 镜像地址

### 🐳 Docker Hub
- **仓库地址**: https://hub.docker.com/r/justlikemaki/openclaw-docker-cn-im
- **拉取命令**:
  ```bash
  docker pull justlikemaki/openclaw-docker-cn-im:1.0.0
  docker pull justlikemaki/openclaw-docker-cn-im:latest
  ```

## 快速开始

### 使用 Docker Compose（推荐）

1. **下载配置文件**
   ```bash
   # 下载 docker-compose.yml 和 .env.example
   wget https://raw.githubusercontent.com/justlovemaki/OpenClaw-Docker-CN-IM/main/docker-compose.yml
   wget https://raw.githubusercontent.com/justlovemaki/OpenClaw-Docker-CN-IM/main/.env.example
   ```

2. **配置环境变量**
   ```bash
   # 复制环境变量模板
   cp .env.example .env
   
   # 编辑 .env 文件，填入您的配置
   nano .env  # 或使用其他编辑器
   ```

3. **启动服务**
   ```bash
   docker-compose up -d
   ```

4. **查看日志**
   ```bash
   docker-compose logs -f
   ```

### 最小配置说明

启动容器至少需要配置以下环境变量：

| 环境变量 | 说明 | 示例 |
|---------|------|------|
| `MODEL_ID` | AI 模型名称 | `gpt-4` |
| `BASE_URL` | AI 服务 API 地址 | `https://api.openai.com/v1` |
| `API_KEY` | AI 服务 API 密钥 | `sk-xxx...` |
| `FEISHU_APP_ID` | 飞书应用 ID（可选） | `cli_xxx...` |
| `FEISHU_APP_SECRET` | 飞书应用密钥（可选） | `xxx...` |

> 💡 **提示**：如需启用其他 IM 平台（钉钉、QQ机器人、企业微信），请参考下方的详细配置说明。

## 特性

- 🚀 **开箱即用**：预装所有中国主流IM平台插件
- 🔧 **灵活配置**：通过环境变量轻松配置各平台凭证
- 🐳 **Docker 部署**：一键启动，无需复杂配置
- 🔌 **插件整合**：集成飞书、钉钉、QQ机器人、企业微信等平台
- 📦 **数据持久化**：支持配置和工作空间数据持久化
- 💻 **OpenCode AI**：内置 OpenCode AI 代码助手，支持智能代码生成和分析
- 🎭 **Playwright 支持**：预装 Playwright 浏览器自动化工具，支持网页操作和截图
- 🗣️ **中文 TTS**：支持中文语音合成（Text-to-Speech），可将文本转换为语音

## 支持的平台

### IM 平台
- ✅ 飞书（Feishu/Lark）
- ✅ 钉钉（DingTalk）
- ✅ QQ 机器人（QQ Bot）
- ✅ 企业微信（WeCom）
- ✅ 自带内置其它APP（可选）

### 集成工具
- ✅ OpenCode AI - AI 代码助手
- ✅ Playwright - 浏览器自动化
- ✅ 中文 TTS - 语音合成

本目录包含构建 OpenClaw-Docker-CN-IM 镜像所需的所有文件。

## 文件说明

- [`Dockerfile`](openclaw/Dockerfile) - Docker 镜像构建文件
- [`init.sh`](openclaw/init.sh) - 容器初始化脚本（作为主程序运行）
- [`docker-compose.yml`](openclaw/docker-compose.yml) - Docker Compose 配置文件
- [`.env.example`](openclaw/.env.example) - 环境变量配置模板
- [`.dockerignore`](openclaw/.dockerignore) - Docker 构建忽略文件
- [`openclaw.json`](openclaw/openclaw.json) - OpenClaw 默认配置文件（可选，容器会自动生成）

## 构建镜像

在 `openclaw` 目录下执行以下命令构建镜像：

```bash
cd openclaw
docker build -t openclaw:local .
```

## 配置环境变量

在运行容器之前，建议先配置环境变量：

1. 复制环境变量模板文件：
```bash
cp .env.example .env
```

2. 编辑 `.env` 文件，修改相应的配置值（如 API_KEY、BASE_URL 等）

## 运行容器

### 方式 1：使用 Docker 命令

```bash
docker run -d \
  --name openclaw-gateway \
  --privileged \
  -e MODEL_ID=model id \
  -e BASE_URL=http://xxxxx/v1 \
  -e API_KEY=123456 \
  -e API_PROTOCOL=openai-completions \
  -e CONTEXT_WINDOW=200000 \
  -e MAX_TOKENS=8192 \
  -e FEISHU_APP_ID=your-app-id \
  -e FEISHU_APP_SECRET=your-app-secret \
  -e DINGTALK_CLIENT_ID=your-dingtalk-client-id \
  -e DINGTALK_CLIENT_SECRET=your-dingtalk-client-secret \
  -e DINGTALK_ROBOT_CODE=your-dingtalk-robot-code \
  -e DINGTALK_CORP_ID=your-dingtalk-corp-id \
  -e DINGTALK_AGENT_ID=your-dingtalk-agent-id \
  -e QQBOT_APP_ID=your-qqbot-app-id \
  -e QQBOT_CLIENT_SECRET=your-qqbot-client-secret \
  -e WECOM_TOKEN=your-token \
  -e WECOM_ENCODING_AES_KEY=your-aes-key \
  -e OPENCLAW_GATEWAY_TOKEN=7788414 \
  -e OPENCLAW_GATEWAY_BIND=lan \
  -e OPENCLAW_GATEWAY_PORT=18789 \
  -v ~/.openclaw:/home/node/.openclaw \
  -v ~/.openclaw/workspace:/home/node/.openclaw/workspace \
  -p 18789:18789 \
  -p 18790:18790 \
  --restart unless-stopped \
  justlikemaki/openclaw-docker-cn-im:latest
```

### 方式 2：使用 Docker Compose（推荐）

确保已配置 `.env` 文件后，直接运行：

```bash
docker-compose up -d
```

Docker Compose 会自动读取 `.env` 文件中的环境变量。

## 环境变量说明

### 模型配置

本项目支持 **OpenAI 协议**和 **Claude 协议**两种 API 格式。

#### 基础配置

- `MODEL_ID` - 模型名称（默认：model id）
- `BASE_URL` - Provider Base URL（默认：http://xxxxx/v1）
- `API_KEY` - Provider API Key（默认：123456）
- `API_PROTOCOL` - API 协议类型（默认：openai-completions）
  - `openai-completions` - OpenAI 协议（适用于 OpenAI、Gemini 等模型）
  - `anthropic-messages` - Claude 协议（适用于 Claude 模型，支持 Prompt Caching 等特性）
- `CONTEXT_WINDOW` - 模型上下文窗口大小（默认：200000）
- `MAX_TOKENS` - 模型最大输出 tokens（默认：8192）

#### 协议对比

| 特性 | OpenAI 协议 | Claude 协议 |
|------|------------|------------|
| API 类型 | `openai-completions` | `anthropic-messages` |
| Base URL | 需要 `/v1` 后缀 | 不需要 `/v1` 后缀 |
| 支持模型 | OpenAI、Gemini 等 | 仅 Claude |
| 特殊特性 | - | Prompt Caching、Extended Thinking |

#### 配置示例

**使用 OpenAI 协议（Gemini 模型）**

```bash
MODEL_ID=gemini-3-flash-preview
BASE_URL=http://localhost:3000/v1
API_KEY=your-api-key
API_PROTOCOL=openai-completions
CONTEXT_WINDOW=1000000
MAX_TOKENS=8192
```

**使用 Claude 协议（Claude 模型）**

```bash
MODEL_ID=claude-sonnet-4-5
BASE_URL=http://localhost:3000
API_KEY=your-api-key
API_PROTOCOL=anthropic-messages
CONTEXT_WINDOW=200000
MAX_TOKENS=8192
```

> 💡 **提示**：使用 OpenAI 协议时，Base URL 需要包含 `/v1` 后缀；使用 Claude 协议时，Base URL 不需要 `/v1` 后缀。

### 通道配置
- `TELEGRAM_BOT_TOKEN` - Telegram 机器人令牌（可选，留空则不启用 Telegram）
- `FEISHU_APP_ID` - 飞书应用 ID（可选，留空则不启用飞书）
- `FEISHU_APP_SECRET` - 飞书应用密钥（可选，留空则不启用飞书）
- `DINGTALK_CLIENT_ID` - 钉钉应用 Client ID（可选，留空则不启用钉钉）
- `DINGTALK_CLIENT_SECRET` - 钉钉应用 Client Secret（可选，留空则不启用钉钉）
- `DINGTALK_ROBOT_CODE` - 钉钉机器人 Code（可选，默认与 Client ID 相同）
- `DINGTALK_CORP_ID` - 钉钉企业 ID（可选）
- `DINGTALK_AGENT_ID` - 钉钉应用 Agent ID（可选）
- `QQBOT_APP_ID` - QQ 机器人 AppID（可选，留空则不启用 QQ 机器人）
- `QQBOT_CLIENT_SECRET` - QQ 机器人 AppSecret（可选，留空则不启用 QQ 机器人）
- `WECOM_TOKEN` - 企业微信 Token（可选，留空则不启用企业微信）
- `WECOM_ENCODING_AES_KEY` - 企业微信 EncodingAESKey（可选，留空则不启用企业微信）

### Gateway 配置
- `OPENCLAW_GATEWAY_TOKEN` - Gateway 访问令牌（默认：7788414）
- `OPENCLAW_GATEWAY_BIND` - 绑定地址（默认：lan）
- `OPENCLAW_GATEWAY_PORT` - Gateway 端口（默认：18789）
- `OPENCLAW_BRIDGE_PORT` - Bridge 端口（默认：18790）

### 其他配置
- `WORKSPACE` - 工作空间目录（默认：/home/node/.openclaw/workspace）

## 端口说明

- `18789` - OpenClaw Gateway 端口
- `18790` - OpenClaw Bridge 端口

## 数据持久化

容器使用以下卷进行数据持久化：

- `/home/node/.openclaw` - OpenClaw 配置和数据目录
- `/home/node/.openclaw/workspace` - 工作空间目录

## 初始化脚本功能

[`init.sh`](openclaw/init.sh) 脚本在容器启动时执行以下操作：

1. 创建必要的目录结构
2. 根据环境变量动态生成配置文件（如果不存在）
3. 设置正确的文件权限
4. 启动 OpenClaw Gateway 服务（verbose 模式）

## 配置文件生成

容器首次启动时，如果 `/home/node/.openclaw/openclaw.json` 不存在，初始化脚本会根据环境变量自动生成配置文件，包括：

- **模型配置**：使用指定的模型和 Provider
- **通道配置**：
  - Telegram 机器人（如果提供了 TELEGRAM_BOT_TOKEN）
  - 飞书（Feishu）应用（如果提供了 FEISHU_APP_ID 和 FEISHU_APP_SECRET）
  - 钉钉（DingTalk）应用（如果提供了 DINGTALK_CLIENT_ID 和 DINGTALK_CLIENT_SECRET，可选配置 DINGTALK_ROBOT_CODE、DINGTALK_CORP_ID、DINGTALK_AGENT_ID）
  - QQ 机器人（如果提供了 QQBOT_APP_ID 和 QQBOT_CLIENT_SECRET）
  - 企业微信（WeCom）应用（如果提供了 WECOM_TOKEN 和 WECOM_ENCODING_AES_KEY）
- **Gateway 配置**：端口、绑定地址、认证令牌
- **插件配置**：自动启用相应的通道插件

## 查看日志

```bash
docker logs -f openclaw-gateway
```

## 停止容器

```bash
docker stop openclaw-gateway
```

或使用 Docker Compose：

```bash
docker-compose down
```

## 自定义配置

如件，可以：

1. 在宿主机创建配置文件 `~/.openclaw/openclaw.json`
2. 挂载该目录到容器：`-v ~/.openclaw:/home/node/.openclaw`
3. 容器启动时会检测到已存在的配置文件，跳过自动生成

## 注意事项

1. 确保宿主机的 18789 和 18790 端口未被占用
2. 配置文件中的敏感信息（如 API 密钥、令牌）应妥善保管
3. 首次运行时会自动创建必要的目录和配置文件
4. 容器以 `node` 用户身份运行，确保挂载的卷有正确的权限
5. 如果需要启用 Telegram，必须提供有效的 `TELEGRAM_BOT_TOKEN`
6. 飞书配置默认已启用，可通过环境变量修改 App ID 和 Secret
7. 如果需要启用钉钉，必须提供有效的 `DINGTALK_CLIENT_ID` 和 `DINGTALK_CLIENT_SECRET`，可选配置 `DINGTALK_ROBOT_CODE`、`DINGTALK_CORP_ID`、`DINGTALK_AGENT_ID`
8. 如果需要启用 QQ 机器人，必须提供有效的 `QQBOT_APP_ID` 和 `QQBOT_CLIENT_SECRET`
9. 如果需要启用企业微信，必须提供有效的 `WECOM_TOKEN` 和 `WECOM_ENCODING_AES_KEY`

## 飞书配置

### 1. 获取飞书机器人凭证

1. 在 [飞书开放平台](https://open.feishu.cn/) 创建自建应用
2. 添加应用能力-机器人
3. 在凭证页面获取 **App ID** 和 **App Secret**
4. 开启所需权限（见下方）⚠️ **重要**
5. 配置事件订阅（见下方）⚠️ **重要**

### 2. 必需权限

| 权限 | 范围 | 说明 |
|------|------|------|
| `contact:user.base:readonly` | 用户信息 | 获取用户基本信息（用于解析发送者姓名，避免群聊/私聊把不同人当成同一说话者） |
| `im:message` | 消息 | 发送和接收消息 |
| `im:message.p2p_msg:readonly` | 私聊 | 读取发给机器人的私聊消息 |
| `im:message.group_at_msg:readonly` | 群聊 | 接收群内 @机器人 的消息 |
| `im:message:send_as_bot` | 发送 | 以机器人身份发送消息 |
| `im:resource` | 媒体 | 上传和下载图片/文件 |

### 3. 可选权限

| 权限 | 范围 | 说明 |
|------|------|------|
| `im:message.group_msg` | 群聊 | 读取所有群消息（敏感） |
| `im:message:readonly` | 读取 | 获取历史消息 |
| `im:message:update` | 编辑 | 更新/编辑已发送消息 |
| `im:message:recall` | 撤回 | 撤回已发送消息 |
| `im:message.reactions:read` | 表情 | 查看消息表情回复 |

### 4. 事件订阅 ⚠️

**这是最容易遗漏的配置！** 如果机器人能发消息但收不到消息，请检查此项。

在飞书开放平台的应用后台，进入 **事件与回调** 页面：

1. **事件配置方式**：选择 **使用长连接接收事件**（推荐）
2. **添加事件订阅**，勾选以下事件：

| 事件 | 说明 |
|------|------|
| `im.message.receive_v1` | 接收消息（必需） |
| `im.message.message_read_v1` | 消息已读回执 |
| `im.chat.member.bot.added_v1` | 机器人进群 |
| `im.chat.member.bot.deleted_v1` | 机器人被移出群 |

3. 确保事件订阅的权限已申请并通过审核

### 5. 配置方式

**环境变量配置**

在 `.env` 文件中添加：
```bash
FEISHU_APP_ID=your-app-id
FEISHU_APP_SECRET=your-app-secret
```

> 💡 **参考项目**：[clawdbot-feishu](https://github.com/m1heng/clawdbot-feishu) - 飞书机器人完整实现示例

## 钉钉配置

### 1. 创建钉钉应用

1. 访问 [钉钉开发者后台](https://open-dev.dingtalk.com/)
2. 创建企业内部应用
3. 添加「机器人」能力
4. 配置消息接收模式为 **Stream 模式**
5. 发布应用

### 2. 获取凭证

从开发者后台获取：

- **Client ID**（AppKey）
- **Client Secret**（AppSecret）
- **Robot Code**（与 Client ID 相同）
- **Corp ID**（与 Client ID 相同）
- **Agent ID**（应用 ID）

### 3. 配置 OpenClaw

**环境变量配置**

在 `.env` 文件中添加：
```bash
DINGTALK_CLIENT_ID=your-dingtalk-client-id
DINGTALK_CLIENT_SECRET=your-dingtalk-client-secret
DINGTALK_ROBOT_CODE=your-dingtalk-robot-code
DINGTALK_CORP_ID=your-dingtalk-corp-id
DINGTALK_AGENT_ID=your-dingtalk-agent-id
```

**参数说明**：
- `DINGTALK_CLIENT_ID` - 必需，钉钉应用的 Client ID（AppKey）
- `DINGTALK_CLIENT_SECRET` - 必需，钉钉应用的 Client Secret（AppSecret）
- `DINGTALK_ROBOT_CODE` - 可选，机器人 Code，默认与 Client ID 相同
- `DINGTALK_CORP_ID` - 可选，企业 ID
- `DINGTALK_AGENT_ID` - 可选，应用 Agent ID

> 💡 **参考项目**：[openclaw-channel-dingtalk](https://github.com/soimy/openclaw-channel-dingtalk) - 钉钉渠道完整实现示例


## 企业微信配置

### 获取企业微信凭证

1. 访问 [企业微信管理后台](https://work.weixin.qq.com/)
2. 进入"应用管理" - 用API模式创建"智能机器人"应用
3. 在应用的"接收消息"配置中设置 Token 和 EncodingAESKey
4. 设置"接收消息"URL 为你的服务地址（例如：https://your-domain.com/webhooks/wxwork），需要当前服务可公网访问

### 配置方式

**环境变量配置**

在 `.env` 文件中添加：
```bash
WECOM_TOKEN=your-token
WECOM_ENCODING_AES_KEY=your-aes-key
```

> 💡 **参考项目**：[openclaw-plugin-wecom](https://github.com/sunnoy/openclaw-plugin-wecom) - 企业微信插件完整实现示例

## QQ 机器人配置

### 获取 QQ 机器人凭证

1. 访问 [QQ 开放平台](https://q.qq.com/)
2. 创建机器人应用
3. 获取 AppID 和 AppSecret（ClientSecret）
4. 获取主机在公网的ip，配置到ip白名单
5. 将 AppID 和 AppSecret 配置到环境变量中

### 配置方式

**环境变量配置**

在 `.env` 文件中添加：
```bash
QQBOT_APP_ID=你的AppID
QQBOT_CLIENT_SECRET=你的AppSecret
```

> 💡 **参考项目**：[qqbot](https://github.com/sliverp/qqbot) - QQ 机器人完整实现示例

## AIClient-2-API 配置指南

本项目已支持 OpenAI 和 Claude 两种协议，可直接对接 [AIClient-2-API](https://github.com/justlovemaki/AIClient-2-API) 服务。

### 前置准备

1. 启动 AIClient-2-API 服务
2. 在 Web UI (`http://localhost:3000`) 配置至少一个提供商
3. 记录配置文件中的 API Key

### 配置方式一：OpenAI 协议（推荐用于 Gemini）

在 `.env` 文件中配置：

```bash
MODEL_ID=gemini-3-flash-preview
BASE_URL=http://localhost:3000/v1
API_KEY=your-api-key
API_PROTOCOL=openai-completions
CONTEXT_WINDOW=1000000
MAX_TOKENS=8192
```

### 配置方式二：Claude 协议（推荐用于 Claude）

在 `.env` 文件中配置：

```bash
MODEL_ID=claude-sonnet-4-5
BASE_URL=http://localhost:3000
API_KEY=your-api-key
API_PROTOCOL=anthropic-messages
CONTEXT_WINDOW=200000
MAX_TOKENS=8192
```

### 指定特定提供商（可选）

如需指定特定提供商，可修改 Base URL：

```bash
# Kiro 提供的 Claude (OpenAI 协议)
BASE_URL=http://localhost:3000/claude-kiro-oauth/v1

# Kiro 提供的 Claude (Claude 协议)
BASE_URL=http://localhost:3000/claude-kiro-oauth

# Gemini CLI (OpenAI 协议)
BASE_URL=http://localhost:3000/gemini-cli-oauth/v1

# Antigravity (OpenAI 协议)
BASE_URL=http://localhost:3000/gemini-antigravity/v1
```

### 常见问题

**Q: 修改了环境变量但配置没有生效？**
- 容器启动时只有在配置文件不存在时才会生成新配置
- 如需重新生成配置，请删除现有配置文件：
  ```bash
  # 删除配置文件
  rm ~/.openclaw/openclaw.json
  # 重启容器
  docker-compose restart
  ```
- 或者直接删除整个数据目录重新开始：
  ```bash
  rm -rf ~/.openclaw
  docker-compose up -d
  ```

**Q: 连接失败？**
- 确认 AIClient-2-API 服务运行中
- 检查 Base URL 是否正确（OpenAI 协议需要 `/v1` 后缀）
- 尝试使用 `127.0.0.1` 替代 `localhost`

**Q: 401 错误？**
- 检查 API Key 是否正确配置
- 确认环境变量 `API_KEY` 已设置

**Q: 模型不可用？**
- 在 AIClient-2-API Web UI 确认已配置对应提供商
- 重启容器：`docker-compose restart`

---

## 安装的包

镜像中已全局安装以下 npm 包：

- `openclaw@latest` - OpenClaw 主程序
- `opencode-ai@latest` - OpenCode AI
- `playwright` - Playwright 浏览器自动化工具
- `@m1heng-clawd/feishu` - 飞书插件（从 GitHub 安装）
- `clawdbot-channel-dingtalk` - 钉钉插件（从 GitHub 安装）
- `qqbot` - QQ 机器人插件（先克隆到 `/tmp/qqbot`，然后从本地目录安装）
- `openclaw-plugin-wecom` - 企业微信插件（从 GitHub 安装）

## 启动命令

容器使用以下命令启动 OpenClaw：

```bash
openclaw gateway --verbose
```

这将以详细日志模式启动 Gateway 服务。


