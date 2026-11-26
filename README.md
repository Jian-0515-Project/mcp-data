# date-tool-mcp

一个基于 [MCP (Model Context Protocol)](https://modelcontextprotocol.io) Python SDK 的简单 MCP 服务，使用 `FastMCP` 实现，向支持 MCP 的客户端（如 Trae、Claude Desktop 等）提供日期查询工具。

## 功能

| 工具 | 说明 | 返回示例 |
| --- | --- | --- |
| `get_today` | 返回当前的年月日 | `2026-11-26` |

## 环境要求

- Python 3.10+
- 依赖：`mcp>=1.28.1`

## 安装

```bash
pip install -r requirements.txt
```

## 运行

```bash
python server.py
```

默认以 stdio 方式启动服务，等待 MCP 客户端连接。

## 在 MCP 客户端中配置

以 JSON 配置为例（将路径替换为本机实际路径）：

```json
{
  "mcpServers": {
    "date-tool-mcp": {
      "command": "python",
      "args": ["d:\\PycharmProjects\\AgentProject\\mcp_upload\\server.py"]
    }
  }
}
```

配置后，客户端即可调用 `get_today` 工具获取当天日期。

## 项目结构

```
mcp_upload/
├── server.py         # MCP 服务入口与工具定义
├── requirements.txt  # 依赖清单
└── README.md
```

## 扩展新工具

在 [server.py](server.py) 中使用 `@mcp.tool()` 装饰器定义函数即可，函数签名和文档字符串会作为工具的参数与描述暴露给客户端：

```python
@mcp.tool()
def get_time() -> str:
    """返回当前的时分秒，格式 HH:MM:SS。"""
    return datetime.now().strftime("%H:%M:%S")
```
