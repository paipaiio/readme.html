# README HTML Converter Skill

`readme-html-converter` 是一个 Codex skill，用来把项目里的 `README.md` 或其他 Markdown 技术文档转换成独立的 `README.html`。

它不是简单把 Markdown 渲染成网页，也不是只读取 README。它会先读取 README，再扫描项目结构、入口文件、配置文件、脚本、环境变量样例和部署文件，最后生成一个分区分层、分页分标签、带交互能力的技术文档页面。

## 适用场景

- 需要把 `README.md` 转成更适合展示、交付或部署的 `README.html`
- 技术文档里有安装步骤、运行命令、环境变量、部署参数、API 示例或配置项
- 希望 HTML 文档结合真实项目结构展示入口、脚本、配置、部署和测试信息
- 希望区分信息来源，例如来自 README、`package.json`、`.env.example`、`Dockerfile` 或项目文件树
- 希望发现 README 与真实项目文件不一致的地方，并在页面里标出来
- 希望自动隐藏真实密钥、token、数据库密码等敏感信息
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
Use $readme-html-converter to convert the current README.md and project structure into one complete interactive README.html.
```

中文也可以这样说：

```text
使用 $readme-html-converter，把当前项目的 README.md 和项目结构转换成一个单文件 README.html，要求保留全部信息，并做成分区、分页、分标签和可交互的说明页面。
```

默认情况下，skill 会让 Codex：

1. 完整读取当前目录的 `README.md`
2. 扫描项目结构，重点查看入口文件、配置文件、脚本、环境变量样例、部署文件、测试目录和已有 docs
3. 盘点标题、段落、列表、表格、代码块、命令、环境变量、参数、链接和图片
4. 用真实项目文件校验 README 中的运行命令、配置项、入口和部署说明
5. 给重要事实打来源标记，例如 `README`、`package.json`、`.env.example`、`Observed`
6. 对 README 与项目文件冲突的地方生成可见提示
7. 对真实密钥、token、数据库密码等敏感信息进行脱敏
8. 把内容重新组织成更适合阅读的 HTML 结构
9. 在 `README.md` 同目录生成 `README.html`
10. 给命令、配置、API 示例和重要参数增加一键复制按钮
11. 在存在参数设置的场景里增加简单的交互预览
12. 检查 HTML 是否保留了原始 README 的全部信息，并且体现关键项目结构
13. 只输出一个单文件 `README.html`，不额外生成模板 HTML、预览 HTML、CSS、JS 或资源文件

## GitHub Pages 部署

这个仓库已经包含 GitHub Pages workflow：`.github/workflows/pages.yml`。

它会在 GitHub Actions 里临时执行：

```bash
mkdir -p _site
cp README.html _site/index.html
```

GitHub Pages 的站点入口必须是 `index.html`、`index.md` 或 `README.md`。为了保持仓库里只有一个 HTML 文件，仓库中继续只保留 `README.html`，部署产物里再临时生成 `index.html`。

启用方式：

1. 打开 GitHub 仓库 `paipaiio/readme.html`
2. 进入 `Settings`
3. 左侧选择 `Pages`
4. 在 `Build and deployment` 里把 `Source` 设为 `GitHub Actions`
5. 回到 `Actions`，运行或等待 `Deploy README.html to GitHub Pages`
6. 部署完成后访问 Pages 地址

项目页通常是：

```text
https://paipaiio.github.io/readme.html/
```

如果推送到 `main` 后没有立刻生效，等几分钟再刷新。

## 输出效果

生成的 `README.html` 默认应该具备这些能力：

| 能力 | 说明 |
| --- | --- |
| 分级展示 | 按 README 的标题层级组织内容 |
| 项目结构展示 | 基于实际文件树展示入口、脚本、配置、部署、测试和 docs |
| 扫描摘要 | 展示识别到的技术栈、入口、脚本、配置、部署文件和测试目录 |
| 来源标记 | 标出信息来自 README、配置文件、manifest、部署文件或项目扫描 |
| 冲突提示 | README 与真实项目文件不一致时显示警告 |
| 敏感信息脱敏 | 不展示真实 `.env`、token、私钥、数据库密码等内容 |
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
├── .github/
│   └── workflows/
│       └── pages.yml
├── agents/
│   └── openai.yaml
└── references/
    └── conversion-checklist.md
```

各文件作用：

| 文件 | 作用 |
| --- | --- |
| `SKILL.md` | skill 的核心说明，定义何时触发以及执行规则 |
| `README.md` | 当前仓库的使用说明 |
| `README.html` | 当前仓库的可交互使用说明 |
| `.github/workflows/pages.yml` | GitHub Pages 部署流程，把 `README.html` 作为 Pages 首页发布 |
| `agents/openai.yaml` | skill 在 Codex UI 中展示的元数据 |
| `references/conversion-checklist.md` | 转换完成前的检查清单 |
| `LICENSE` | MIT 开源许可证 |

## 质量要求

执行转换时，需要重点确认：

- `README.html` 没有丢失 `README.md` 的信息
- 已扫描项目结构，并把关键入口、脚本、配置、部署文件和测试信息体现在 HTML 中
- README 中的命令、配置、入口和部署说明尽量与真实项目文件交叉校验
- 关键事实有来源标记或来源说明
- README 与项目文件冲突的地方有可见提示
- 真实密钥、token、数据库密码、私钥等敏感信息不会出现在 HTML 或复制内容里
- 原文中的所有标题、命令、代码块、表格、链接、图片和配置项都被保留
- 代码块和关键参数都有复制入口
- 左侧目录、标签页和分页之间能正确联动，不能出现目录点了但内容仍在隐藏标签页里的情况
- 直接打开 `README.html#某个章节` 时，页面能自动显示对应标签页并定位到章节
- 生成结果只有一个单文件 `README.html`，CSS 和 JavaScript 都内联在这个文件里
- 参数演示使用的是 README 中出现过的真实字段，或明确标注为示例值
- 交互控件可以通过键盘访问，并有清晰的激活和反馈状态
- HTML 可以直接从本地打开，不依赖外部 CDN
- 移动端不会出现正文或按钮严重溢出

## 许可证

本项目使用 MIT License。详见 `LICENSE`。
