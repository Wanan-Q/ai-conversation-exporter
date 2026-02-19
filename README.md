# AI 对话导出工具（Bookmarklet）

一键导出 AI 对话为 Markdown 文档，**零配置、零依赖、所有浏览器通用**。

[![支持平台](https://img.shields.io/badge/平台-6个AI平台-blue)]() [![浏览器](https://img.shields.io/badge/浏览器-全兼容-green)]()

---

## 📊 更新日志

### v2.0（总结 + 导出，推荐使用）

**目录**：`v2.0/`

**核心变化**：从「仅导出」升级为「总结 + 导出」—— 自动发送总结指令给 AI，等待 AI 完成后再导出（含总结内容）。

**支持平台**：6 个（豆包、DeepSeek、Gemini、ChatGPT、元宝、千问）

> ⚠️ **Claude 导出已停用**：v2.0 不再支持 Claude。如需导出 Claude 对话，请使用 v1.0 的 `bookmarklet_claude.html`。

**新增功能**：
- 总结指令：发送「总结当前对话，在对话框直接回复，不需要图片和文件。」（千问夸克版为「总结当前对话，对话框直接回答。」）
- 完成检测：各平台采用不同逻辑判断 AI 是否生成完毕
- 兜底机制：超时（2/3 分钟）后自动导出，避免无限等待

**完成检测逻辑**：

| 平台 | 检测方式 | 说明 |
|------|----------|------|
| 豆包、Gemini、ChatGPT | 停止按钮显隐 | 先记录停止按钮出现过，当其消失时视为完成 |
| DeepSeek、元宝 | 发送键置灰 | 发送按钮从 disabled 恢复为可点击时视为完成 |
| 千问夸克 | loading 消失 | 检测 loading 按钮消失 |
| 千问非夸克 | 剪贴板填入 + 发送键置灰 | 因输入框限制，先复制到剪贴板，用户粘贴后检测发送键 |

**千问区分**：
- `qianwen.com/chat` → 非夸克版（`bookmarklet_qianwen_general_summary_export.html`）
- `qianwen.com/quarkchat` → 夸克版（`bookmarklet_qianwen_quark_summary_export.html`）

**文件**：
- 通用版：`multi_platform_exporter_v2.html`
- 单平台：`bookmarklet_xxx_summary_export.html`（豆包、deepseek、gemini、chatgpt、yuanbao、qianwen_general、qianwen_quark）

---

### v1.0（仅导出）

**目录**：`v1.0/`

**支持平台**：7 个（含 Claude），仅导出当前对话，不包含总结功能。

---

## 📑 目录

- [✨ 核心特性](#-核心特性)
- [📦 支持的 AI 平台](#-支持的-ai-平台)
- [🚀 快速开始](#-快速开始)
  - [方案 A：单平台书签](#方案-a单平台书签推荐打开更快)
  - [方案 B：通用版](#方案-b通用版支持多平台自动识别)
- [📝 使用方法](#-使用方法)
- [🎯 核心功能详解](#-核心功能详解)
- [🔧 添加新平台支持](#-添加新平台支持)
- [❓ 常见问题](#-常见问题)
- [📂 项目结构](#-项目结构)
- [🛠️ 技术实现](#️-技术实现)
- [📊 更新日志](#-更新日志)
- [🔐 隐私与安全](#-隐私与安全)

---

## ✨ 核心特性

- 🚀 **零配置部署**：无需安装 Python、插件或任何依赖，纯浏览器端运行
- 🌐 **全浏览器支持**：兼容 Chrome、Edge、Firefox、Safari 等所有现代浏览器
- 📱 **跨平台通用**：Windows、macOS、Linux 均可无缝使用
- 🎯 **智能内容解析**：自动识别并转换表格、代码块、列表、标题等 Markdown 结构
- 🔄 **即点即导**：在任意支持的 AI 对话页面点击书签即可导出
- 🎨 **格式完美保留**：保留 Markdown 格式、代码语言标记、表格结构、粗体斜体等样式
- ⚡ **双版本方案**：单平台书签（性能优化）+ 通用版本（多平台自动识别）
- 🏷️ **智能命名**：导出文件名包含平台名、对话标题（如有）和时间戳，便于管理

---

## 📦 支持的 AI 平台

| 平台 | 域名 | v2.0（总结+导出） | v1.0（仅导出） |
|------|------|-------------------|----------------|
| 豆包 (Doubao) | doubao.com | ✅ | ✅ |
| DeepSeek | chat.deepseek.com | ✅ | ✅ |
| Gemini | gemini.google.com | ✅ | ✅ |
| 千问 (Qianwen) | qianwen.com/chat、qianwen.com/quarkchat | ✅（分夸克/非夸克） | ✅ |
| ChatGPT | chatgpt.com, chat.openai.com | ✅ | ✅ |
| 元宝 (Yuanbao) | yuanbao.tencent.com | ✅ | ✅ |
| Claude | claude.ai | ❌ 已停用 | ✅ |

---

## 🚀 快速开始

### v2.0（推荐）：总结 + 导出

**通用版**：打开 `v2.0/multi_platform_exporter_v2.html`，拖拽「📝 总结并导出AI对话」到书签栏。

**单平台书签**（打开更快）：
- 豆包：`v2.0/bookmarklet_doubao_summary_export.html`
- DeepSeek：`v2.0/bookmarklet_deepseek_summary_export.html`
- Gemini：`v2.0/bookmarklet_gemini_summary_export.html`
- ChatGPT：`v2.0/bookmarklet_chatgpt_summary_export.html`
- 元宝：`v2.0/bookmarklet_yuanbao_summary_export.html`
- 千问（非夸克）：`v2.0/bookmarklet_qianwen_general_summary_export.html`
- 千问（夸克）：`v2.0/bookmarklet_qianwen_quark_summary_export.html`

### v1.0：仅导出（含 Claude）

**通用版**：`v1.0/multi_platform_exporter.html`  
**单平台**：`v1.0/bookmarklet_xxx.html`（豆包、deepseek、gemini、qianwen、chatgpt、yuanbao、claude）

---

## 📝 使用方法

### 1. 创建书签

**如何显示书签栏**：
- **Chrome/Edge**：按 `Ctrl+Shift+B`（Windows）或 `Cmd+Shift+B`（Mac）
- **Firefox**：按 `Ctrl+Shift+B` 或在菜单中启用
- **Safari**：按 `Cmd+Shift+B` 或在「显示」菜单中启用

**如何添加书签**：
1. 用浏览器打开对应的 HTML 文件（如 `multi_platform_exporter.html`）
2. 将页面上的按钮**拖拽**到浏览器书签栏

### 2. 导出对话

1. 在 AI 对话页面（确保有用户提问和 AI 回复）
2. 点击书签栏中的导出按钮
3. 浏览器会自动下载 `.md` 文件

**示例文件名**：
- `Doubao_20260216_141510.md`
- `ChatGPT_20260216_143025.md`

---

---

## 🎯 核心功能详解

### 1. 智能内容识别

- ✅ **表格识别**：自动识别 `<table>` 并转换为 Markdown 表格，处理 th/td、多列对齐
- ✅ **代码块解析**：识别 `<pre><code>`，自动检测语言类型（class 或内容特征），智能移除行号
- ✅ **标题转换**：H1-H6 转换为 Markdown 标题（层级自动+1，避免与文档标题冲突）
- ✅ **列表处理**：有序/无序列表转换，保留嵌套层级
- ✅ **格式保留**：加粗（`**text**`）、斜体（`*text*`）、行内代码（`` `code` ``）
- ✅ **语言检测**：
  - 优先读取 `class="language-xxx"`
  - 备选：内容特征检测（SELECT → sql, def/import → python）

### 2. 智能过滤机制

自动过滤无关内容，确保导出的对话纯净：

| 过滤类型 | 识别方法 | 说明 |
|---------|---------|------|
| 侧边栏历史 | 位置判断（right < 280px） | 通过 getBoundingClientRect() 过滤 |
| 对话建议 | 长度过滤（< 5 字符） | 过滤空内容和单字符 |
| 工具栏按钮 | 容器选择器排除 | 不在指定容器内的元素自动忽略 |
| 重复内容 | 角色合并逻辑 | 连续相同角色的消息自动合并 |

### 3. 多层级角色识别

采用多种方法确保准确识别用户和 AI 的消息：

**识别方法优先级**：
1. **DOM 属性法**（最可靠）
   - ChatGPT: `data-message-author-role="user|assistant"`
   
2. **CSS 类名法**（最常用）
   - 豆包: className 包含 `justify-end` → user
   - DeepSeek: className 包含 `d29f3d7d` → user
   - 千问: className 包含 `question` → user
   - 元宝: className 包含 `--human` → user
   - Claude: className 包含 `float-right` → user
   
3. **自定义标签法**（Google 特色）
   - Gemini: `<user-query-content>` → user, `<message-content>` → assistant

**智能修正机制**：
- 如果首条消息被识别为 AI，但内容长度 < 300 字符，自动修正为 user（处理误判）
- 连续相同角色的消息自动合并（避免对话碎片化）

---

## 🔧 添加新平台支持

如果你想为新的 AI 平台（如 Kimi、文心一言等）添加支持，可以使用 **AI Agent 自动生成代码**。

### 操作步骤

1. **准备环境**
   - 打开新平台的对话页面（确保有用户提问和 AI 回复）
   - 按 `F12` 打开开发者工具

2. **运行分析脚本**

   **第一步：分析用户消息**
   - 切到 **Elements** 标签
   - 点击左上角的**选择工具**（或按 `Ctrl+Shift+C`）
   - **点击一条用户消息的文字**
   - 切到 **Console**，粘贴以下代码并回车：

   ```javascript
   (function(){
   var el=$0;if(!el){console.log('ERROR: 请先在 Elements 里选中文字');return;}
   console.log('=== 从选中元素向上遍历所有父级 ===');
   console.log('提示：单条消息的容器通常在 Level 3-8 之间');
   console.log('');
   var cur=el;
   for(var i=0;i<30&&cur&&cur!==document.body;i++){
     var tn=cur.nodeName,cn=cur.className||'(no class)',children=cur.children.length;
     var tid=cur.getAttribute?cur.getAttribute('data-testid'):'',mid=cur.getAttribute?cur.getAttribute('data-message-id'):'';
     var role=cur.getAttribute?cur.getAttribute('data-message-author-role'):'';
     console.log('Level '+i+': '+tn+' | class: '+cn+' | children: '+children+(tid?' | testid: '+tid:'')+(mid?' | msgid: '+mid:'')+(role?' | role: '+role:''));
     cur=cur.parentElement;
   }
   console.log('');
   console.log('请把上面的输出复制发给 AI');
   })();
   ```

   **第二步：分析 AI 回复**
   - 继续在 Elements 里，用选择工具**点击一条 AI 回复的文字**
   - 在 Console 粘贴**相同的代码**，回车

3. **使用 AI Agent 生成代码**

   将两次控制台输出（从 `=== 从选中元素向上遍历所有父级 ===` 开始）发给任意 AI Agent（如 ChatGPT、Claude、DeepSeek 等），并提供以下提示：

   ```
   我想为新的 AI 平台添加对话导出支持。这是用户消息和 AI 回复的 DOM 结构分析结果：

   [粘贴两次控制台输出]

   请参考 @README.md 和 @multi_platform_exporter.html，生成该平台的硬编码规则，
   包括：容器选择器、角色判断方法、以及完整的书签代码。
   ```

   **AI Agent 会自动**：
   - 分析 DOM 结构
   - 找出区分用户/AI 的关键特征
   - 生成可直接使用的代码

4. **集成到项目**
   - 将 AI 生成的代码添加到 `multi_platform_exporter.html`
   - 或创建新的单独书签文件（如 `bookmarklet_newplatform.html`）

---

## ❓ 常见问题

### Q1: 提示「未提取到对话内容」或「No messages found」？

**可能原因**：
1. 页面未完全加载完成
2. 平台改版导致 CSS 选择器失效
3. 对话内容在 iframe 或 Shadow DOM 中
4. 使用了不支持的平台

**解决方法**：
1. **等待加载**：确保页面完全加载后再点击书签（等待 AI 回复完成）
2. **刷新重试**：`Ctrl+R` 刷新页面后重新尝试
3. **查看日志**：按 `F12` 打开控制台，查看具体错误信息
4. **验证平台**：确认当前页面的域名在支持列表中
5. **更新书签**：检查是否有新版本的书签代码

### Q2: 表格或代码块格式错误？

**可能原因**：
- 表格/代码块的 HTML 结构特殊（如嵌套 div）
- 包含工具栏、行号等无关元素
- 表格中包含特殊字符（如 `|`）

**解决方法**：
1. **检查导出文件**：用 Markdown 编辑器查看是否可手动修复
2. **优化规则**：使用「添加新平台支持」流程，通过 AI Agent 优化提取规则
3. **手动编辑**：导出后在编辑器中调整格式

**已处理的特殊情况**：
- ✅ 代码块行号自动移除（正则：`^\s*\d+\s+`）
- ✅ 表格管道符自动转义（`|` → `\|`）
- ✅ 表格换行自动处理（`\n+` → 空格）

### Q3: 角色识别错误（用户问题被识别为 AI 回复）？

**原因**：
- DOM 结构特殊或平台改版
- 角色判断规则失效

**自动修正机制**（已内置）：
- 如果首条消息不是 user 且内容 < 300 字符，自动修正为 user

**手动解决方法**：
1. **快速修复**：导出后手动编辑 Markdown 文件，修改 `# User` 和 `# AI` 标题
2. **规则更新**：使用「添加新平台支持」流程重新生成适配规则

### Q4: 单平台书签和通用版有什么区别？

| 对比项 | 单平台书签 | 通用版 |
|-------|-----------|--------|
| **支持平台** | 1 个 | v2.0 为 6 个，v1.0 为 7 个 |
| **代码大小** | ~7KB | ~11KB |
| **加载速度** | 极快 | 稍慢（首次需解析平台判断逻辑） |
| **适用场景** | 只用一个平台（如只用 DeepSeek） | 使用多个平台 |
| **维护成本** | 低（单一规则） | 中（需维护多平台规则） |
| **推荐人群** | 专注单一 AI 工具的用户 | 多平台对比测试的用户 |

**选择建议**：
- ✅ **只用一个平台** → 选择对应的单平台书签（性能最优）
- ✅ **使用 2-3 个平台** → 可两者都装（按需点击）
- ✅ **使用 4+ 个平台** → 推荐通用版（一个书签通吃）

### Q5: 导出的文件编码有问题（乱码）？

**原因**：文件编码不是 UTF-8

**解决方法**：
- 代码已设置 `charset=utf-8`，一般不会出现此问题
- 如果仍有乱码，用 VSCode 打开，右下角选择「通过编码重新打开」→ UTF-8

### Q6: 可以导出指定范围的对话吗（如最近 10 条）？

**当前版本**：不支持，会导出页面上所有可见的对话

**变通方法**：
1. 滚动到想要导出的起始位置
2. 不要向上滚动加载更多历史消息
3. 点击书签导出

### Q7: 为什么有些 AI 回复内容缺失？

**可能原因**：
1. AI 回复尚未完全生成完毕
2. 内容被折叠或隐藏（如「显示更多」按钮）
3. 内容在懒加载区域

**解决方法**：
1. 等待 AI 回复完全结束后再导出
2. 手动展开所有折叠内容
3. 滚动到页面底部确保内容完全加载

---

## 📂 项目结构

```
get_conversation_and_update/
├── v2.0/                                    # 总结+导出（推荐）
│   ├── multi_platform_exporter_v2.html       # 通用版，6 平台
│   ├── bookmarklet_doubao_summary_export.html
│   ├── bookmarklet_deepseek_summary_export.html
│   ├── bookmarklet_gemini_summary_export.html
│   ├── bookmarklet_chatgpt_summary_export.html
│   ├── bookmarklet_yuanbao_summary_export.html
│   ├── bookmarklet_qianwen_general_summary_export.html   # 千问非夸克
│   └── bookmarklet_qianwen_quark_summary_export.html     # 千问夸克
├── v1.0/                                    # 仅导出（含 Claude）
│   ├── multi_platform_exporter.html
│   ├── bookmarklet_doubao.html
│   ├── bookmarklet_deepseek.html
│   ├── bookmarklet_gemini.html
│   ├── bookmarklet_qianwen.html
│   ├── bookmarklet_chatgpt.html
│   ├── bookmarklet_yuanbao.html
│   └── bookmarklet_claude.html
└── README.md
```

---

## 🛠️ 技术实现

### 核心技术栈

- **纯 JavaScript ES5**：无需任何外部库，兼容所有浏览器
- **递归 DOM 遍历**：深度优先遍历，完整解析 HTML 结构
- **正则表达式匹配**：识别代码语言、表格边界、列表层级
- **Blob API**：客户端生成并自动下载 Markdown 文件
- **Bookmarklet 技术**：`javascript:(function(){...})();` 协议实现一键执行

### 平台识别机制（通用版）

通过 `location.hostname` 自动识别当前平台：

| 平台 | 检测域名 | 识别方法 |
|------|----------|----------|
| 豆包 | doubao.com | className 匹配 `justify-end` |
| DeepSeek | chat.deepseek.com | className 匹配 `d29f3d7d` |
| Gemini | gemini.google.com | tagName 匹配 `USER-QUERY-CONTENT` / `MESSAGE-CONTENT` |
| 千问 | qianwen.com, tongyi.aliyun.com | className 匹配 `question` |
| ChatGPT | chatgpt.com, chat.openai.com | attribute 匹配 `data-message-author-role` |
| 元宝 | yuanbao.tencent.com | className 匹配 `--human` |
| Claude | claude.ai | className 匹配 `float-right` |

### 内容提取流程

```
1. 【平台识别】（通用版）
   └─ 根据 hostname 加载对应规则
   ↓
2. 【查找容器】
   ├─ 通过 CSS 选择器定位消息容器
   └─ 过滤位置异常的元素（如侧边栏：right < 280px）
   ↓
3. 【角色识别】
   ├─ 方法1: DOM 属性（data-message-author-role）
   ├─ 方法2: CSS 类名（userPattern 正则匹配）
   ├─ 方法3: 标签名（自定义标签如 USER-QUERY-CONTENT）
   └─ 智能修正：首条消息若非 user 且内容短，自动修正为 user
   ↓
4. 【递归解析 HTML】
   ├─ TABLE → 提取为 Markdown 表格（th/td → | 列 |）
   ├─ PRE/CODE → 提取为代码块（自动检测语言，去除行号）
   ├─ H1-H6 → 转换为 Markdown 标题（层级+1）
   ├─ UL/OL/LI → 转换为 Markdown 列表
   ├─ STRONG/B → **粗体**
   ├─ EM/I → *斜体*
   ├─ CODE（行内）→ `代码`
   └─ 文本节点 → 保留并规范化空格
   ↓
5. 【内容过滤】
   ├─ 过滤位置异常的容器
   ├─ 过滤内容过短的消息（< 5 字符）
   └─ 去除多余换行（3+ → 2）
   ↓
6. 【消息合并】
   └─ 连续相同角色的消息合并为一条（避免碎片化）
   ↓
7. 【标题提取】（部分平台支持）
   ├─ 豆包：[class*="group/title"] .truncate
   ├─ Gemini：span.gds-title-m, span[class*="conversation-title"]
   └─ 文件名格式：平台_标题_时间戳.md
   ↓
8. 【生成文件】
   ├─ 拼接 Markdown：标题 + 时间 + 对话内容
   ├─ 创建 Blob 对象（type: text/markdown;charset=utf-8）
   ├─ 生成临时下载链接（URL.createObjectURL）
   └─ 触发下载并清理资源（URL.revokeObjectURL）
```

### 关键算法说明

**1. 表格提取（exT 函数）**
```javascript
// 遍历 tr -> th/td，转换为 Markdown 表格
// 第一行自动添加分隔符 | --- | --- |
// 处理单元格中的换行和管道符
```

**2. 代码块提取（exC 函数）**
```javascript
// 提取 code 元素的 innerText
// 去除行号（正则匹配 ^\s*\d+\s+）
// 检测语言类型（className 或内容特征）
```

**3. 角色判断（getRole 函数）**
```javascript
// 根据平台规则选择判断方法：
// - attribute: 读取 data-message-author-role
// - className: 正则匹配 userPattern
// - tagName: 检查元素标签名
```

---

## 🔐 隐私与安全

**数据安全**：
- ✅ 纯本地运行，不上传任何数据
- ✅ 不依赖第三方服务
- ✅ 不存储任何个人信息

**敏感内容处理**：
- 导出后可手动编辑，删除敏感信息
- 可使用加密工具（如 VeraCrypt）加密存储文件夹
- 导出的文件建议不要上传到公共云盘

---

