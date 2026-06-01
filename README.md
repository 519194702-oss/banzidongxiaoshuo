# 终极可拖拽互动小说编辑器 v3.0 - 多用户版

[![GitHub License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Version](https://img.shields.io/badge/version-3.0-brightgreen.svg)]()
[![Awesome](https://img.shields.io/badge/awesome-yes-ff69b4.svg)]()

一个功能强大的Web应用，用于创建、编辑和管理互动小说。支持**多用户认证**、AI生成、拖拽排序、多项目管理、多格式导出等高级功能。

**🚀 [立即体验](./index-v3.html)** | **📚 [完整文档](./docs/)** | **🎯 [快速开始](#快速开始)**

---

## ✨ v3.0 新功能亮点

### 🔐 用户认证系统
- **用户注册/登录** - 安全的用户账户管理
- **个人账户** - 每个用户拥有独立的项目空间
- **密码加密** - 基础密码哈希存储（生产环境应使用bcrypt）
- **登出功能** - 安全退出账户

### 📁 多项目管理
- **创建多个项目** - 支持无限数量的小说项目
- **项目列表** - 快速查看和切换项目
- **项目统计** - 显示每个项目的分支数和字数
- **项目切换** - 一键加载不同的项目

### 📝 核心功能（继承自 v2.0）
- ✅ **分支树管理** - 可视化树状分支结构
- ✅ **拖拽排序** - 使用 Sortable.js 实现
- ✅ **编辑删除** - 支持分支的编辑和删除
- ✅ **撤销/重做** - Ctrl+Z / Ctrl+Y
- ✅ **版本历史** - 完整的版本快照
- ✅ **多格式导出** - HTML / PDF / JSON / Markdown
- ✅ **实时搜索** - 快速定位分支
- ✅ **AI 集成** - OpenAI / Claude / 本地 LLM
- ✅ **快捷键支持** - 快速操作

---

## 🎯 快速开始

### 1️⃣ 直接在线使用（推荐）

```
打开 index-v3.html 文件
```

### 2️⃣ 本地运行

```bash
# 克隆仓库
git clone https://github.com/519194702-oss/banzidongxiaoshuo.git

# 进入目录
cd banzidongxiaoshuo

# 用浏览器打开
open index-v3.html  # macOS
start index-v3.html # Windows
xdg-open index-v3.html # Linux
```

### 3️⃣ 使用步骤

**首次使用：**

```
1. 打开 index-v3.html
   ↓
2. 注册账户 (输入用户名、邮箱、密码)
   ↓
3. 登录账户
   ↓
4. 创建新项目
   ↓
5. 开始创建你的互动小说！
```

---

## 📊 版本对比

| 功能 | v1.0 | v2.0 | v3.0 |
|------|------|------|------|
| 基础编辑 | ✅ | ✅ | ✅ |
| 现代 UI | ❌ | ✅ | ✅ |
| 撤销/重做 | ❌ | ✅ | ✅ |
| 版本历史 | ❌ | ✅ | ✅ |
| 多格式导出 | ✅ | ✅ | ✅ |
| AI 集成 | ✅ | ✅ | ✅ |
| **用户认证** | ❌ | ❌ | ✅ |
| **多项目管理** | ❌ | ❌ | ✅ |
| **多用户支持** | ❌ | ❌ | ✅ |

---

## 🔧 配置 AI API

### OpenAI 配置

```javascript
// 在浏览器开发者工具 (F12) 中执行：
localStorage.setItem("openai_apiKey", "sk-your-api-key");
```

### Claude 配置

```javascript
localStorage.setItem("anthropic_apiKey", "your-api-key");
```

### 本地 LLM

```javascript
// 确保本地运行 Ollama
// http://localhost:11434
```

详见 [API 配置指南](./docs/API-Setup.md)

---

## ⌨️ 快捷键

| 快捷键 | 功能 |
|--------|------|
| `Enter` | 提交选择 |
| `Ctrl+Z` | 撤销 |
| `Ctrl+Y` | 重做 |
| `Ctrl+E` | 导出 HTML |

---

## 🏗️ 项目结构

```
banzidongxiaoshuo/
├── index-v3.html              # ⭐ 主程序 (多用户版)
├── index-v2.html              # 改良版
├── index.html                 # 原始版本
├── README.md                  # 项目文档
├── docs/
│   └── API-Setup.md           # API 配置指南
└── .gitignore
```

---

## 🔒 安全性说明

### 当前实现
- ✅ 基础用户认证 (localStorage)
- ✅ 密码哈希存储 (btoa)
- ✅ 用户数据隔离

### 生产环境建议
- 🚀 使用 bcrypt 加密密码
- 🚀 后端验证所有请求
- 🚀 HTTPS 传输
- 🚀 JWT Token 认证
- 🚀 数据库存储

---

## 📦 技术栈

| 技术 | 版本 | 用途 |
|------|------|------|
| **HTML5** | - | 结构 |
| **CSS3** | - | 样式 |
| **JavaScript** | ES6+ | 核心逻辑 |
| **Sortable.js** | 1.15.0 | 拖拽排序 |
| **jsPDF** | 2.5.1 | PDF 导出 |
| **Font Awesome** | 6.0 | 图标库 |

---

## 📝 更新日志

### v3.0 (当前)
- ✅ 完整的用户认证系统
- ✅ 多项目管理
- ✅ 用户项目隔离
- ✅ 项目切换
- ✅ 改进的 UI/UX

### v2.0
- ✅ 现代化设计
- ✅ 撤销/重做
- ✅ 版本历史
- ✅ 多格式导出

### v1.0
- ✅ 基础分支编辑
- ✅ HTML/PDF 导出

---

## 🤝 贡献指南

欢迎提交 Issue 和 Pull Request！

```bash
git checkout -b feature/amazing-feature
git commit -m 'Add amazing feature'
git push origin feature/amazing-feature
```

---

## 📄 许可证

MIT License - 详见 [LICENSE](LICENSE) 文件

---

## 📞 联系方式

- **GitHub**: [@519194702-oss](https://github.com/519194702-oss)
- **Email**: 519194702@qq.com
- **Issues**: [GitHub Issues](https://github.com/519194702-oss/banzidongxiaoshuo/issues)

---

## 🌟 鸣谢

- [Sortable.js](https://sortablejs.github.io/Sortable/) - 拖拽排序
- [jsPDF](https://github.com/parallax/jsPdf) - PDF 导出
- [Font Awesome](https://fontawesome.com/) - 图标库
- [OpenAI](https://openai.com/) - GPT API
- [Anthropic](https://www.anthropic.com/) - Claude API

---

**最后更新**: 2024年6月  
**当前版本**: v3.0 (多用户版)  
**开发状态**: 🟢 活跃开发

🎉 **[立即开始使用 index-v3.html](./index-v3.html)**
