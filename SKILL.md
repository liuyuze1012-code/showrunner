---
name: space101-editing
description: 太空101 ChatCut 剪辑与动画技能（**横版 16:9**）：品牌视觉系统（火星余烬橙三皮肤制）、十种标准动画件、零积分资源清单、模板路线图、设计风格库 ID。Trigger when Gavin edits 太空101/雏形 videos in ChatCut, builds motion graphics/templates/animations, applies the show brand or design styles, or asks about ChatCut credits/free resources. Use together with prototype-episode skill for full episode production.
---

# 太空101 Video Editing — ChatCut 剪辑与动画手册
2026-09-10 建立并拆分为独立 skill。与 prototype-episode（选题/脚本/管线）配套使用；
版式与本地管线规格在 prototype-episode/FORMAT_6。
**ChatCut 账号内有同源副本**：Workflow Skill「太空101 剪辑规范」(id 904de3be…)，
供 ChatCut 自带 Agent 使用。本文件改动后必须用 manage_skill update_from_directory
同步该副本（双端一致性责任在本文件持有者）。

品牌视觉规范见本文件《品牌》节（共创中）；版式/管线见 FORMAT_6。

## 画幅（2026-09-10 Gavin 定：横版）
- **本技能面向横版 16:9（1920×1080）**——EP6 起太空101 以横版制作，优先使用 ChatCut
  内面向横版的能力与模板。竖版 1080×1920 规格（气泡/卡/字幕几何）为 EP1-EP5 遗留，
  见 prototype-episode/FORMAT_6，仅在明确要竖版发布时使用。
- 横版布局基线（EP6 首集验证中，验证后固化数值）：主持人全屏为默认态；信息卡=居中
  大面板（~1500w）或左右侧栏板；字幕底部居中单行；角标左上「雏形·太空101」；
  十种动画件与三皮肤/单橙法则全部照用，只换画幅比例。

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
