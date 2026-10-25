# oralenglish-skill

英语专四（TEM-4）口语思辨陪练 Skill。一轮一轮陪练：AI 给出英文思辨 Topic 与一正一反两句参考句型，你口头作答后，AI 逐字转写、地道改写并点评你的中式英语，并给【继续】/【重新回答】两个流程选项。

## 项目解决什么问题

备考专四口语时，很多学生卡在三个痛点：

1. **开口没观点**：面对思辨话题说不出正反两面的表达，缺可直接套用的口语骨架。
2. **中式英语改不掉**：说完自己不知道哪里不对（中文直译语序、中式搭配、逻辑断层、母语负迁移），也得不到针对性的地道改写。
3. **缺练**：没有一轮一轮逼自己开口、反复打磨的陪练节奏。

本项目用纯对话式陪练，针对专四口语给出“出题 → 作答 → 转写 → 改写 → 点评 → 再练”的闭环，重点根治中式英语。

## 主要功能

- **一轮一轮陪练**：每个 Topic 反复打磨，直到你说顺为止。
- **出题带脚手架**：每轮给出 Topic，附【支持】（肯定立场）与【反对】（否定立场）两句纯英文参考句型，可套用可改编。
- **三段式反馈**：
  - ①【我的原句】逐字转写你口述的英文，原样保留表达与错误。
  - ②【优化句】仅 1 版适配专四口语的改写，优先根治中式英语（中文直译语序/中式搭配/逻辑断层/母语负迁移），拒绝浅层同义词替换，核心改动加粗，口语化、不过度书面。
  - ③【简短点评】点明本次中式英语问题，并说明逻辑连贯度、句式地道度、用词自然度。
- **流程自选**：【继续】基于当前话题深度追问开启新一轮；【重新回答】不换话题，重答再反馈，循环至你说【继续】。
- **内置话题库**：12 个专四风格思辨 Topic，开局可自动选题，也支持你指定话题。

**不支持**：网页抓取、PDF 解析、图形界面，不读取文件，全程纯文本对话。

## 目录结构

```
oralenglish/
├── README.md                # 本文档
└── oralenglish-skill/       # Skill 本体（可加载的文件夹）
    ├── SKILL.md             # Skill 说明与流程规则（主文件，纯指令，无脚本）
    └── agents/
        └── openai.yaml      # OpenAI 风格 agent 配置（system prompt + 模型参数）
```

## 安装方法

本项目是一个纯指令型 Skill，**运行时无任何代码/依赖**，安装即“把文件夹放进 Agent 的 Skills 目录”：

```bash
# 1. 将 Skill 文件夹复制到 Agent 的 skills 根目录（如 <workspace>/.user_skills/）
#    以下以 Windows PowerShell 为例：
Copy-Item -LiteralPath "oralenglish-skill" -Destination "<workspace>/.user_skills/" -Recurse

# 2. 确认加载后的路径形如 <workspace>/.user_skills/oralenglish-skill/SKILL.md
```

在支持 Skill 的 Agent 中加载后即可使用，无需额外安装依赖。

> **开发/校验可选依赖**：仅当你要跑官方 `quick_validate.py` 校验脚本时才需要 PyYAML。
> ```bash
> pip install PyYAML
> python <skill-creator>/scripts/quick_validate.py oralenglish-skill
> ```
> 已通过校验，输出 `Skill is valid!`。

## 使用方法

在支持 Skill 的 Agent 中触发本 Skill，直接说“开始练口语思辨”或指定话题即可。每轮流程：

1. AI 给出 **Topic** + 【支持】/【反对】两句纯英文参考句型。
2. 你用英文**口头作答**。
3. AI 输出 ①【我的原句】②【优化句】③【简短点评】。
4. 你选择 **【继续】**（深度追问，开启新一轮）或 **【重新回答】**（不换话题重答，循环改进）。

## 输入输出示例

**输入（开局）**：开始练口语思辨

**输出（出题）**：

> Topic: Should college students take part-time jobs?
> 【支持】I'd argue that taking a part-time job is worthwhile because it builds skills that the classroom can't teach.
> 【反对】On the other hand, I'd say a part-time job distracts students from their real priority — studying.

**输入（作答）**：I think part-time job can help me learn knowledge and earn money, and I think this is very good for my future. My English is poor but I try my best.

**输出（反馈）**：

> ①【我的原句】I think part-time job can help me learn knowledge and earn money, and I think this is very good for my future. My English is poor but I try my best.
>
> ②【优化句】I believe a part-time job helps me **pick up practical skills** and earn some money, which **will benefit my future career**. **My English isn't perfect, but** I'm working hard to improve it.
>
> ③【简短点评】"learn knowledge" 是典型中式搭配（英文用 gain/acquire knowledge）；"My English is poor" 属母语负迁移，更地道说 "My English isn't perfect"。整体逻辑顺，但第二个 and 连接松散，改成 which 引导更连贯。用词已经比较自然，口语里可多用 I believe/I feel 代替重复的 I think。
>
> 【继续】 / 【重新回答】
