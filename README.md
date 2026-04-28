# ZhiDu 知读

> 基于《如何阅读一本书》四层次方法论的 Obsidian AI 阅读陪伴代理。把阅读规则转成工具调用驱动的交互流程。

![version](https://img.shields.io/badge/version-0.6.0-blue)
![license](https://img.shields.io/badge/license-MIT-green)
![Obsidian](https://img.shields.io/badge/Obsidian-%E2%89%A51.5.0-purple)
![platform](https://img.shields.io/badge/platform-Desktop%20only-lightgrey)

---

## 这是什么

**ZhiDu 知读** 是一个 Obsidian 插件，把 [Mortimer J. Adler](https://en.wikipedia.org/wiki/Mortimer_J._Adler) 的《如何阅读一本书》四层次阅读方法（基础阅读 / 检视阅读 / 分析阅读 / 主题阅读）落地为一个**可以陪你读书的 AI 代理**。

它不是「让 AI 替你读书」——而是把"先看目录、再做检视、最后分析论证"这套阅读规则，**变成可以一句斜杠命令就触发的工作流**，并把过程产物（结构笔记、概念笔记、辩证笔记）自动归档到你的 Obsidian 仓库里。

> 适合：想严肃读书、又想借 AI 提效但不愿被 AI 取代的人。

---

## 核心功能

| 命令 | 阅读层次 | 一句话效果 |
|------|---------|-----------|
| `/inspect 《书名》` | 检视阅读 | 10 分钟看懂全书结构，输出结构笔记 |
| `/analyze 《书名》` | 分析阅读 | 逐章深读，提炼论证和核心概念 |
| `/theme 话题` | 主题阅读 | 多本书围绕同一话题横向对比 |
| `/ask-four 《书名》` | 阅读问答 | 回答艾德勒的四个基本问题 |
| `/help` | — | 查看完整命令列表 |

所有笔记会自动写入仓库下的 `知读笔记/` 目录。

---

## 快速安装（三步走）

> 详细图文步骤、常见错误处理、卸载方法，请看 [INSTALL.md](INSTALL.md)。

### 1. 装 Obsidian

到 [obsidian.md/download](https://obsidian.md/download) 下载并安装（免费、不需要注册）。第一次打开时创建一个"仓库（vault）"，记住它在哪个文件夹。

### 2. 把插件文件放到正确位置

把本仓库 `zhidu-reader/` 文件夹（含 `main.js` / `manifest.json` / `styles.css` 三个文件）整个复制到：

```
<你的仓库>/.obsidian/plugins/zhidu-reader/
```

> ⚠️ `.obsidian` 是隐藏文件夹，需要在文件资源管理器里打开"显示隐藏项目"。

### 3. 启用插件 + 填 API Key

1. 重启 Obsidian → 设置 → 第三方插件 → 关闭"安全模式" → 启用 **ZhiDu 知读**
2. 点插件右边的齿轮 → 把第二步申请到的 API Key 粘贴进去
3. 左侧工具栏点"书本"图标，打开聊天面板，开始用

---

## API Key 配置

插件靠大模型工作，需要一把"钥匙"。**默认接智谱 GLM**（注册简单、新用户有免费额度）：

1. 打开 [bigmodel.cn](https://bigmodel.cn/) 注册并登录（手机号即可）
2. 进控制台 → API Keys → 创建一个新的 Key
3. 把 Key 填到插件设置里

| 默认模型 | 用途 |
|---------|------|
| `glm-4.6` | 主模型（对话和推理） |
| `glm-4-flash` | 摘要模型（高并发处理） |

**也支持其他服务商**：DeepSeek、OpenRouter、月之暗面等。在插件设置里切换"服务商"即可。

---

## 配套工具（强烈推荐）

本插件只认 `.md` 格式的书。下面两个免费工具可以补完整个阅读链路：

- 📚 **找书**：[annas-archive.2rdh.com](https://annas-archive.2rdh.com/)  
  Anna's Archive 镜像站。搜书名 → 优先选 EPUB 下载。

- 📄 **PDF / EPUB 转 Markdown**：[mineru.net](https://mineru.net/)  
  上海人工智能实验室开源项目 MinerU 的在线版。中文书、扫描版、含公式表格的复杂版式识别效果都很好。

完整流程：annas-archive 下载 PDF → mineru.net 转 md → 放到仓库 `book-library/` 目录 → 在 Obsidian 里 `/inspect 书名` 开始读。

---

## 常见问题（精简）

**Q：启用后看不到右侧聊天面板？**  
看左侧工具栏有没有"书本"图标，点一下；或按 `Ctrl+P` 搜索 "ZhiDu" 打开。

**Q：API Key 会被同步到云盘吗？**  
会。Key 保存在 `.obsidian/plugins/zhidu-reader/data.json`。如果你的仓库走 git 同步，请把这一行加到 `.gitignore`：
```
.obsidian/plugins/zhidu-reader/data.json
```
本仓库的 `.gitignore` 已经做了这个排除。

**Q：`/theme` 主题阅读会很贵吗？**  
默认最多并发读 10 本书。担心成本可以在设置里调低"摘要模型并发数"和"每个会话的联网搜索上限"。

更多问题（升级、卸载、报错排查）请看 [INSTALL.md 的 FAQ 章节](INSTALL.md#常见问题)。

---

## 兼容性

- ✅ Windows / macOS 桌面版 Obsidian（≥ 1.5.0）
- ❌ iOS / iPadOS / Android（插件依赖桌面端能力，移动端不可用）

---

## License

[MIT](LICENSE) © 2026 ziho

---

## 致谢

- 阅读方法论：Mortimer J. Adler & Charles Van Doren，《如何阅读一本书》（*How to Read a Book*）
- 笔记系统：[Obsidian](https://obsidian.md)
- 默认大模型：[智谱 AI](https://bigmodel.cn) GLM 系列
