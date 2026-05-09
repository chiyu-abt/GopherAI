# 企业知识库智能问答系统

基于 Go + EINO + RAG + MCP 构建的企业级智能知识库问答系统，
支持私有文档检索、上下文增强生成、多工具调用等能力，
用于解决企业内部文档查询效率低、大模型幻觉严重等问题。

---

# 项目介绍

本项目面向企业内部知识管理场景，
采用 Go 构建高并发 AI 后端服务，
结合 RAG（检索增强生成）与 MCP（模型上下文协议）机制，
实现私有知识库的精准问答。

系统支持：

- 企业文档上传
- 文档向量化
- 语义检索
- 上下文增强问答
- 多轮会话
- 工具调用
- 权限隔离

---

# 技术栈

## 后端

- Golang
- Gin
- GORM
- JWT

## AI 能力

- EINO Framework
- RAG
- MCP Protocol
- Embedding Model
- LLM

## 中间件

- Redis
- RabbitMQ
- MySQL

## 部署

- Docker
- Linux

---

# 核心架构

用户问题
   ↓
Query 重写
   ↓
向量检索
   ↓
RAG 上下文增强
   ↓
MCP 工具调用
   ↓
LLM 生成回答
   ↓
结果返回

---

# 核心功能

## 用户系统

- JWT 登录认证
- 用户权限隔离
- 多用户知识库管理

## 知识库系统

- PDF / Markdown 文档上传
- 文档切片
- 向量化存储
- 语义召回

## 智能问答系统

- 多轮上下文会话
- RAG 检索增强生成
- Query Rewrite 查询改写
- Prompt 模板管理

## MCP 工具系统

- 外部工具注册
- Function Calling
- 动态工具扩展

---

# RAG 工作流程

## 文档预处理

上传文档后：

- 文档解析
- 文本切片
- Embedding 向量化
- 写入向量数据库

## 查询阶段

用户问题进入系统后：

1. Query Rewrite 优化用户问题
2. Embedding 编码
3. TopK 相似度召回
4. 拼接上下文
5. 输入大模型生成答案

---

# MCP 工具调用机制

系统支持 MCP 协议进行工具扩展。

当模型识别用户需要：

- 查询数据库
- 调用外部 API
- 获取实时信息

时，
系统会自动选择对应 Tool，
实现 Function Calling。

---

# 项目亮点

## 1. Go 高并发 AI 后端

基于 Goroutine + Channel 构建高并发 AI 服务，
支持多请求并发处理。

## 2. RAG 降低模型幻觉

通过向量召回 + 上下文增强，
减少大模型脱离知识库胡乱回答的问题。

## 3. Query Rewrite 查询改写

针对企业内部模糊问题，
自动进行 Query Rewrite，
提升召回准确率。

## 4. RabbitMQ 异步解耦

文档解析与向量化采用 MQ 异步处理，
避免阻塞主流程。

## 5. Redis 多级缓存

缓存热点问答与用户会话，
降低数据库与模型调用压力。

---

# 系统架构图

客户端
   ↓
Gin API Gateway
   ↓
AI Service
   ├── RAG 检索模块
   ├── MCP Tool 模块
   ├── Prompt 模块
   └── Session 模块
   ↓
Redis / MySQL / RabbitMQ

---

# 项目结构

```text
.
├── cmd
├── config
├── internal
│   ├── handler
│   ├── service
│   ├── repository
│   ├── rag
│   ├── mcp
│   ├── llm
│   └── middleware
├── pkg
└── scripts
```

---

# 快速启动

## 启动 MySQL

```bash
docker run -d -p 3306:3306 mysql
```

## 启动 Redis

```bash
docker run -d -p 6379:6379 redis
```

## 启动 RabbitMQ

```bash
docker run -d -p 5672:5672 rabbitmq
```

## 启动项目

```bash
go run main.go
```

---

# API 示例

## 用户提问

```http
POST /api/chat
```

## 请求参数

```json
{
  "question": "公司的报销流程是什么？"
}
```

## 返回结果

```json
{
  "answer": "根据企业制度..."
}
```

---

# 性能优化

- Redis 热点缓存
- RabbitMQ 异步处理
- Goroutine 并发处理
- 连接池优化
- Prompt 模板复用

---

# 后续优化方向

- 引入向量数据库
- 多 Agent 协同
- 知识图谱增强
- 多模态文档解析
- 流式输出
