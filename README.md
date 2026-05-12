# README HTML Converter Skill

`readme-html-converter` 是一个 Codex skill，用来把项目里的 `README.md` 或其他 Markdown 技术文档转换成独立的 `README.html`。

它不是简单把 Markdown 渲染成网页，而是要求生成一个分区分层、分页分标签、带交互能力的技术文档页面，并且必须保留原始 README 里的全部信息。

## 适用场景

- 需要把 `README.md` 转成更适合展示、交付或部署的 `README.html`
- 技术文档里有安装步骤、运行命令、环境变量、部署参数、API 示例或配置项
- 希望 HTML 文档里提供一键复制命令、参数预览、标签导航、分页阅读和搜索过滤
- 希望文档从纯文本说明升级成一个可交互的说明面板

## 安装方式

把这个仓库克隆到 Codex 的 skills 目录：

```bash
git clone git@github.com:paipaiio/readme.html.git "${CODEX_HOME:-$HOME/.codex}/skills/readme-html-converter"
```

如果已经安装过，可以进入 skill 目录更新：

```bash
cd "${CODEX_HOME:-$HOME/.codex}/skills/readme-html-converter"
git pull
```

安装后，在新的 Codex 会话中就可以通过 `$readme-html-converter` 调用。

## 使用方式

在目标项目目录中发出类似请求：

```text
Use $readme-html-converter to convert the current README.md into a complete interactive README.html.
```

中文也可以这样说：

```text
使用 $readme-html-converter，把当前项目的 README.md 转换成 README.html，要求保留全部信息，并做成分区、分页、分标签和可交互的说明页面。
```

默认情况下，skill 会让 Codex：

1. 完整读取当前目录的 `README.md`
2. 盘点标题、段落、列表、表格、代码块、命令、环境变量、参数、链接和图片
3. 把内容重新组织成更适合阅读的 HTML 结构
4. 在 `README.md` 同目录生成 `README.html`
5. 给命令、配置、API 示例和重要参数增加一键复制按钮
6. 在存在参数设置的场景里增加简单的交互预览
7. 检查 HTML 是否保留了原始 README 的全部信息

## 输出效果

生成的 `README.html` 默认应该具备这些能力：

| 能力 | 说明 |
| --- | --- |
| 分级展示 | 按 README 的标题层级组织内容 |
| 分标签展示 | 按概览、安装、使用、配置、部署、FAQ 等主题拆分标签 |
| 分页或步骤展示 | 对较长的安装、部署、使用流程做分页或步骤切换 |
| 一键复制 | 对命令、配置文件、环境变量、JSON、URL 等增加复制按钮 |
| 参数交互预览 | 用输入框、开关、下拉框等演示参数变化后的配置或命令 |
| 搜索过滤 | 对内容较多的文档提供快速查找能力 |
| 响应式布局 | 在手机和桌面端都能正常阅读 |

## 参数交互示例

如果 README 中包含类似这些参数：

```env
APP_MODE=development
PORT=3000
API_BASE_URL=http://localhost:3000
JWT_SECRET=replace-with-a-secure-secret
```

那么 `README.html` 里可以提供一个小型交互面板，让用户选择运行模式、端口和接口地址，然后实时生成新的 `.env` 示例，并提供复制按钮。

这个演示不需要连接真实系统，只需要帮助读者理解不同参数设置后的效果。

## 仓库结构

```text
.
├── SKILL.md
├── README.md
├── README.html
├── LICENSE
├── agents/
│   └── openai.yaml
├── assets/
│   └── readme-html-template.html
└── references/
    └── conversion-checklist.md
```

各文件作用：

| 文件 | 作用 |
| --- | --- |
| `SKILL.md` | skill 的核心说明，定义何时触发以及执行规则 |
| `README.md` | 当前仓库的使用说明 |
| `README.html` | 当前仓库的可交互使用说明 |
| `agents/openai.yaml` | skill 在 Codex UI 中展示的元数据 |
| `assets/readme-html-template.html` | 生成交互式 README HTML 时可参考的模板 |
| `references/conversion-checklist.md` | 转换完成前的检查清单 |
| `LICENSE` | MIT 开源许可证 |

## 质量要求

执行转换时，需要重点确认：

- `README.html` 没有丢失 `README.md` 的信息
- 原文中的所有标题、命令、代码块、表格、链接、图片和配置项都被保留
- 代码块和关键参数都有复制入口
- 参数演示使用的是 README 中出现过的真实字段，或明确标注为示例值
- HTML 可以直接从本地打开，不依赖外部 CDN
- 移动端不会出现正文或按钮严重溢出

## 许可证

本项目使用 MIT License。详见 `LICENSE`。
