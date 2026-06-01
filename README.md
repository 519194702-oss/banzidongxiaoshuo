# 终极可拖拽互动小说编辑器 v2.0

[![GitHub License](https://img.shields.io/badge/license-MIT-blue.svg)](https://github.com/519194702-oss/banzidongxiaoshuo/blob/main/LICENSE)
[![Version](https://img.shields.io/badge/version-2.0-brightgreen.svg)](https://github.com/519194702-oss/banzidongxiaoshuo)

一个功能强大的Web应用，用于创建、编辑和管理互动小说。支持AI生成、拖拽排序、多格式导出、版本历史等多种高级功能。

## ✨ 核心功能

### 📝 内容编辑
- **分支树管理** - 可视化树状分支结构，支持多层级嵌套
- **拖拽排序** - 使用 Sortable.js 实现分支的实时拖拽重排
- **编辑删除** - 支持编辑已有分支和删除不需要的分支
- **实时搜索** - 按选择内容、文本、标签搜索特定分支
- **分支统计** - 实时显示分支总数、字数统计

### 🤖 AI 内容生成
- **多模型支持**
  - OpenAI GPT-4 / GPT-3.5-Turbo
  - Claude 3 (Anthropic)
  - 本地 LLM (Ollama、LLaMA等)
- **API 密钥管理** - 安全存储和配置各模型的 API 密钥
- **生成进度反馈** - 加载动画和实时状态提示

### 💾 数据管理
- **自动保存** - 每30秒自动保存数据到 localStorage
- **版本历史** - 完整的版本快照和恢复功能
- **撤销/重做** - Ctrl+Z / Ctrl+Y 快速操作
- **多格式导出**
  - HTML - 可直接打开的网页格式
  - PDF - 专业排版的文档格式
  - JSON - 数据备份和导入
  - Markdown - 编辑和分享友好的格式

### 🎨 用户界面
- **现代设计** - 清爽的渐变背景和响应式布局
- **标签页导航** - 故事 / 大纲 / 导出 三个视图
- **三栏布局** - 顶栏导航 / 左侧分支树 / 右侧内容区
- **深色模式友好** - 支持浅色主题，深色模式优化中
- **移动端适配** - 在平板和手机上均可正常使用

### ⌨️ 快捷键支持
| 快捷键 | 功能 |
|--------|------|
| `Enter` | 提交选择 |
| `Ctrl+Z` | 撤销 |
| `Ctrl+Y` | 重做 |
| `Ctrl+F` | 搜索 |
| `Ctrl+E` | 导出 HTML |
| `Ctrl+Shift+D` | 清除所有数据 |

## 🚀 快速开始

### 方式 1：直接使用（推荐）

1. **访问在线版本**
   ```
   https://519194702-oss.github.io/banzidongxiaoshuo/
   ```

2. **本地使用**
   - 克隆仓库：`git clone https://github.com/519194702-oss/banzidongxiaoshuo.git`
   - 用浏览器打开 `index-v2.html`

### 方式 2：配置 AI API

#### OpenAI 配置

```javascript
// 在浏览器开发者工具(F12)中执行
localStorage.setItem("openai_apiKey", "your-api-key-here");
```

详见 [API配置指南](./docs/API-Setup.md)

#### 本地 LLM 配置

1. 安装 [Ollama](https://ollama.ai)
2. 运行模型：`ollama run llama2`
3. 在编辑器中选择"本地 LLM"

## 📊 使用流程

```
1. 打开编辑器
   ↓
2. 选择 AI 模型（如 OpenAI）
   ↓
3. 输入第一个剧情选择（如"登上飞船"）
   ↓
4. 系统自动生成故事内容
   ↓
5. 点击左侧分支继续发展故事线
   ↓
6. 重复步骤 3-5 创建分支故事
   ↓
7. 导出为 HTML / PDF / JSON / Markdown
```

## 💻 技术栈

| 技术 | 描述 |
|------|------|
| **前端** | Vanilla JavaScript (无框架) |
| **UI组件** | Font Awesome 6.0 图标库 |
| **拖拽** | Sortable.js 1.15.0 |
| **PDF导出** | jsPDF 2.5.1 |
| **Markdown** | Marked.js 解析器 |
| **存储** | Browser localStorage + sessionStorage |
| **API** | OpenAI / Anthropic / 本地 LLM |

## 📦 项目结构

```
banzidongxiaoshuo/
├── index-v2.html           # 主程序（改良版）
├── index.html              # 原始版本
├── README.md               # 项目文档
├── docs/
│   └── API-Setup.md        # API 配置指南
└── .gitignore             # Git 忽略配置
```

## 🔧 高级配置

### 修改小说初始标题

在 `index-v2.html` 中找到：

```javascript
const manager = new NovelManager();
// novel 对象会从 localStorage 加载或初始化为：
// { title: "星际探险", ... }
```

修改为你的标题：

```javascript
loadNovel() {
    const saved = localStorage.getItem("novel");
    return saved ? JSON.parse(saved) : {
        title: "你的小说标题",  // 修改这里
        chapters: [],
        currentContext: "",
        branchCount: 0,
        currentBranches: [],
        createdAt: new Date().toISOString()
    };
}
```

### 自定义 AI 调用

修改 `callAI` 函数来使用你的后端 API：

```javascript
async function callAI(prompt, model) {
    const response = await fetch("https://your-backend.com/api/generate", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({
            prompt: prompt,
            model: model,
            max_tokens: 300
        })
    });
    const data = await response.json();
    return data.content;
}
```

### 启用深色模式

在 CSS 中添加：

```css
@media (prefers-color-scheme: dark) {
    :root {
        --primary: #8b9eff;
        --light: #2d3748;
        --dark: #f7fafc;
    }
}
```

## 🔒 安全性

### ⚠️ API 密钥管理

**不要**在代码中硬编码 API 密钥！

**推荐做法**：
1. 在浏览器 DevTools 中手动设置：
   ```javascript
   localStorage.setItem("openai_apiKey", "sk-xxxx");
   ```

2. 使用后端代理（最安全）：
   ```
   浏览器 → 你的后端 → OpenAI/Claude
   ```

3. 环境变量 + 构建时注入（CI/CD）

详见 [API安全指南](./docs/API-Setup.md#安全建议)

## 📈 性能优化

- 使用虚拟滚动处理大量分支
- 定期清理历史版本以节省存储空间
- 异步 AI 调用不阻塞 UI
- 优化 PDF 导出的文本分页

## 🐛 已知问题

- [ ] PDF 导出不支持中文字体（可手动配置）
- [ ] localStorage 有 5-10MB 限制
- [ ] 某些浏览器下拖拽可能有卡顿
- [ ] AI 生成速度取决于网络和模型响应时间

## 📝 更新日志

### v2.0 (当前版本)
- ✅ 完全重写 UI，现代化设计
- ✅ 添加撤销/重做功能
- ✅ 支持版本历史
- ✅ 多格式导出 (HTML/PDF/JSON/Markdown)
- ✅ 分支编辑和删除
- ✅ 实时搜索和统计
- ✅ 快捷键支持
- ✅ AI API 骨架集成

### v1.0
- ✅ 基础分支树编辑
- ✅ HTML/PDF 导出
- ✅ 本地存储

## 🤝 贡献指南

欢迎提交 Issue 和 Pull Request！

1. Fork 本仓库
2. 创建特性分支 (`git checkout -b feature/AmazingFeature`)
3. 提交更改 (`git commit -m 'Add some AmazingFeature'`)
4. 推送到分支 (`git push origin feature/AmazingFeature`)
5. 开启 Pull Request

## 📄 许可证

本项目采用 MIT 许可证 - 详见 [LICENSE](./LICENSE) 文件

## 📞 联系方式

- **GitHub**: [@519194702-oss](https://github.com/519194702-oss)
- **Email**: 519194702@qq.com
- **Issues**: [GitHub Issues](https://github.com/519194702-oss/banzidongxiaoshuo/issues)

## 🙏 致谢

- [Sortable.js](https://sortablejs.github.io/Sortable/) - 拖拽排序
- [jsPDF](https://github.com/parallax/jsPdf) - PDF 导出
- [Font Awesome](https://fontawesome.com/) - 图标库
- [Marked.js](https://marked.js.org/) - Markdown 解析
- [OpenAI](https://openai.com/) - GPT API
- [Anthropic](https://www.anthropic.com/) - Claude API

## 🌟 Star History

如果你觉得这个项目有用，请给个 Star ⭐

---

**最后更新**: 2024年6月  
**版本**: 2.0  
**状态**: 🟢 活跃开发
