---
name: space101-editing
description: 太空101 ChatCut 剪辑与动画技能（**横版 16:9**）：品牌视觉系统（火星余烬橙三皮肤制）、十种标准动画件、零积分资源清单、模板路线图、设计风格库 ID。Trigger when Gavin edits 太空101/雏形 videos in ChatCut, builds motion graphics/templates/animations, applies the show brand or design styles, or asks about ChatCut credits/free resources. Use together with prototype-episode skill for full episode production.
---

# 太空101 Video Editing — ChatCut 剪辑与动画手册
2026-09-10 建立并拆分为独立 skill。与 prototype-episode（选题/脚本/管线）配套使用；
版式与本地管线规格在 prototype-episode/FORMAT_6。
**ChatCut 账号内有同源副本**：Workflow Skill「太空101 剪辑规范」(id 904de3be…)，
供 ChatCut 自带 Agent 使用。本文件是**唯一真源**（git 跟踪）。
⚠️ 同步坑（2026-09-20 实测）：`manage_skill update_from_directory` 只能在 **ChatCut 自带 Agent**
（有后端工作区）上跑；**Claude Code 外部 desktop MCP 跑不了**（"no backend filesystem workspace"，
且无接受内联内容的 action）。故本文件改动后，账号副本需从 ChatCut 内置 Agent 侧执行 update_from_directory
才能同步——外部改完先记为待同步。

品牌视觉规范见本文件《品牌》节（共创中）；版式/管线见 FORMAT_6。

## 画幅（2026-09-10 Gavin 定：横版）
- **本技能面向横版 16:9（1920×1080）**——EP6 起太空101 以横版制作，优先使用 ChatCut
  内面向横版的能力与模板。竖版 1080×1920 规格（气泡/卡/字幕几何）为 EP1-EP5 遗留，
  见 prototype-episode/FORMAT_6，仅在明确要竖版发布时使用。
- 横版布局基线（EP6 首集验证中，验证后固化数值）：主持人全屏为默认态；字幕底部
  居中单行；角标左上「雏形·太空101」；十种动画件与三皮肤/单橙法则照用。
- **卡片尺寸二分法（Gavin 2026-09-11 定，硬规则）**：
  ① 大卡/信息密集卡 → **直接全屏**，完全盖住脸——禁止"占大半屏露一条脸"的中间态；
  ② 小图形/单数据点 → 贴入画面空位：头部左侧的空区、脸下方的空区——脸保持全屏主体，
  图形来找空隙，而不是图形压人。每张卡先判断属于哪一类再定尺寸，没有第三类。

## 分工（不变的铁律）
- **ChatCut**：AI 生成（扣积分）· A-roll+AI片段粗拼 · 内置效果/转场/缩放 · MG 代码动画 ·
  模板系统 · 导出——**剪辑/MG/效果/导出全部零积分，只有 submit_* 生成任务扣积分**。
- **本地管线**：字幕、分段合成、QC、母带交付（EP5 工具链，scripts/ep5_pipeline/）。
- Desktop 专属：AI Portrait Cutout（人像抠像）本机模型，零积分（15s≈90s 处理）。

## 品牌（共创记录，未定项标注）
- ✅ 签名色方向：**暖色**。主候选 B「火星余烬」：暖黑底 #0A0806-#12100E · 锈橙 #E05A2B ·
  沙色 #D9C6A8 · 暖白 #F5EFE8。备选 D「发射曙光」金 #E9B84F（若并用：橙为主、金只做
  终章升华/endcard 专用色）。
- ✅ 卡面弃黄调纸面（"not tech enough"—Gavin）。
- ✅ **三皮肤制（Gavin 2026-09-10 定）**：品牌恒定层（暖黑底+余烬橙+四字体+运动语言）
  不变，卡面三种皮肤并存、**每集选一**。已存入 ChatCut 风格库「我的风格」：
  ① 冷白实验室 (a02d77db1d) #EDF0F3 —— 数据密集集
  ② 深空控制台 (9e9352b6d6) #141A22+暖细边 —— 沉浸叙事集
  ③ 工程蓝图 (630f2d0276) #12263E+白线稿+虚线框 —— 机制拆解/旗舰集
  每集开工时 manage_design_style apply 对应皮肤；单橙法则与曙光金终章限定写在
  每套 styleGuide 里。旧「雏形·纸墨档案」(3d3d454399) 风格已过时，勿用（待删）。
- 字体（ChatCut 渲染器目录已验证可用名）：Noto Serif SC（标题/字幕）· LXGW WenKai TC
  （楷体正文）· Playfair Display（衬线大数字）· Ma Shan Zheng（书法角标）。
- 定稿后动作：写入 ChatCut 设计风格「我的风格」（manage_design_style create）→
  所有 MG/模板自动继承；同步更新本文件与 FORMAT_6。

## 十种标准动画件（全零积分；1-5 自写 MG，6-10 内置）
| # | 名称 | 服务节拍 | 实现 |
|---|---|---|---|
| 1 | 计数滚动卡 | 数字轰炸 | MG：大衬线数字滚动+下划线自画（每集3-5次，模板优先级最高） |
| 2 | 真比例对比条 | 数字对比 | MG：条形按真实比例生长，签名色条压轴 |
| 3 | 承诺时间线 | 跳票/演变叙事 | MG：节点逐亮，失效项划线，末格签名色 |
| 4 | 轨道转移示意 | 讲机制 | MG：SVG 单坐标系，行星公转+虚线弧自画+计数器 |
| 5 | 引文打字机卡 | 条文/引语 | MG：逐字打出，关键短语下划线扫过，风险词变色 |
| 6 | 放大镜聚焦 | 看文件 | 内置 Magnifying Glass / Dome Magnifier 压文件截图 |
| 7 | 马赛克揭密 | 解密时刻 | 内置 Local Mosaic：先打码，说到即揭 |
| 8 | CRT 老监视器 | 档案影像 | 内置 CRT Retro 套旧闻/老发射画面 |
| 9 | 变焦标点 | 结论/悬念 | Zoom 预设：Punch=重锤 · Slow Push=渐近 |
| 10 | 品牌转场三件套 | 剪辑语法 | 只用三种：Whip Pan=清单项间 · Dip to Black=章节T点 · Impact Shake=slam |

MG 授权规则：所有 MG 走 create_motion_graphic_from_code（免费）；先做代表作给 Gavin
验收，通过后才批量/成模板（chatcut-create-motion-graphics skill 的代表作门禁）。
可编辑属性必开：文字、数字、颜色——模板改字改数即可复用。

## AI 概念镜头系统（第二种 AI 影像模式，2026-09-11 立）
与 diorama 并列的 AI B-roll 模式，职责不同：
- **diorama 微缩模型** → 证物感/数据场景（账本、装置、基地剖面）；
- **概念镜头（本节）** → 填补"不可拍摄的画面"：抽象隐喻、不存在的未来场景、
  看不见的过程。实拍管拍得到的，概念镜头管拍不到的。

**三类题材**（生成前先归类）：
1. 历史/科学类比——如"炼金术vs数学"：黑板前的孤独科学家 ↔ 炉火前的中世纪炼金术士；
   "试错迷宫"：千条分岔死路的搜索空间可视化。
2. 反乌托邦/哲学可视化——把抽象概念实体化（如"监控长出手脚"=暗色城市上空的巨型机械体）。
3. 假想边界场景/未来图景——机器人做高风险家务、火箭空中解体的氛围插画等。

**画面风格（用法学参考对标，色彩必须回到本品牌）**：
- 半写实概念艺术（semi-photorealistic concept art）：粗粝真实质感（拉丝金属/粉笔灰/
  暗色石料/磨损机械关节），拒绝卡通感和亮面 stock 味。
- 构图：中景/特写 hero shot，浅景深虚化背景，视线锁在隐喻主体上。
- 光色：高对比主光 + 体积雾 + 深阴影——但调色**必须落在本品牌色域**：暖黑深空底色温、
  余烬橙 #E05A2B 做唯一强调光/警示光，沙色暖白做辅助——**不用**参考对标的
  teal/cyan/crimson 冷色系。单橙法则照常适用。

**剪辑语法**：
- Ken Burns 永动：每张概念图必须带持续镜头运动——105%→112% 缓推，或对角缓移，禁静止。
- 节奏：单张 1.8-2.5s，严格对齐口播句拍；概念镜头是标点不是段落。
- 进出：0.3s 快速转场（whip-pan / 数字瞬切）+ 低频 whoosh 音标记"从现实进入隐喻"；
  与品牌转场三件套兼容。
- 层级：概念图放底层视频轨作高对比画布，文字标注/划重点卡/图形叠加在上层轨。
- 内容对位逻辑：隐喻实体化——讲"黑盒"就画黑盒，讲"炼金术"就画炼金术士，
  不用泛泛的代码滚屏/星空素材充数；术语必须翻译成一眼看懂的画面钩子。

**⛔ 人工验证硬门（Gavin 2026-09-11 钦定，任何情况下不得跳过）**：
1. 未经 Gavin 明确许可，**禁止生成任何 AI 图片/视频**（生成扣积分）。
2. 流程顺序锁死：先剪完全部实拍 B-roll → 再做完动画 → Gavin 说"可以生成了"
   → 才提交生成（附提示词表+预算）→ 生成物逐张交 Gavin 审 → **审批通过的才许上时间轴**。
3. 未过审的生成物不入片、不复用；此门同样适用于 diorama 模式。

## Skill 市场可用件（社区/官方，按需调用）
- 拼贴 B-roll（口播稿→大纸片拼贴，与卡片语言近）· 视频封面生成 · 拉片分镜图 ·
  长视频转短视频 · 透明框口播包装。用前先查其是否触发生成计费。

## 模板路线图（品牌定稿后执行）
1. 按定稿卡面重做动画件 1→2→3→4 的代表作 → Gavin 验收
2. manage_template 存为模板（含可编辑属性）；设计风格存「我的风格」
3. EP6 起：脚本标注哪句用哪个模板件，粗拼阶段直接套用
4. 角标/气泡环/endcard 同步换新色系；本地管线 furniture 重渲一套

## 经验坑位
- AI 效果（抠像等）状态用 track_progress target=effect 轮询；处理中导出会缺层。
- 预览缩略图不渲染 AI 效果——验收必须 local_export 真渲染后抽帧。
- local_export 相对路径落 ~/Movies/ChatCut/；绝对路径会弹系统保存框需人点。
- 背景替换（抠像+MG背景）技术可行但 Gavin 否了观感（2026-09-10）——不默认使用，
  拍摄端物理改景优先。

## EP7 实战锁定（2026-09-20 · 太空数据中心一集全程验证）

> 下面是"我喜欢、以后要复用"的**技法库**，不是固定模板。**每集跳出框架、按内容重新设计**；
> 这些只是可调用的手法。**尤其偏爱侧栏卡（sidebar）。**

### ★ 两大核心心法（最重要，先记这两条）
1. **心法①：会生成 AI 内容 + 锁定风格。** 纸模微缩 diorama 配方（见 C 节）——这是要复刻的核心能力。
2. **心法②：卡片技法。** 每张卡都要**大量加图、加运动、加动态**，一张卡绝不静止；见 A/B 节。

### ★ AI 占比铁律（把整片当 100%）
本集 AI 生成用得**偏多**（可接受，为验证风格）。**未来：少用 AI 视频、多用卡片、多用真实图片/B-roll。**
优先级：**卡片 + 真实图/B-roll ＞ AI 静图(+Ken Burns) ＞ AI 视频(i2v，只给最爱的镜)**。
AI diorama 作点缀/情绪/不可拍画面，**不做骨干**。生成前仍走「人工验证硬门」+ 明确"生成"+预算。

### A. 卡片类型库（本集验证，锁定复用）
1. **侧栏卡（sidebar-over-face，最爱）**——主持人脸在画右、左侧开阔 → 左面板（root 透明，
   `linear-gradient(90deg, 深底0.97→0.93@60%→0@100%)` 右缘淡出到透明，左 8px 橙脊 + 蓝图网格）。
   脸全程可见。开场/立场/机制类"人在说话"段用它。
2. **渐进构建卡（满铺运动铁律）**——禁静态海报：每 ~3–5s 出新元素跟着当前那句话；卡时长裁到
   "最后一拍 +0.5s"；**没有新运动可加就删卡、只留脸**。
3. **中美两语视觉系统**——同皮肤两语法：美国=路演/hype（聚光锥、Playfair 巨数发光、PITCH DECK 角标、
   扫描线、火花、橙 punch 词）；中国=施工蓝图/honest（虚线规划书/节点、手绘橙下划线、印章 seal、
   工程标尺、克制左对齐）。承载"那反观我们中国"。
4. **图卡管线**——顶图+编号+标题+描述，缓 Ken Burns；两三张并排做流程/盘点。
5. **HUD/准星/实时计数卡（活靶子式）**——深底+hero 图+旋转准星+逐帧计数 HUD(标"个人估算")+碎片 blip。
6. **人物 pop-out 引文卡**——名人透明抠像右下角弹入+橙 halo（禁 drop-shadow filter）；
   **本地图不能 propertyOverride → 人像烤进"每人一个专属 MG 资产"**。
7. **填空 furniture**——自绘 SVG 图标流程+连接箭头、四角 corner brackets、巨号淡水印字、工程标尺。别留大片空。

### B. 运动/密度铁律
- **满铺 B-roll**：纯 VO 段每 2–3s 换一镜，≥20 镜/分，单镜静止 ≤1s，**硬切、不复用**，
  一镜一概念严格跟句，**diorama:实拍 ≈ 2:1**（实拍只押情绪点/转场）。
- **卡片**：同上 3–5s 出新；长镜拆短；裁尾不留死气。

### C. AI 生成配方（锁定）
- **选定风格 = 纸模微缩博物馆 diorama**（比"半写实概念艺术暖黑+余烬橙"更受青睐）。
  **模板（只换[主体]/[红色物]，余字不改）**：
  `[主体：具体主角在做动作]. Miniature papercraft diorama, matte low-poly painted-cardboard museum model,`
  `desaturated warm grey-beige palette, everything greyscale EXCEPT one single red accent which is [红色物].`
  `Blurred grey factory-workshop skyline background. Soft even studio lighting, subtle vignette,`
  `retro print-grain texture. Slight low camera angle, three-quarter view, hero object centered, horizontal 16:9.`
  铁律：同调色（暖灰+唯一红）/同虚化工厂背景/同柔光/同颗粒/同微低机位；只换主角；
  **红色是视线锚，一两个母题（卫星/红）反复出现黏合硬切。**
- **静图管线**：`submit_image`(gpt-image-2.5-flare, 16:9, quality high) → 生成图=云资产**可 propertyOverride**
  （本地推的不行）→ Ken-Burns 包装 MG(img prop + objectFit cover + scale 1.0→1.05 + panDir + "AI·示意"角标) → 放 **V2 空段**，硬切 ~2s。
- **图生视频（让红动起来）**：`submit_video` seedance-2-5, `firstFrame=静图`, 4s, 720p, 16:9；
  prompt="extremely subtle motion, slow gentle push-in, the red […] animates(升/绕/扫/脉冲), everything else holds still, locked-off"。
  **并发≤3（分批）**；**视频必须直接落轨**（`<Video>` 放 MG 前端渲染=黑）；视频只 4s，长槽用 `playbackRate=120/槽帧` 放慢填满。

### D. B-roll 工作流（锁定）
- **来源**：agent 用真 Chrome 打开 Pexels 页抓 `videos.pexels.com` 直链再 curl（页面 HTML 被 Cloudflare 挡 curl）；
  Pexels/Pixabay/NASA=🟢 免署名可商用；**忌 SpaceX-Flickr(CC BY-NC)**。
- **落轨**：专用 **V2 轨（静音）**，层序在 A-roll 上、卡片下 → 旁白继续、卡片盖上、B-roll 只填空段。
- **专有名词配专属素材**（SpaceX/星舰/猎鹰、ISS、造星=机械臂/焊接/钢铁厂）；Blue Origin 免费素材稀缺。
  相关性优先、不复用、时长短、硬切；上轨前抽 3 帧验（黑场/彩条/slate/花絮）。webm 可导入但别塞进 MG。

### E. 轨道结构（锁定）
V1 A-roll（底、含旁白音）→ **V2 B-roll+diorama（静音, order1）** → **V3 卡片/MG（order2）**。B-roll 只在空段。

### F. 技术坑位（务必避免，本集踩过）
- MG 校验器：属性必须以 `props.X` 读（别用别名）；声明的属性/读入的颜色变量**都必须被用**；
  `interpolate` outputRange 必须字面量数组（禁 `.map()`）；箭头返回对象要 `})`。
- **渲染变黑**：多层 drop-shadow/blur filter + 超大 world+多图+抠像 会把前端预览打黑 →
  盘点用 **v9(真人像 badge)不用 v13(全身抠像)**；避免 filter 链；单张模糊背景 OK。
- `<Video>` 放 MG=前端黑 → **视频直接落轨**。
- 本地 push 的图**不能** propertyOverride（无 remoteUrl）；生成/云图可以。
- `submit_video` 并发≤3；视频时长≤生成长度，长槽用 playbackRate 填。
- 片是 16:9 就生 16:9（生成前确认画幅，别默认竖屏）。`preview_timeline` limit≤100。

### G. 合规与授权
- AI 镜：抖音"内容由AI生成"声明 + 逐镜"AI·示意"角标（直接落轨的视频会丢角标 → 全局兜底或另叠角标）。
- 署名：CC-BY/🔴 写进简介（贝索斯/黄仁勋=Wikimedia CC-BY，NOIRLab 星座=CC-BY，公司渲染/央视/新华=🔴自担）。
- 本集经 Gavin 明确**启用中美对比**（覆盖 FORMAT_6 无中美对比原则）。
