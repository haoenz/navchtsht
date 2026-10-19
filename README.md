# navi 中文速查表

[![navi](https://img.shields.io/badge/navi-2.24%2B-blue)](https://github.com/denisidoro/navi)
[![License: GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg)](https://www.gnu.org/licenses/gpl-3.0)

我自己维护的中文 [navi](https://github.com/denisidoro/navi) cheatsheet 仓库。
现有片段覆盖 12 个工具，每个工具一个 `.cheat` 文件，边用边查，同时也是编写 cheat 文件的语法参考。

两种检索方式并存：

- **按名字查用法**：搜 `repo add`、`widget zsh`、`tag-rules`，直接看到具体命令。
- **按需求找工具**：搜「查找命令」「工具搜索」「命令速查」「速查表」「卸载」「预览」这类功能词，反查该用哪条命令。

## 目录结构

```
.
├── README.md
└── cheats/
    ├── navi.cheat     # navi 本身：搜索、变量、仓库、配置
    ├── git.cheat      # git 本身：日常、分支、远程、撤销、冷门子命令
    ├── zsh-git.cheat  # oh-my-zsh git 插件 alias：按缩写反查
    ├── ouch.cheat     # 压缩解压：tar、zip、7z、rar、zst 等
    ├── keifu.cheat    # Git 提交图 TUI
    ├── difit.cheat    # 浏览器里的 Git diff 查看器
    ├── glow.cheat     # 终端渲染 markdown
    ├── rich.cheat     # 终端富文本：markdown、CSV、JSON、代码高亮
    ├── tokei.cheat    # 代码统计：行数、语言构成
    ├── herdr.cheat    # AI agent 终端工作区：会话、面板、agent、远程
    ├── zellij.cheat   # 终端多路复用：会话、面板、布局、插件
    └── tmux.cheat     # 终端多路复用：会话、窗口、面板、复制模式
```

| 工具 | 一句话用途 | 典型反查词 |
| --- | --- | --- |
| navi | 命令行片段速查表 | 查找命令、工具搜索 |
| git | 版本控制本身 | 变基、撤销、找回提交、子模块、历史改写 |
| zsh-git | oh-my-zsh git 插件 alias 速查 | gst、gco、alias 反查 |
| tokei | 代码行数统计 | 代码统计、行数、语言构成 |
| ouch | 压缩与解压 | 解压、打包、zip |
| keifu | 看 Git 提交图 | 提交图、分支图 |
| difit | 浏览器里看 Git diff、审 PR | 查看差异、代码审查、PR 审查 |
| glow | 终端渲染 markdown | 渲染 md、预览 |
| rich | 终端富文本/表格/高亮 | CSV 表格、语法高亮 |
| herdr | 面向 AI agent 的终端工作区 | AI 代理、面板分屏、远程、agent 管理 |
| zellij | 终端多路复用 | 分屏、浮动面板、布局、会话 |
| tmux | 终端多路复用 | 分屏、会话、复制模式、快捷键 |

## 依赖

- [navi](https://github.com/denisidoro/navi) >= 2.24
- [fzf](https://github.com/junegunn/fzf)（交互选择片段和变量时需要）
- git（`navi repo add` 需要）

## 使用本仓库

方式一，临时指定路径（适合先试用）：

```bash
navi --path ~/文档/navchtsht/cheats
```

方式二，写进配置文件常驻（推荐）。编辑 `~/.config/navi/config.yaml`：

```yaml
cheats:
  paths:
    - /home/yiyan/.local/share/navi/cheats
    - /home/yiyan/文档/navchtsht/cheats
```

第一个路径是 navi 默认目录，保留它才能看到 `navi repo add` 导入的仓库。

之后直接运行 `navi` 即可，用 `navi --tag-rules 'navi' ` 只看本仓库的片段。

方式三，作为仓库导入（推送到远程之后）：

```bash
navi repo add <GitHub 用户名>/<仓库名>
```

## cheat 文件语法速查

| 写法 | 含义 |
| --- | --- |
| `% tag1, tag2` | 给下一个片段打标签，可用于 `--tag-rules` 过滤 |
| `# 说明文字` | 片段的注释，在列表中作为描述显示；**同一片段只保留最后一条** |
| 普通行 | 片段要执行的命令，连续多行会一起执行 |
| `<变量>` | 变量占位符，执行前询问取值 |
| `$ 变量: 命令` | 该变量的候选值来自命令输出；作用于同标签组，同名后写覆盖先写 |
| 空行 | 分隔两个片段 |

另有两个容易踩的点（均已对照 navi 2.24 源码确认）：

- 片段哈希只由标签和注释组成，两者都相同的片段会被**静默去重**（命令不参与判断），所以描述要唯一。
- 注释只有一行生效，写多行不会拼接，只留下最后一行。

一个最小示例：

```cheat
% git, 基础

# 克隆仓库
git clone <url>

$ url: echo https://github.com/denisidoro/navi
```

## 功能索引写法

navi 把「标签列 + 注释列 + 命令列」交给 fzf，并用 `--with-nth 1,2,3` 只搜索这三列的**截断版**。
默认注释列宽 45 列，80 列终端下大约只有**前 20 个汉字**参与搜索，超出部分会被显示截断，也搜不到。

因此本仓库统一采用「功能词前置」的注释格式：

```cheat
# 关键词、同义词｜补充说明
```

例如：

```cheat
# 查找命令、工具搜索、命令速查、命令大全、速查表
navi

# 只打印不执行｜预览、审查、复制命令、管道
navi --print --best-match --query <关键词>

# 移除已导入仓库｜卸载、删除、清理
repo=<repo>; rm -rf "$HOME/.local/share/navi/cheats/${repo:?}"
```

写法要点：

1. 前 20 个汉字内放最可能被搜到的功能词和同义词，`｜` 之后是给人读的补充。
2. 竖线不用 `|`，避免和 shell 管道混淆；注释里的 `#` 只要不在行首就没问题。
3. 终端足够宽时可见字符更多，但按 20 字预算写能保证在窄终端里同样搜得到。

## 常用命令

```bash
navi                                # 交互式浏览全部片段
navi -q '查找命令'                  # 按功能需求反查工具
navi -q 'repo add'                  # 按命令名查具体用法
navi --tag-rules 'navi,!基础'      # 按标签过滤，! 表示排除
navi --print                       # 只打印片段，不执行
navi --query '创建仓库' --best-match   # 非交互，直接选最佳匹配
navi repo add denisidoro/cheats     # 导入第三方仓库
eval "$(navi widget zsh)"           # 加载 shell 快捷键组件
```

## 新增内容

在 `cheats/` 下新建 `<工具>.cheat`，用 `% 工具, 类别` 作为标签即可；文件会被 navi 自动发现，无需注册。
工具用途一律先在本机 `<工具> --help` 核实过再写，避免记错参数。
新增条目按上面的「功能索引写法」组织注释。

提交前做两层验证：

```bash
# 语法与变量能否正常展开
navi --path cheats --print --best-match --query '<注释里的关键词>' < /dev/null

# 功能词能否命中（应返回目标命令）
navi --path cheats --print --best-match --query '卸载' < /dev/null
```

## 许可

本项目以 [GPLv3](./LICENSE) 协议发布。
