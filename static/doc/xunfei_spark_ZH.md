# 科大讯飞星火大模型配置指南

本文档介绍如何在 MuseBot 中配置和使用科大讯飞星火大模型。

## 支持的服务接口

科大讯飞星火大模型提供两种接口类型：

### 1. HTTP 服务接口

- **服务名称**: Spark Pro
- **协议**: HTTP
- **接口地址**: `https://spark-api-open.xf-yun.com/v1/chat/completions`
- **认证方式**: HTTP Basic Auth

### 2. WebSocket 服务接口

- **服务名称**: Spark Pro
- **协议**: WebSocket
- **接口地址**: `wss://spark-api.xf-yun.com/v3.1/chat`
- **认证方式**: APPID + APISecret + APIKey

## 配置方式

### 方式一：环境变量配置

在启动 MuseBot 之前设置以下环境变量：

```bash
# 设置 LLM 类型为 xunfei
export TYPE="xunfei"

# WebSocket 服务认证信息（用于 WebSocket 方式连接）
export XUNFEI_SPARK_APP_ID="1be7c069"
export XUNFEI_SPARK_API_SECRET="NWVhM2I4MjEyODAzZmE2NDc3YjlkMTAx"
export XUNFEI_SPARK_API_KEY="47b56bc111a294c4908ba993cda86dff"
export XUNFEI_SPARK_WS_URL="wss://spark-api.xf-yun.com/v3.1/chat"

# HTTP 服务认证信息（用于 HTTP 方式连接）
export XUNFEI_SPARK_HTTP_AUTH="hECUEzZujvRaHWAhlJqA:WswiqFkaNMFooUVtsZUm"
export XUNFEI_SPARK_HTTP_URL="https://spark-api-open.xf-yun.com/v1/chat/completions"
```

然后启动 MuseBot：

```bash
./MuseBot
```

### 方式二：命令行参数配置

直接在启动命令中指定参数：

```bash
./MuseBot \
  -type=xunfei \
  -xunfei_spark_app_id="1be7c069" \
  -xunfei_spark_api_secret="NWVhM2I4MjEyODAzZmE2NDc3YjlkMTAx" \
  -xunfei_spark_api_key="47b56bc111a294c4908ba993cda86dff" \
  -xunfei_spark_http_auth="hECUEzZujvRaHWAhlJqA:WswiqFkaNMFooUVtsZUm" \
  -xunfei_spark_http_url="https://spark-api-open.xf-yun.com/v1/chat/completions" \
  -xunfei_spark_ws_url="wss://spark-api.xf-yun.com/v3.1/chat"
```

### 方式三：通过管理 API 配置

MuseBot 启动后，可以通过 HTTP API 动态更新配置：

#### 更新 APPID

```bash
curl -X POST http://localhost:36060/conf/update \
  -H "Content-Type: application/json" \
  -d '{
    "type": "base",
    "key": "xunfei_spark_app_id",
    "value": "1be7c069"
  }'
```

#### 更新 API Secret

```bash
curl -X POST http://localhost:36060/conf/update \
  -H "Content-Type: application/json" \
  -d '{
    "type": "base",
    "key": "xunfei_spark_api_secret",
    "value": "NWVhM2I4MjEyODAzZmE2NDc3YjlkMTAx"
  }'
```

#### 更新 API Key

```bash
curl -X POST http://localhost:36060/conf/update \
  -H "Content-Type: application/json" \
  -d '{
    "type": "base",
    "key": "xunfei_spark_api_key",
    "value": "47b56bc111a294c4908ba993cda86dff"
  }'
```

#### 更新 HTTP 认证信息

```bash
curl -X POST http://localhost:36060/conf/update \
  -H "Content-Type: application/json" \
  -d '{
    "type": "base",
    "key": "xunfei_spark_http_auth",
    "value": "hECUEzZujvRaHWAhlJqA:WswiqFkaNMFooUVtsZUm"
  }'
```

#### 切换 LLM 类型为讯飞星火

```bash
curl -X POST http://localhost:36060/conf/update \
  -H "Content-Type: application/json" \
  -d '{
    "type": "base",
    "key": "type",
    "value": "xunfei"
  }'
```

### 方式四：使用 .env 文件配置

创建 `.env` 文件并添加以下内容：

```bash
# 设置 LLM 类型
TYPE=xunfei

# WebSocket 服务认证信息
XUNFEI_SPARK_APP_ID=1be7c069
XUNFEI_SPARK_API_SECRET=NWVhM2I4MjEyODAzZmE2NDc3YjlkMTAx
XUNFEI_SPARK_API_KEY=47b56bc111a294c4908ba993cda86dff
XUNFEI_SPARK_WS_URL=wss://spark-api.xf-yun.com/v3.1/chat

# HTTP 服务认证信息
XUNFEI_SPARK_HTTP_AUTH=hECUEzZujvRaHWAhlJqA:WswiqFkaNMFooUVtsZUm
XUNFEI_SPARK_HTTP_URL=https://spark-api-open.xf-yun.com/v1/chat/completions
```

## 配置字段说明

| 配置字段 | 说明 | 默认值 | 是否必填 |
|---------|------|-------|---------|
| `xunfei_spark_app_id` | WebSocket 服务的 APPID | - | WebSocket 必填 |
| `xunfei_spark_api_secret` | WebSocket 服务的 API Secret | - | WebSocket 必填 |
| `xunfei_spark_api_key` | WebSocket 服务的 API Key | - | WebSocket 必填 |
| `xunfei_spark_http_auth` | HTTP 服务的认证信息（格式：`用户名:密码`） | - | HTTP 必填 |
| `xunfei_spark_http_url` | HTTP 服务接口地址 | `https://spark-api-open.xf-yun.com/v1/chat/completions` | 可选 |
| `xunfei_spark_ws_url` | WebSocket 服务接口地址 | `wss://spark-api.xf-yun.com/v3.1/chat` | 可选 |

## 您的认证信息

根据您提供的信息，以下是您的科大讯飞星火 API 认证凭证：

### HTTP 服务接口
- **认证信息**: `hECUEzZujvRaHWAhlJqA:WswiqFkaNMFooUVtsZUm`
- **接口地址**: `https://spark-api-open.xf-yun.com/v1/chat/completions`

### WebSocket 服务接口
- **APPID**: `1be7c069`
- **APISecret**: `NWVhM2I4MjEyODAzZmE2NDc3YjlkMTAx`
- **APIKey**: `47b56bc111a294c4908ba993cda86dff`
- **接口地址**: `wss://spark-api.xf-yun.com/v3.1/chat`

## 验证配置

启动 MuseBot 后，您可以通过以下命令查看当前配置：

```bash
curl http://localhost:36060/conf/get | jq '.data.base | {
  xunfei_spark_app_id,
  xunfei_spark_api_secret,
  xunfei_spark_api_key,
  xunfei_spark_http_auth,
  xunfei_spark_http_url,
  xunfei_spark_ws_url
}'
```

或查看日志输出，启动时会打印所有配置信息。

## 注意事项

1. **认证方式选择**：
   - HTTP 接口使用 Basic Auth 认证，需要配置 `xunfei_spark_http_auth`
   - WebSocket 接口需要三个独立的凭证：`APPID`、`APISecret` 和 `APIKey`

2. **接口地址**：
   - 接口地址已设置默认值，通常情况下不需要修改
   - 如果讯飞更新了接口地址，可以通过配置项进行覆盖

3. **安全性**：
   - 请妥善保管您的 API 凭证，不要泄露给他人
   - 建议使用环境变量而不是在代码中硬编码凭证

4. **日志**：
   - MuseBot 启动时会记录所有配置信息（包括 API 凭证）
   - 生产环境中注意日志文件的访问权限

## 快速开始

最简单的启动方式是使用环境变量：

```bash
# 创建环境变量配置
cat > .env << 'EOF'
TYPE=xunfei
XUNFEI_SPARK_APP_ID=1be7c069
XUNFEI_SPARK_API_SECRET=NWVhM2I4MjEyODAzZmE2NDc3YjlkMTAx
XUNFEI_SPARK_API_KEY=47b56bc111a294c4908ba993cda86dff
XUNFEI_SPARK_HTTP_AUTH=hECUEzZujvRaHWAhlJqA:WswiqFkaNMFooUVtsZUm
EOF

# 加载环境变量并启动
source .env
./MuseBot
```

启动成功后，MuseBot 将使用科大讯飞星火大模型处理对话请求。

## 故障排查

如果遇到问题，请检查：

1. **配置是否正确加载**：查看启动日志中的配置输出
2. **API 凭证是否有效**：确认 APPID、APISecret、APIKey 和 HTTP Auth 信息正确
3. **网络连接**：确保服务器可以访问讯飞 API 接口
4. **LLM 类型设置**：确认 `TYPE` 环境变量或 `-type` 参数设置为 `xunfei`

如有问题，请查看 MuseBot 日志获取详细错误信息。
