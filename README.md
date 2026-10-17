# navi 中文速查表

[![navi](https://img.shields.io/badge/navi-2.24%2B-blue)](https://github.com/denisidoro/navi)

我自己维护的中文 [navi](https://github.com/denisidoro/navi) cheatsheet 仓库。
第一个 cheat 文件以 **navi 命令本身**为例，边用边查，同时也是编写 cheat 文件的语法参考。

## 目录结构

```
.
├── README.md
└── cheats/
    └── navi.cheat    # 以 navi 自身为例的中文速查表
```

## 依赖

- [navi](https://github.com/denisidoro/navi) >= 2.24
- [fzf](https://github.com/junegunn/fzf)（交互选择片段和变量时需要）
- git（`navi repo add` 需要）

## 使用本仓库

方式一，临时指定路径（适合先试用）：

```bash
navi --path ~/文档/haoenz_navi_cheatsheet/cheats
```

方式二，写进配置文件常驻（推荐）。编辑 `~/.config/navi/config.yaml`：

```yaml
cheats:
  paths:
    - /home/yiyan/文档/haoenz_navi_cheatsheet/cheats
```

之后直接运行 `navi` 即可，用 `navi --tag-rules 'navi' ` 只看本仓库的片段。

方式三，作为仓库导入（推送到远程之后）：

```bash
navi repo add <GitHub 用户名>/haoenz_navi_cheatsheet
```

## cheat 文件语法速查

| 写法 | 含义 |
| --- | --- |
| `% tag1, tag2` | 给下一个片段打标签，可用于 `--tag-rules` 过滤 |
| `# 说明文字` | 片段的注释，在列表中作为描述显示 |
| 普通行 | 片段要执行的命令，连续多行会一起执行 |
| `<变量>` | 变量占位符，执行前询问取值 |
| `$ 变量: 命令` | 该变量的候选值来自命令输出 |
| 空行 | 分隔两个片段 |

一个最小示例：

```cheat
% git, 基础

# 克隆仓库
git clone <url>

$ url: echo https://github.com/denisidoro/navi
```

## 常用命令

```bash
navi                               # 交互式浏览全部片段
navi -q '克隆'                     # 预填搜索词
navi --tag-rules 'navi,!基础'      # 按标签过滤，! 表示排除
navi --print                       # 只打印片段，不执行
navi --query '创建仓库' --best-match   # 非交互，直接选最佳匹配
navi repo add denisidoro/cheats     # 导入第三方仓库
eval "$(navi widget zsh)"           # 加载 shell 快捷键组件
```

## 新增内容

在 `cheats/` 下新建 `<主题>.cheat`，用 `% 主题` 作为标签即可；文件会被 navi 自动发现，无需注册。
提交前可以用 `navi --path cheats --print --best-match --query <关键词>` 验证语法。

## 许可

个人使用，未附带许可证。
