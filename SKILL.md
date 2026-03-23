---
name: Dog-XHS
description: "小红书相关操作，覆盖账号定位、选题研究、内容生产、发布执行与复盘修复的小红书全链路运营技能。凡是小红书的浏�?搜索/发布/评论任务，默认必须使�?OpenClaw 内置浏览器流程并指定 profile=\"openclaw\"；除非用户明确要求，否则不要使用系统 open 或外部浏览器�?
---

# Openclaw 小红书运营技能（通用版）

目标：构建可复用的“小红书运营”流程，让任何账号类型都能复用同一套动作框架�?

## 适用范围（默认即通用流程�?

- 账号定位与内容方�?
- 选题产出与争议点挖掘
- 竞品/同类账号对标
- 小红书发布前演练与内容交�?
- 发布后快速复盘（互动结构、评论回复、热点追踪）
- Viral Copy 链路（输�?URL，高贴合学习封面/配图、标题、正文并生成可发布近似结构笔记）

将每类账号的行业细节作为“案例模块（case module）”挂载到通用流程中�?

## 常用术语

- `选题`：可发布、可讨论、可转发的内容切入点
- `引流钩子`：标�?开头一句用于触发停留与点击
- `结构化输出`：标题、正文、互动问句、话题、标签五元组
- `快照`：用于验证页面状态的关键证据快照
- `回放`：流程失败后重试或改道执�?

## 0) 首次使用：配置收集（重要！）

### 触发条件
首次使用本skill时，必须先执行配置收集流程�?

### 对话模板

**�?步：欢迎+说明**
> 你好！我是小红书运营助手 🤖
> 首次使用需要简单配置一下，让我能帮你管理账号～
> 大概需�?分钟

**�?步：收集小红书信�?*
> **小红书配�?*
> 1. 账号名称：（如：狗哥AI之旅�?
> 2. 小红书号：（如：728952472�?
> 3. cookies：需要你的浏览器cookies（a1, webId, xsecappid�?
> 
> 不知道怎么获取？打开小红书创作服务平�?�?F12 �?Application �?Cookies

**�?步：收集小绿书信�?*
> **微信公众号配�?*
> 1. appid：（如：wx77109d7e269659de�?
> 2. appsecret：（你的公众号AppSecret�?
> 3. author：（作者名�?
> 4. account_name：（公众号名称）
> 5. slogan：（口号，可选）

**�?步：确认保存**
> 确认以下信息�?
> - 小红书：xxx
> - 公众号：xxx
> - 保存�?config.json�?

### 保存位置
```
workspace/xiaohongshu/[账号名]/config.json
```

### 配置格式
```json
{
  "xiaohongshu": {
    "account_name": "狗哥AI之旅",
    "xhs_id": "728952472",
    "cookies": {
      "a1": "xxx",
      "webId": "xxx",
      "xsecappid": "xxx"
    }
  },
  "wechat": {
    "appid": "xxx",
    "appsecret": "xxx",
    "author": "狗哥",
    "account_name": "狗哥的胡思乱�?,
    "slogan": "创业 · AI · 那些没人告诉你的�?
  }
}
```

### 自动读取
- 后续操作自动读取 config.json
- 无需重复询问

## 1) 启动与环境校验（所有任务都遵循�?

执行前先�?`references/xhs-runtime-rules.md` 中“运行规则”执行，优先遵循失败可复用顺序�?

- 固定使用内置浏览�?profile：`openclaw`，出现通道异常先切回后再重试�?
- �?browser（openclaw-manager）能力处�?disabled/不可用：先执行一次轻量重试（�?status/profiles），仍不可用则进入故障引导，明确告知用户“当前浏览器工具未启用”，并引导用户按文档启用后再继续（参考：`https://docs.openclaw.ai/tools/browser`）�?
- �?`evaluate` 为先，关键节点少�?`snapshot`，单步动作最多重试一次�?
- 失败后保留已获结果，切稳健路径并汇报�?

## 1) 技能默认行为（所有任务都遵循�?

- **先读本技能目录下�?`persona.md`**（小红书平台专用人设/语气/发布与回复风格）。所有对外文案（发帖/评论回复/私信话术）都必须遵循�?
- 开始新任务前，先读 `knowledge-base/README.md` 这个总览入口，再�?`references/xhs-knowledge-base.md` 的规则检索最近的同类记录；能复用�?pattern 不重复摸索�?
- 优先输出可执行的 SOP 而非一次性内容稿
- 语言优先“能对话”而不是“写报告”：短句、口语、站位明确、可引导评论
- 所有输出默认保留“可追问点”，用于评论区继续延�?

## 1.5) 账号隔离（必须遵守）

�?`references/xhs-account-isolation.md` 执行�?

### 隔离内容�?大类�?
1. **内容隔离**：每个账号只能发布对应方向内�?
2. **发布隔离**：发布前确认账号
3. **数据隔离**：粉�?互动分开统计
4. **素材隔离**：配�?封面/草稿按账号分开
5. **文件夹隔�?*：每个账号独立目�?
6. **封面风格隔离**：每个账号固定封面风�?
7. **运营方案隔离**：每个账号独立operation.md

### 账号清单
| 账号 | 小红书号 | 内容方向 | 状�?|
|------|----------|----------|------|
| 狗哥AI之旅 | 728952472 | AI热点、干货、观�?| 运营�?|
| 男友改造计�?| - | 男士美妆、穿�?| 运营�?|
| 狗哥的美食纪 | - | 美食探店、菜�?| 运营�?|
| 养生�?| - | 养生、健�?| 规划�?|
| 玄学�?| - | 玄学、风�?| 规划�?|

### 执行检查清�?
1. 打开创作后台 �?确认左上角账号名
2. 确认内容与账号方向匹�?
3. 素材放入对应账号目录
4. 发布前二次确认账号无�?

## 2) 账号定位（可复用�?

每个账号先确�?4 个变量：

- 目标用户：年�?场景/痛点（如「下班后碎片时间」「追星讨论人群」）
- 内容价值主张：每篇给用户什么（观点、情绪价值、实操建议）
- 差异化角度：同类账号不做什么、你做什�?
- 风格规范：语气、长度、冲突边界（避免过激�?

输出�?

- 人设关键词（3-5�?
- 内容支柱�? 个）
- 口头�?固定句式�?-3 个）
- 不能碰底线（红线）清单（剧透、人身攻击、虚假承诺）

## 2.5) 账号分析（新增）

�?`references/xhs-account-analysis.md` 执行�?

- 默认采样最�?9-15 篇内容做轻量体检
- 从定位、内容结构、互动转化、辨识度、可持续�?5 个维度判�?
- 输出必须包含“最大优势、最大短板、下一步动作�?

## 3) 通用选题与对标流�?

### A. 平台侧抓取信号（可并行）

1. 先在小红书抓同题材高互动内容（点�?收藏/评论高于近期平均值）
2. 记录可复用字段：`title`, `hook`, `angle`, `结构标签`, `评论信号`, `互动CTA`, `标签组`
3. 汇总前 10-20 条到候选池

### A.1 首页推荐流分析（新增�?

�?`references/xhs-home-feed-analysis.md` 执行�?

- 先看首页推荐流里“为什么推给你�?
- 再提炼可复用的传播钩子、内容结构和选题方向
- 结果优先服务账号定位、选题灵感和后续内容判�?

### B. 需求侧补充信号（行�?场景�?

1. 按主题去主流平台/社媒抓“评论区观点分歧�?
2. 抽取支持/反对/中性观点各一�?
3. 输出可发文争论点（争议但可控�?

### C. 形成选题清单（每轮至�?3 条）

每条选题包含�?

- 选题标题�?0 字内可选）
- 观点标签（支�?反对/中性）
- 预计互动钩子
- 证据来源（哪组高互动数据�?
- 风险提示（是否容易踩线）

## 3.2) 选题灵感（新增）

�?`references/xhs-topic-ideation.md` 执行�?

- 将平台信号、需求信号、账号定位合并成可发布选题
- 默认输出 3-5 条，每条都要带互动钩子和三段式结�?
- 产物可直接作为内容生成或 Viral Copy 的前置输�?

## 3.5) 搜索并浏览（新增操作类型�?

�?`references/xhs-runtime-rules.md` 的搜索与评论入口章节执行�?

- 只允许从搜索结果页进入帖子；
- 优先通知/回复场景前先对位校验�?
- 连续失败回退策略见引用文件�?

## 3.6) Viral Copy（URL �?新笔记）

�?`references/xhs-viral-copy-flow.md` 执行�?

- 输入：目标爆款笔�?URL（可多条）�?
- 输出�? 套可发布素材（封�?配图方案 + 标题 + 正文 + 话题）�?
- 复刻原则：高贴合主题与结构（标题句式、封面信息层级、正文节奏、互动机制），同时避免逐字照抄与素材侵权�?

## 3.7) AI热点检索（新增�?

�?`references/xhs-ai-hotspot.md` 执行�?

- 触发条件：用户说"生成AI日报"�?收集AI热点"�?今日AI新闻"
- 热点来源�?6kr、虎嗅、钛媒体、知乎、微博热搜、TechCrunch、Hacker News�?
- 输出格式：Top 3热点 + 详细热点 + 趋势观察 + 选题建议
- 知识库：每次检索结果保存到 `knowledge-base/hotspots/YYYY-MM-DD.md`
- 频率：建议每天早�?点、下�?点各执行一�?

## 3.8) 配图生成规范

�?`references/xhs-image-prompt.md` 执行�?

### 核心原则
- 禁止出现：小红书logo、XHS标识、其他平台logo
- 设计风格：渐变背�?白色大字+中文+emoji
- 生成流程：先内容确认 �?生成配图 �?最后封�?

### 图片尺寸
- 封面�?:4�?20x960起）
- 内容配图�?:4�?:1

### 配图数量
- 热点/观点�?�?
- 工具测评�?�?
- 教程/评测�?�?

## 3.9) 内容策略与选题�?

�?`references/xhs-content-strategy.md` 执行�?

### 内容结构�?:3:2:1�?
- 干货教程�?0%
- 热点解读�?0%
- 观点讨论�?0%
- 互动话题�?0%

### 标题规范
- �?0�?
- 数字+关键�?情绪�?

### 正文结构
- 开头钩�?
- 核心内容�?段式�?
- 互动引导
- 话题标签�?-8个）

## 3.10) 小绿书同步发布（自动执行！）

�?`references/xhs-wechat-sync.md` 执行�?

### 同步原则
- **小红书发什么，小绿书就发什�?*
- 内容必须一致，只是格式转换

### 流程（自动执行）
1. 小红书发布成�?
2. **自动同步**到小绿书（推送到草稿箱）
3. 格式转换：emoji保留、话题转标签

### ⚠️ 重要：必须使用图片消息（newspic）！
- �?禁止使用图文模式（news�?
- �?必须使用图片消息（newspic�?
- 脚本：`publish_image_post.py` 使用 `article_type = "newspic"`

### 配置
- 公众号：狗哥的胡思乱�?
- AppID：wx77109d7e269659de
- 发布脚本�?*wechat-article-skill**/scripts/publish_image_post.py（newspic图片消息�?

## 3.11) 子频道通知（Skill更新时）

### 规则
- 每次更新skill规范时，手动通知到对应子频道
- 发布不需要自动同步到子频�?

### 通知场景
- 新增功能
- 规范更新
- 账号变更

### 子频道对�?
- 狗哥AI之旅 �?1484919294058954922
- 男友改造计�?�?1484919374631403690

### 通知格式
```
**�?[账号名] Skill更新**

- 更新内容：xxx
- 详情见：references/xxx.md
```

### 小绿书同步（保持自动�?
- 小红书发布成�?�?自动同步到小绿书（草稿箱�?

### 同步内容
- 发布成功通知
- 笔记标题
- 状�?

### 格式
```
**�?[账号名] 笔记发布成功**

- 标题：xxx
- 内容类型：xxx
- 状态：已发�?审核�?
```

## 4) 通用内容模板（小红书�?

每次产出至少 2 个备选：

- 标题（争�?立场/反问，≤20字优先）
- 开头钩子（1-2 句）
- 正文�? 段：观点→证据→反方�?
- 互动提问�? 句）
- 话题�?-8 个）
- 风险标注（是否剧�?/ 引战边界 / 版权风险�?

## 5) 通用发布链路（不发稿�?

详细发布执行路径请直接按 `references/xhs-publish-flows.md` 执行，避免重复维护�?

发布前必须满足的核心点：

- 账号先登录创作后台，确认页面�?`openclaw` profile 可操作�?
- 明确发布类型（视�?/ 图文 / 长文），三要素：封面、标题、正文�?
- 到达“发布”按钮可见处停手，默认不直接点击发布�?
- 若涉及截图确认，优先附件形式发送到飞书，并在用户确认后再发布�?

## 5.5) XiaohongshuSkills 发布（推荐）

使用 XiaohongshuSkills 进行自动化发布，比浏览器更稳定�?

### 发布脚本位置
```
{baseDir}/../xhs-scripts/publish_pipeline.py
```

### 基础发布命令

```bash
python {baseDir}/../xhs-scripts/publish_pipeline.py \
  --headless \
  --title "笔记标题" \
  --content "笔记正文 #话题1 #话题2" \
  --image-urls "https://example.com/image1.jpg" "https://example.com/image2.jpg"
```

### 使用本地图片
```bash
python {baseDir}/../xhs-scripts/publish_pipeline.py \
  --headless \
  --title "笔记标题" \
  --content "笔记正文 #话题" \
  --images "C:/path/to/image1.jpg" "C:/path/to/image2.jpg"
```

### 预览模式（仅填充，不发布�?
```bash
python {baseDir}/../xhs-scripts/publish_pipeline.py \
  --preview \
  --title "笔记标题" \
  --content "笔记正文" \
  --image-urls "https://example.com/image.jpg"
```

### 多账号发�?
```bash
# 指定账号发布
python {baseDir}/../xhs-scripts/publish_pipeline.py \
  --account 账号别名 \
  --headless \
  --title "标题" \
  --content "正文" \
  --image-urls "URL"
```

### 搜索与互�?
```bash
# 搜索笔记
python {baseDir}/../xhs-scripts/cdp_publish.py search-feeds --keyword "关键�?

# 点赞
python {baseDir}/../xhs-scripts/cdp_publish.py note-upvote --feed-id FEED_ID --xsec-token TOKEN

# 评论
python {baseDir}/../xhs-scripts/cdp_publish.py post-comment-to-feed \
  --feed-id FEED_ID \
  --xsec-token TOKEN \
  --content "评论内容"

# 获取数据看板
python {baseDir}/../xhs-scripts/cdp_publish.py content-data --csv-file "/path/to/export.csv"
```

### 注意事项
- 首次使用需扫码登录：`python scripts/cdp_publish.py login`
- 登录状态缓�?12 小时
- 无头模式 `--headless` 推荐后台运行
- 图片可用 `--image-urls`（URL）或 `--images`（本地路径）

---

## 6) 评论与回复（轻量�?

评论检查与回复统一遵循 `references/xhs-comment-ops.md`，并结合 `examples/reply-examples.md` 作文案风格�?

- 默认优先走通知页，先对位后输入后发送�?
- 默认 one-send-per-turn（如无明确要求不连发）�?
- 长度、隐性承诺、风控停损点等风险控制项请以引用文件为准�?

## 6.5) 知识库沉淀（新增）

�?`references/xhs-knowledge-base.md` 执行�?

- 总览入口固定�?`knowledge-base/README.md`
- 细分记录按类型写�?`knowledge-base/accounts/`、`knowledge-base/topics/`、`knowledge-base/patterns/`、`knowledge-base/actions/`、`knowledge-base/reviews/`
- 分析优先沉淀 `pattern` / `topic` / `review`
- 执行动作优先沉淀 `action`
- 任务结束时至少留下可检索的结论、证据、风险和下一�?

## 7) 失败与修复（必须遵循�?

- 自动化失败先重试一次（同策略）
- 仍失败则改道：换到“更稳妥同义路径�?
- 不做无效重复动作；保留当前进度可复用，报告一次用户需手动的单一动作
- 若知识库暂时不可写，先返回结构化摘要，任务结束后补记，不阻塞主流�?

## 8) 通用提取示例（Evaluate�?

通用字段提取脚本示例�?`references/xhs-eval-patterns.md`�?

## 9) 具体案例：陪你看剧（保留为特例）
### 使用方式

本技能主文件保留通用框架；垂直行业经验放�?`examples/` 目录，按内容类型选用�?

- 先按《通用流程》跑一�?
- 再加载对应案例文件补齐行业特殊动�?

当前已可用案例：

- `examples/drama-watch/case.md`（陪你看剧账号）

每个内容类型按目录组织，文件命名可为�?

- `examples/<vertical>/<vertical>.md`（推荐）
- �?`examples/<vertical>/README.md`


- `examples/lifestyle/`（待补充�?
- `examples/cosmetics/`（待补充�?
- `examples/fitness/`（待补充�?

---

## 实操经验（持续有效）

- **统一规则：所有浏览器操作一律走内置浏览�?profile=`openclaw`**（除非用户明确要求使�?Chrome 扩展 Relay）�?
- 文字配图是稳定写入口，typed text 直接成为封面文案
- 发布话题优先�?UI 选题，不建议纯文本粘贴大�?`#话题`
- `evaluate` 批量改写富文本时，尽量少改版式，避免丢失 topic entity
- 关键步骤前保留一次快照，可用于复盘与问题定位
- `发布` 按钮可见 �?发布成功；必须明确标注“到发布页停手�?
- 若出现新类型评论节奏问题，优先减少每小时回复密度而非提高频率

## 运营成熟路径（可选）

- 标题池：按“站�?反问/冲突”各保留 10 条可复用模板
- 话题池：按账号调性建立常用关键词与同义替换列�?
- 复用机制：每次复盘后把可复用表达同步进案例文�?


---

## 5.6) AI����ͼ���ɣ����� image-style-forge��

ʹ�� image-style-forge ����С�������ͼ��Ȼ���Ϸ�����

### ��������
- �û�˵"���ɷ���ͼ"��"���ŷ���"��"AI��ͼ"
- ��ҪΪ�ʼ�����ƥ��ķ���ͼƬ

### ��������

**Step 1: ���� image-style-forge**
ʹ�� {baseDir}/image-style-forge/ �е�������

1. **�����ȡ**����ѡ��
   - �û��ṩ�ο�ͼƬ
   - ��������ṹ��������
   - ���浽����

2. **�����ͼ**
   - ѡ���񣨴�Ԥ�����Զ��壩
   - ������������
   - �������䲻ͬƽ̨����ʾ��

**Step 2: ���ɷ���ͼ**
���� AI ��ͼ��ʹ�õ�ǰģ�ͻ����� API����
- Gemini / DALL-E / Flux / SD

**Step 3: ƴ�ӷ��棨��ѡ��**
�������ֵ��ӣ�ʹ�� ImageMagick��
`ash
convert background.png -gravity center -pointsize 48 -fill white -annotate +0+0 "��������" cover.png
`

**Step 4: ����**
�����ɵ�ͼƬ·������ xhs-scripts ������
`ash
python xhs-scripts/publish_pipeline.py --headless --title "�ʼǱ���" --content "����#����" --images "���ɵķ���ͼ·��.png"
`

### Ԥ�����
{baseDir}/image-style-forge/styles/ �а�����
- cute / fresh / warm / bold / minimal
- retro / pop / notion / chalkboard / study-notes

### �򻯰棺ֱ������С������ͼ
�����踴�ӷ�񣬿�ֱ���� AI ���ɣ�

��ʾ��ģ�壺
"С���������3:4���棬[��������]�����䱳������ɫ���ֱ��⣬��Լ�ִ������壬8k"

---

## 5.7) AI����ͼ���ɣ��Ƽ���

ʹ�� Gemini Nano Banana Pro ����С�������ͼ��

### ���ɷ���

**Step 1: ���ɷ���ͼ**

ʹ�� scripts/generate_image.py��

`ash
uv run scripts/generate_image.py --prompt "С�����������" --filename "cover.png" --resolution "1K"
`

**��ʾ��ģ��**��
`
С������棬3:4���棬[����ؼ���]�����䱳������ɫ���ֱ��⣬�ִ���Լ�����壬8k
`

**ʾ��**��
`ash
uv run scripts/generate_image.py --prompt "С������棬AI�ձ�����ɫ�Ƽ��б�����AI�����ˣ����ִ��ԣ��ִ���Լ�����壬8k" --filename "ai_daily_cover.png" --resolution "1K"
`

### ������������

**Step 1: ���ɷ���**
`ash
uv run scripts/generate_image.py --prompt "��������" --filename "cover.png" --resolution "1K"
`

**Step 2: ������ʹ�ñ���ͼƬ��**
`ash
python xhs-scripts/publish_pipeline.py --headless --title "����" --content "����#����" --images "cover.png"
`

### ע������
- ����ߴ磺3:4 ���棨1080x1440��
- �ֱ��ʣ�1K �㹻
- ��񣺼�Լ�ִ������䱳�������ֱ���
- API��ʹ�� GEMINI_API_KEY

### ����Ҫ��
- uv ����
- GEMINI_API_KEY ��������

---

## 6) ������ظ���������

