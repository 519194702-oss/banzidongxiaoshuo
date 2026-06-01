# API 配置指南

## 如何配置 AI API 密钥

本编辑器支持多个 AI 模型来生成故事内容。按照以下步骤配置你的 API：

## 1. OpenAI GPT-4

### 获取 API 密钥

1. 访问 [OpenAI 官网](https://platform.openai.com/)
2. 注册或登录账户
3. 进入 [API Keys](https://platform.openai.com/api-keys) 页面
4. 点击 "Create new secret key"
5. 复制生成的密钥

### 在编辑器中配置

```javascript
// 在浏览器开发者工具中执行：
localStorage.setItem("openai_apiKey", "你的API密钥");
```

或者在编辑器中设置菜单（将在后续版本支持）

### 费用

- 按照 token 计费
- 查看 [定价页面](https://openai.com/pricing)

---

## 2. Claude 3 (Anthropic)

### 获取 API 密钥

1. 访问 [Anthropic 官网](https://www.anthropic.com/)
2. 申请 API 访问权限
3. 获得 API 密钥后保存

### 在编辑器中配置

```javascript
localStorage.setItem("anthropic_apiKey", "你的API密钥");
```

### 费用

- 按照 token 计费
- 查看 [定价详情](https://www.anthropic.com/pricing)

---

## 3. 本地 LLM

### 使用本地模型

如果你想使用本地的大语言模型（如 Ollama、LLaMA 等），可以修改代码调用本地 API：

```javascript
async function callAI(prompt, model) {
    if (model === "local") {
        const response = await fetch("http://localhost:11434/api/generate", {
            method: "POST",
            headers: { "Content-Type": "application/json" },
            body: JSON.stringify({
                model: "llama2",
                prompt: prompt,
                stream: false
            })
        });
        const data = await response.json();
        return data.response;
    }
    // ... 其他模型的处理
}
```

### 推荐本地模型

- **Ollama** - 轻量级本地 LLM 运行工具
- **LLaMA 2** - Meta 开源模型
- **Mistral** - 高效开源模型

---

## 环境变量配置（可选）

创建 `.env` 文件来管理 API 密钥：

```
OPENAI_API_KEY=sk-xxx
ANTHROPIC_API_KEY=xxx
LOCAL_LLM_URL=http://localhost:11434
```

然后在初始化时加载：

```javascript
async function loadEnvConfig() {
    const response = await fetch('.env');
    const envData = await response.text();
    // 解析并设置到 localStorage
}
```

---

## 安全建议

⚠️ **重要**：永远不要在代码中硬编码 API 密钥！

### 最佳实践

1. **使用环境变量** - 将密钥存储在环境变量中
2. **后端代理** - 通过后端服务代理 API 请求
3. **加密存储** - 如果本地存储密钥，使用加密算法
4. **定期轮换** - 定期更新 API 密钥

### 浏览器存储安全

```javascript
// 使用受限的密钥作为演示用
const demoKeys = {
    openai: "demo-key-xxxx",  // 演示密钥
    anthropic: "demo-key-yyyy"
};

// 或使用 session storage（关闭浏览器后删除）
sessionStorage.setItem("apiKey", "xxx");
```

---

## 测试 API 连接

### 检查 OpenAI 连接

```javascript
async function testOpenAIConnection(apiKey) {
    try {
        const response = await fetch("https://api.openai.com/v1/models", {
            headers: { "Authorization": `Bearer ${apiKey}` }
        });
        const data = await response.json();
        console.log("✅ 连接成功！", data);
    } catch (error) {
        console.error("❌ 连接失败:", error);
    }
}

testOpenAIConnection(localStorage.getItem("openai_apiKey"));
```

### 检查本地 LLM 连接

```javascript
async function testLocalLLM() {
    try {
        const response = await fetch("http://localhost:11434/api/tags");
        const data = await response.json();
        console.log("✅ 本地 LLM 运行中！", data);
    } catch (error) {
        console.error("❌ 无法连接本地 LLM");
    }
}

testLocalLLM();
```

---

## 故障排除

### 问题 1: API 密钥无效

**症状**: 生成内容时出现 401 错误

**解决方案**:
1. 检查密钥是否正确复制
2. 确认密钥未过期
3. 检查账户余额是否充足
4. 重新生成新的密钥

### 问题 2: 请求超时

**症状**: 等待很长时间后仍无响应

**解决方案**:
1. 检查网络连接
2. 减少生成的文本长度
3. 检查 API 服务状态
4. 尝试使用不同的模型

### 问题 3: 配额限制

**症状**: "Rate limit exceeded" 错误

**解决方案**:
1. 等待一段时间后重试
2. 使用付费计划提升限额
3. 优化请求频率

---

## 速率限制

各 API 服务的速率限制：

| 服务 | 限制 | 说明 |
|------|------|------|
| OpenAI | 每分钟 3-90 请求 | 取决于计划 |
| Claude | 每分钟 50 请求 | 可根据使用量调整 |
| 本地 LLM | 无限制 | 受本机性能限制 |

---

## 成本估算

### OpenAI GPT-3.5-Turbo

- 输入: $0.0005 / 1K tokens
- 输出: $0.0015 / 1K tokens

**示例**: 生成 1000 个 token 的内容
- 输入 (500 tokens): $0.00025
- 输出 (1000 tokens): $0.0015
- **总计**: $0.00175

### Claude 3

- 输入: $0.003 / 1K tokens
- 输出: $0.015 / 1K tokens

---

## 更多资源

- [OpenAI 文档](https://platform.openai.com/docs)
- [Anthropic 文档](https://docs.anthropic.com)
- [Ollama 指南](https://ollama.ai)
- [LLaMA 项目](https://github.com/facebookresearch/llama)

---

**最后更新**: 2024年6月

**反馈**: 如有问题，请提交 Issue
