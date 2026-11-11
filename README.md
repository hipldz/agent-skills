# agent-skills

个人使用的 Agent Skills(目前是Codex为主)，包含个人文章文风复刻、本地会话管理和 Azure 图片生成工具。

> 最后更新：2026-11-11

## 技能列表

| Skill | 用途 | 说明 |
| --- | --- | --- |
| [`write-pldz-articles`](write-pldz-articles/SKILL.md) | 复刻本人的文章文风，支持新写、续写、改写和风格审稿 | 参考语气、措辞、句子节奏和展开方式，不限博客或技术文章 |
| [`codex-session-manager`](codex-session-manager/SKILL.md) | 列出、检查、归档、恢复和删除本地 Codex 会话 | 提供 Python CLI 和本地 Web UI |
| [`azure-image-gen`](azure-image-gen/SKILL.md) | 通过自己的 Azure OpenAI GPT-Image-2 部署生成图片 | 需要 Azure 部署和环境变量配置 |

## 安装

在 WSL/Linux 中，从本仓库根目录执行，将需要的 skill 目录复制到 `~/.agents/skills/`：

```bash
mkdir -p ~/.agents/skills
cp -R write-pldz-articles codex-session-manager azure-image-gen ~/.agents/skills/
```

可以只保留上面命令中需要安装的目录名。仓库没有 `install.sh` 或预打包压缩包，复制时需保留各 skill 的完整目录结构。

两个工具脚本都只使用 Python 标准库，无需安装第三方 Python 包；会话管理工具要求 Python 3.10+，并通过官方 Codex CLI 执行修改操作。

## 个人文章文风复刻

[`write-pldz-articles/`](write-pldz-articles/) 用来复刻本人写文章的方式，包括语气、措辞、长短句、补充说明和内容展开。支持新写、续写、改写和文风审阅，输出题材、体裁和用途由当前任务决定。

内置样文主要来自过去的技术博客，但技能不限于写博客或技术教程。任务中提供了指定样文时，优先参考那些文字；原有场景索引用于查找内置样文，不是文章分类要求。

在 Codex 中显式调用：

```text
$write-pldz-articles 根据这些想法写一篇短文，像我平时写文章的语气，不需要教程结构。
$write-pldz-articles 参考我提供的两篇文章，把 INPUT.md 改写成我的文风，保留事实和原意，输出到 OUTPUT.md。
$write-pldz-articles 接着这篇文章续写，衔接上文的语气和句子节奏。
$write-pldz-articles 对照我的样文审阅这篇草稿，指出哪些句段不像我写的，暂不全文重写。
```

内置材料是写作方式参考，不是完整文章库；历史案例中的事实和个人经历不能直接移入新稿。未覆盖的体裁仅迁移可观察的写法，可通过提供更接近目标用途的样文校准。使用流程见 [`write-pldz-articles/SKILL.md`](write-pldz-articles/SKILL.md)，内置样文索引见 [`scenario-index.md`](write-pldz-articles/references/scenario-index.md)。

## Codex Session Manager

[`codex-session-manager/`](codex-session-manager/) 提供无第三方依赖的 Python CLI 和本地 Web UI，支持列出会话，以及按完整 UUID 检查、归档、恢复或删除会话。

从本仓库根目录运行：

```bash
python3 codex-session-manager/codex_sessions.py list
python3 codex-session-manager/codex_sessions.py inspect <SESSION_ID>
python3 codex-session-manager/codex_sessions.py archive <SESSION_ID>
python3 codex-session-manager/codex_sessions.py unarchive <SESSION_ID>
python3 codex-session-manager/codex_sessions.py web --open
```

工具默认读取 `~/.codex`，也支持通过 `CODEX_HOME` 指定数据目录、通过 `CODEX_BINARY` 指定 Codex 可执行文件。Web UI 仅绑定 `127.0.0.1`，支持筛选和批量删除。

归档、恢复和删除要求完整 UUID，并调用官方 Codex CLI；CLI 需支持 `archive`、`unarchive` 和 `delete --force` 子命令。永久删除不可恢复，详情及 Windows 配置见 [`codex-session-manager/README.md`](codex-session-manager/README.md)。

## Azure GPT-Image-2 Codex skill

本仓库提供 [`azure-image-gen/`](azure-image-gen/) skill，通过用户自己的 Azure OpenAI GPT-Image-2 部署生成图片文件。

### 配置

设置以下环境变量（密钥不要写入仓库、命令参数或 `auth.json`）：

```bash
export AZURE_OPENAI_API_KEY='...'
export AZURE_OPENAI_ENDPOINT='https://YOUR-RESOURCE.openai.azure.com/'
export AZURE_OPENAI_IMAGE_DEPLOYMENT='YOUR-DEPLOYMENT-NAME'
export AZURE_OPENAI_IMAGE_API_VERSION='preview'  # 可选
```

也支持用 `AZURE_OPENAI_BASE_URL` 替代 endpoint、用 `AZURE_OPENAI_DEPLOYMENT_NAME` 替代部署名。部署名应填写在 Azure 中实际创建的名称。

持久化配置和权限建议见 [`azure-image-gen/references/configuration.md`](azure-image-gen/references/configuration.md)。

### 检查与生成

```bash
python3 ~/.agents/skills/azure-image-gen/scripts/azure_image_generate.py --check
```

配置检查通过后生成图片：

```bash
python3 ~/.agents/skills/azure-image-gen/scripts/azure_image_generate.py \
  --size 1024x1024 --quality high --format png --output-dir ./generated-images <<'PROMPT'
A cinematic concept image of ...
PROMPT
```

也可以在 Codex 中显式调用：

```text
$azure-image-gen 生成一张 1536x1024 的电影感概念图，保存到当前项目。
```

此 skill 用于生成新图片，不支持编辑已有图片。完整工作流、尺寸限制和错误处理见 [`azure-image-gen/SKILL.md`](azure-image-gen/SKILL.md)。
