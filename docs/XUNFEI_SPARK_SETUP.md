# XunFei Spark (科大讯飞星火) API Configuration

This document describes how to configure and use the XunFei Spark API with MuseBot.

## Configuration Methods

### 1. Environment Variables

You can set the following environment variables:

```bash
# WebSocket Service Authentication (for websocket-based chat)
export XUNFEI_SPARK_APP_ID="1be7c069"
export XUNFEI_SPARK_API_SECRET="NWVhM2I4MjEyODAzZmE2NDc3YjlkMTAx"
export XUNFEI_SPARK_API_KEY="47b56bc111a294c4908ba993cda86dff"
export XUNFEI_SPARK_WS_URL="wss://spark-api.xf-yun.com/v3.1/chat"

# HTTP Service Authentication (for HTTP-based chat)
export XUNFEI_SPARK_HTTP_AUTH="hECUEzZujvRaHWAhlJqA:WswiqFkaNMFooUVtsZUm"
export XUNFEI_SPARK_HTTP_URL="https://spark-api-open.xf-yun.com/v1/chat/completions"
```

### 2. Command Line Flags

You can pass credentials as command-line arguments when starting MuseBot:

```bash
./MuseBot \
  -xunfei_spark_app_id="1be7c069" \
  -xunfei_spark_api_secret="NWVhM2I4MjEyODAzZmE2NDc3YjlkMTAx" \
  -xunfei_spark_api_key="47b56bc111a294c4908ba993cda86dff" \
  -xunfei_spark_http_auth="hECUEzZujvRaHWAhlJqA:WswiqFkaNMFooUVtsZUm" \
  -xunfei_spark_http_url="https://spark-api-open.xf-yun.com/v1/chat/completions" \
  -xunfei_spark_ws_url="wss://spark-api.xf-yun.com/v3.1/chat"
```

### 3. Using the Admin API

You can update the configuration via HTTP API:

```bash
# Update XunFei Spark App ID
curl -X POST http://localhost:36060/conf/update \
  -H "Content-Type: application/json" \
  -d '{
    "type": "base",
    "key": "xunfei_spark_app_id",
    "value": "1be7c069"
  }'

# Update XunFei Spark API Secret
curl -X POST http://localhost:36060/conf/update \
  -H "Content-Type: application/json" \
  -d '{
    "type": "base",
    "key": "xunfei_spark_api_secret",
    "value": "NWVhM2I4MjEyODAzZmE2NDc3YjlkMTAx"
  }'

# Update XunFei Spark API Key
curl -X POST http://localhost:36060/conf/update \
  -H "Content-Type: application/json" \
  -d '{
    "type": "base",
    "key": "xunfei_spark_api_key",
    "value": "47b56bc111a294c4908ba993cda86dff"
  }'

# Update XunFei Spark HTTP Auth
curl -X POST http://localhost:36060/conf/update \
  -H "Content-Type: application/json" \
  -d '{
    "type": "base",
    "key": "xunfei_spark_http_auth",
    "value": "hECUEzZujvRaHWAhlJqA:WswiqFkaNMFooUVtsZUm"
  }'

# Update XunFei Spark HTTP URL (optional)
curl -X POST http://localhost:36060/conf/update \
  -H "Content-Type: application/json" \
  -d '{
    "type": "base",
    "key": "xunfei_spark_http_url",
    "value": "https://spark-api-open.xf-yun.com/v1/chat/completions"
  }'

# Update XunFei Spark WebSocket URL (optional)
curl -X POST http://localhost:36060/conf/update \
  -H "Content-Type: application/json" \
  -d '{
    "type": "base",
    "key": "xunfei_spark_ws_url",
    "value": "wss://spark-api.xf-yun.com/v3.1/chat"
  }'
```

## Configuration Fields

| Field | Description | Default Value |
|-------|-------------|---------------|
| `xunfei_spark_app_id` | WebSocket service App ID | - |
| `xunfei_spark_api_secret` | WebSocket service API Secret | - |
| `xunfei_spark_api_key` | WebSocket service API Key | - |
| `xunfei_spark_http_auth` | HTTP service authentication (format: `username:password`) | - |
| `xunfei_spark_http_url` | HTTP service endpoint | `https://spark-api-open.xf-yun.com/v1/chat/completions` |
| `xunfei_spark_ws_url` | WebSocket service endpoint | `wss://spark-api.xf-yun.com/v3.1/chat` |

## Service Information

### HTTP Service Interface
- **Service**: Spark Pro
- **Protocol**: HTTP
- **Endpoint**: `https://spark-api-open.xf-yun.com/v1/chat/completions`
- **Authentication**: Basic Auth (`hECUEzZujvRaHWAhlJqA:WswiqFkaNMFooUVtsZUm`)

### WebSocket Service Interface
- **Service**: Spark Pro
- **Protocol**: WebSocket
- **Endpoint**: `wss://spark-api.xf-yun.com/v3.1/chat`
- **Authentication**:
  - APPID: `1be7c069`
  - APISecret: `NWVhM2I4MjEyODAzZmE2NDc3YjlkMTAx`
  - APIKey: `47b56bc111a294c4908ba993cda86dff`

## Using XunFei Spark as LLM Provider

To use XunFei Spark as your LLM provider, set the `type` configuration to `xunfei`:

```bash
export TYPE="xunfei"
```

Or via command line:

```bash
./MuseBot -type=xunfei
```

Or via API:

```bash
curl -X POST http://localhost:36060/conf/update \
  -H "Content-Type: application/json" \
  -d '{
    "type": "base",
    "key": "type",
    "value": "xunfei"
  }'
```

## Viewing Current Configuration

You can view the current configuration via the API:

```bash
curl http://localhost:36060/conf/get
```

This will return a JSON object containing all configuration values, including the XunFei Spark settings.

## Notes

- The HTTP authentication uses Basic Auth format with the credentials separated by a colon
- The WebSocket interface requires three separate credentials: APPID, APISecret, and APIKey
- Default URLs are pre-configured but can be overridden if needed
- All credential values are logged on startup (check your logs to verify configuration)
