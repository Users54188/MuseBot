# XunFei Spark (iFlytek Spark) Configuration Guide

This document describes how to configure and use the XunFei Spark (iFlytek Spark) LLM with MuseBot.

## Supported Service Interfaces

XunFei Spark provides two types of service interfaces:

### 1. HTTP Service Interface

- **Service Name**: Spark Pro
- **Protocol**: HTTP
- **Endpoint**: `https://spark-api-open.xf-yun.com/v1/chat/completions`
- **Authentication**: HTTP Basic Auth

### 2. WebSocket Service Interface

- **Service Name**: Spark Pro
- **Protocol**: WebSocket
- **Endpoint**: `wss://spark-api.xf-yun.com/v3.1/chat`
- **Authentication**: APPID + APISecret + APIKey

## Configuration Methods

### Method 1: Environment Variables

Set the following environment variables before starting MuseBot:

```bash
# Set LLM type to xunfei
export TYPE="xunfei"

# WebSocket Service Authentication (for WebSocket-based connections)
export XUNFEI_SPARK_APP_ID="1be7c069"
export XUNFEI_SPARK_API_SECRET="NWVhM2I4MjEyODAzZmE2NDc3YjlkMTAx"
export XUNFEI_SPARK_API_KEY="47b56bc111a294c4908ba993cda86dff"
export XUNFEI_SPARK_WS_URL="wss://spark-api.xf-yun.com/v3.1/chat"

# HTTP Service Authentication (for HTTP-based connections)
export XUNFEI_SPARK_HTTP_AUTH="hECUEzZujvRaHWAhlJqA:WswiqFkaNMFooUVtsZUm"
export XUNFEI_SPARK_HTTP_URL="https://spark-api-open.xf-yun.com/v1/chat/completions"
```

Then start MuseBot:

```bash
./MuseBot
```

### Method 2: Command Line Parameters

Specify parameters directly in the startup command:

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

### Method 3: Admin API Configuration

After MuseBot is running, you can dynamically update the configuration via HTTP API:

#### Update APPID

```bash
curl -X POST http://localhost:36060/conf/update \
  -H "Content-Type: application/json" \
  -d '{
    "type": "base",
    "key": "xunfei_spark_app_id",
    "value": "1be7c069"
  }'
```

#### Update API Secret

```bash
curl -X POST http://localhost:36060/conf/update \
  -H "Content-Type: application/json" \
  -d '{
    "type": "base",
    "key": "xunfei_spark_api_secret",
    "value": "NWVhM2I4MjEyODAzZmE2NDc3YjlkMTAx"
  }'
```

#### Update API Key

```bash
curl -X POST http://localhost:36060/conf/update \
  -H "Content-Type: application/json" \
  -d '{
    "type": "base",
    "key": "xunfei_spark_api_key",
    "value": "47b56bc111a294c4908ba993cda86dff"
  }'
```

#### Update HTTP Auth

```bash
curl -X POST http://localhost:36060/conf/update \
  -H "Content-Type: application/json" \
  -d '{
    "type": "base",
    "key": "xunfei_spark_http_auth",
    "value": "hECUEzZujvRaHWAhlJqA:WswiqFkaNMFooUVtsZUm"
  }'
```

#### Switch LLM Type to XunFei Spark

```bash
curl -X POST http://localhost:36060/conf/update \
  -H "Content-Type: application/json" \
  -d '{
    "type": "base",
    "key": "type",
    "value": "xunfei"
  }'
```

### Method 4: Using .env File

Create a `.env` file with the following content:

```bash
# Set LLM type
TYPE=xunfei

# WebSocket Service Authentication
XUNFEI_SPARK_APP_ID=1be7c069
XUNFEI_SPARK_API_SECRET=NWVhM2I4MjEyODAzZmE2NDc3YjlkMTAx
XUNFEI_SPARK_API_KEY=47b56bc111a294c4908ba993cda86dff
XUNFEI_SPARK_WS_URL=wss://spark-api.xf-yun.com/v3.1/chat

# HTTP Service Authentication
XUNFEI_SPARK_HTTP_AUTH=hECUEzZujvRaHWAhlJqA:WswiqFkaNMFooUVtsZUm
XUNFEI_SPARK_HTTP_URL=https://spark-api-open.xf-yun.com/v1/chat/completions
```

## Configuration Fields

| Field | Description | Default Value | Required |
|-------|-------------|---------------|----------|
| `xunfei_spark_app_id` | WebSocket service APPID | - | WebSocket only |
| `xunfei_spark_api_secret` | WebSocket service API Secret | - | WebSocket only |
| `xunfei_spark_api_key` | WebSocket service API Key | - | WebSocket only |
| `xunfei_spark_http_auth` | HTTP service authentication (`username:password`) | - | HTTP only |
| `xunfei_spark_http_url` | HTTP service endpoint URL | `https://spark-api-open.xf-yun.com/v1/chat/completions` | Optional |
| `xunfei_spark_ws_url` | WebSocket service endpoint URL | `wss://spark-api.xf-yun.com/v3.1/chat` | Optional |

## Your Authentication Credentials

Based on the information provided, here are your XunFei Spark API credentials:

### HTTP Service Interface
- **Authentication**: `hECUEzZujvRaHWAhlJqA:WswiqFkaNMFooUVtsZUm`
- **Endpoint**: `https://spark-api-open.xf-yun.com/v1/chat/completions`

### WebSocket Service Interface
- **APPID**: `1be7c069`
- **APISecret**: `NWVhM2I4MjEyODAzZmE2NDc3YjlkMTAx`
- **APIKey**: `47b56bc111a294c4908ba993cda86dff`
- **Endpoint**: `wss://spark-api.xf-yun.com/v3.1/chat`

## Verify Configuration

After starting MuseBot, you can view the current configuration:

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

Or check the logs - all configuration values are printed at startup.

## Important Notes

1. **Authentication Method Selection**:
   - HTTP interface uses Basic Auth, configure `xunfei_spark_http_auth`
   - WebSocket interface requires three separate credentials: `APPID`, `APISecret`, and `APIKey`

2. **Endpoint URLs**:
   - Default endpoint URLs are pre-configured
   - Override them only if XunFei updates their API endpoints

3. **Security**:
   - Keep your API credentials secure and do not share them
   - Use environment variables instead of hardcoding credentials

4. **Logging**:
   - MuseBot logs all configuration values at startup (including credentials)
   - Be careful with log file permissions in production

## Quick Start

The simplest way to start is using environment variables:

```bash
# Create environment configuration
cat > .env << 'EOF'
TYPE=xunfei
XUNFEI_SPARK_APP_ID=1be7c069
XUNFEI_SPARK_API_SECRET=NWVhM2I4MjEyODAzZmE2NDc3YjlkMTAx
XUNFEI_SPARK_API_KEY=47b56bc111a294c4908ba993cda86dff
XUNFEI_SPARK_HTTP_AUTH=hECUEzZujvRaHWAhlJqA:WswiqFkaNMFooUVtsZUm
EOF

# Load environment variables and start
source .env
./MuseBot
```

After successful startup, MuseBot will use XunFei Spark LLM to process conversation requests.

## Troubleshooting

If you encounter issues, please check:

1. **Configuration Loaded Correctly**: Check startup logs for configuration output
2. **Valid API Credentials**: Verify APPID, APISecret, APIKey, and HTTP Auth are correct
3. **Network Connectivity**: Ensure the server can reach XunFei API endpoints
4. **LLM Type Setting**: Confirm `TYPE` environment variable or `-type` parameter is set to `xunfei`

For issues, check MuseBot logs for detailed error messages.
