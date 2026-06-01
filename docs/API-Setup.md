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
}
```

### 推荐本地模型

- **Ollama** - 轻量级本地 LLM 运行工具
- **LLaMA 2** - Meta 开源模型
- **Mistral** - 高效开源模型

---

## 安全建议

⚠️ **重要**：永远不要在代码中硬编码 API 密钥！

### 最佳实践

1. **使用环境变量** - 将密钥存储在环境变量中
2. **后端代理** - 通过后端服务代理 API 请求
3. **加密存储** - 如果本地存储密钥，使用加密算法
4. **定期轮换** - 定期更新 API 密钥

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
```

---

**最后更新**: 2024年6月