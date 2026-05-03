# SRT 字幕翻译助手

将 `.srt` 字幕文件翻译成指定语言，保持时间轴和格式不变，并内置术语管理功能确保全文翻译一致性。

## 功能特性

- **格式保留**：完美保持原始时间轴、序号和空行
- **术语管理**：翻译前自动提取术语并生成术语表，避免长字幕前后翻译不一致
- **说话人标记**：保留 `[说话人X]` / `[Speaker X]` 标记
- **口语化处理**：针对播客、访谈类内容优化翻译
- **批量支持**：可翻译单个文件或整个目录
- **多语言支持**：中文、英文、日文、韩文、法文、德文、西班牙文等

## 核心优势：术语管理

长字幕文件（如播客、课程）中，同一术语可能出现数十次。

**无术语表的问题**：
- 第 3 条："大语言模型"
- 第 50 条："大规模语言模型"  
- 第 120 条："LLM"

**有术语表的方案**：
- 所有出现统一译为 "large language model (LLM)"
- 全文一致，专业可靠

翻译前自动提取术语并生成术语表，翻译时严格遵循，确保全文术语统一。

## 安装

### 方式一：直接安装 skill 文件

```bash
# 1. 克隆仓库
git clone https://github.com/yang0/srt-translator.git
cd srt-translator

# 2. 安装到 Claude Code skills 目录（Windows）
mklink /J "%USERPROFILE%\.claude\skills\srt-translator" ".\.srt-translator"

# macOS/Linux
ln -s "$(pwd)/.srt-translator" "$HOME/.claude/skills/srt-translator"
```

### 方式二：手动复制

将 `.srt-translator/SKILL.md` 复制到 Claude Code 的 skills 目录：
```
C:\Users\{用户名}\.claude\skills\srt-translator\SKILL.md
```

## 使用

安装后，在 Claude Code 中直接描述需求即可触发：

```
"帮我把 video.srt 翻译成英文"
"翻译 test 目录下所有字幕文件到日语"
"把 podcast.srt 翻译成法语，用术语表管理"
```

## 工作流程

1. **读取 SRT 文件** — 解析序号、时间轴、字幕文本
2. **提取术语** — 自动识别专业术语、人名、产品名、技术名词等
3. **生成术语表** — 输出 `{文件名}_glossary_{语言代码}.md`
4. **（可选）用户确认** — 修改、补充术语表
5. **翻译字幕** — 分批次翻译，每次携带术语表确保一致性
6. **输出文件** — 生成 `{文件名}_{语言代码}.srt`

## 示例

### 输入：test/test1.srt

```srt
1
00:00:01,790 --> 00:00:03,950
[说话人1] 欢迎收听豆包 AI 播客节目。

2
00:00:07,140 --> 00:00:08,820
[说话人2] 哈喽，大家好，欢迎收听我们的播客。
```

### 生成的术语表：test1_glossary_en.md

```markdown
# 术语表：test1 → English

| 原文 | 译文 | 备注 |
|------|------|------|
| 豆包 | Doubao | 产品名，保留拼音 |
| 播客 | podcast | |
| 大模型 | large language model | 首次出现可写全称 |
| 人工智能 | artificial intelligence (AI) | |
```

### 输出：test/test1_en.srt

```srt
1
00:00:01,790 --> 00:00:03,950
[Speaker 1] Welcome to the Doubao AI Podcast.

2
00:00:07,140 --> 00:00:08,820
[Speaker 2] Hello everyone, welcome to our podcast.
```

## 文件结构

```
srt-translator/
├── .srt-translator/
│   ├── SKILL.md              # Skill 文档（Claude Code 读取）
│   └── srt-translator.skill  # 打包文件
├── test/
│   ├── test1.srt             # 测试用例（中文源文件）
│   └── test1_en.srt          # 翻译结果（英文）
└── README.md                 # 本文件
```

## 支持的语言

| 语言 | 代码 |
|------|------|
| 中文 | zh |
| 英文 | en |
| 日文 | ja |
| 韩文 | ko |
| 法文 | fr |
| 德文 | de |
| 西班牙文 | es |
| 俄文 | ru |
| 葡萄牙文 | pt |
| 意大利文 | it |
| 阿拉伯文 | ar |

## 适用场景

- 视频后期制作中的多语言字幕制作
- 播客节目的国际化翻译
- 在线课程的跨语言发布
- 会议记录的字幕翻译
- 任何需要保持时间轴的 SRT 翻译任务

## 注意事项

1. **备份原文件**：翻译前确认原文件已有备份
2. **检查编码**：确保输出为 UTF-8，避免乱码
3. **单行长度**：字幕文本建议每行不超过 40 个字符
4. **时间轴不变**：只翻译文本，绝不修改时间轴
5. **术语确认**：建议查看生成的术语表，确认关键术语译法

## 贡献

欢迎提交 Issue 和 Pull Request！

## 许可证

MIT

---

**版本**: v1.0  
**维护者**: [yang0](https://github.com/yang0)
