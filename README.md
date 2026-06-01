# 终极可拖拽互动小说编辑器

一个功能强大的Web应用，用于创建、编辑和管理互动小说。支持AI生成、拖拽排序、导出等多种功能。

## 📋 功能特性

### 核心功能
- **分支树管理** - 在左侧面板可视化管理故事的所有分支
- **AI 内容生成** - 支持多个AI模型自动生成故事内容
  - OpenAI
  - Claude (Anthropic)
  - 本地 LLM
- **拖拽排序** - 使用 Sortable.js 实现分支的拖拽重排
- **搜索功能** - 按关键词、标签搜索特定分支
- **导出功能** - 支持导出为 HTML 和 PDF 格式

### 数据持久化
- 使用浏览器 localStorage 自动保存所有故事数据
- 浏览器关闭后数据不丢失

## 🚀 快速开始

### 使用方式

1. **打开编辑器**
   - 直接在浏览器中打开 `index.html` 文件

2. **选择AI模型**
   - 在左上角的"模型选择"下拉菜单中选择一个AI模型

3. **输入剧情选择**
   - 在右下角的输入框中输入你的剧情选择
   - 点击"提交选择"按钮添加新分支

4. **展开分支**
   - 点击左侧的分支条目可以为该分支生成子分支
   - 输入弹窗中的剧情描述来继续故事发展

5. **管理分支**
   - 可以拖拽分支重新排序
   - 使用搜索功能快速定位分支

6. **导出成果**
   - 点击"导出 HTML"下载为网页文件
   - 点击"导出 PDF"下载为PDF文档

## 📊 界面布局

```
┌─────────────────────┬──────────────────────────────┐
│   左侧：分支树      │     右侧：内容编辑           │
│                     │                              │
│ • 模型选择          │  ┌────────────────────────┐  │
│ • 搜索功能          │  │                        │  │
│ • 分支树状结构      │  │  故事内容展示区域      │  │
│ • 拖拽排序          │  │                        │  │
│                     │  └────────────────────────┘  │
│                     │                              │
│                     │  ┌────────────────────────┐  │
│                     │  │ 输入框 | 按钮组        │  │
│                     │  └────────────────────────┘  │
└─────────────────────┴──────────────────────────────┘
```

## 💾 数据结构

```javascript
{
  title: "小说标题",
  chapters: [],           // 所有章节
  currentContext: "",     // 当前故事文本
  branchCount: 0,         // 分支计数器
  currentBranches: [      // 分支树
    {
      id: 1,
      choice: "玩家选择内容",
      text: "AI生成的章节内容",
      continuation: "AI生成的续写",
      children: [],       // 子分支
      tags: []           // 标签
    }
  ]
}
```

## 🛠️ 技术栈

- **前端框架**: 原生 JavaScript (Vanilla JS)
- **拖拽库**: [Sortable.js](https://sortablejs.github.io/Sortable/)
- **PDF导出**: [jsPDF](https://github.com/parallax/jsPdf)
- **存储**: 浏览器 localStorage
- **样式**: 原生 CSS

## 📦 依赖

所有依赖均通过 CDN 加载，无需本地安装：

```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/Sortable/1.15.0/Sortable.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
```

## 🔧 自定义与扩展

### 修改小说标题
编辑 JavaScript 中的初始化代码：
```javascript
let novel = JSON.parse(localStorage.getItem("novel")) || { 
  title:"你的小说名称",  // 修改这里
  chapters:[], 
  currentContext:"", 
  branchCount:0, 
  currentBranches:[] 
};
```

### 集成真实AI API
修改 `callAI()` 函数以调用实际的API：
```javascript
async function callAI(prompt, model){
  // 调用你的AI服务
  const response = await fetch('your-api-endpoint', {
    method: 'POST',
    body: JSON.stringify({ prompt, model })
  });
  return await response.text();
}
```

## 📝 示例使用流程

1. 打开页面，开始创建名为"星际探险"的故事
2. 输入第一个选择，如"登上飞船"
3. 系统自动生成内容并展示在右侧
4. 点击分支继续发展故事线
5. 重复步骤2-4创建复杂的分支故事
6. 完成后导出为HTML或PDF分享

## 📄 许可证

MIT License

## 🤝 贡献

欢迎提交 Issue 和 Pull Request！

## 📞 联系方式

- GitHub: [519194702-oss](https://github.com/519194702-oss)
