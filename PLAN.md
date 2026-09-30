# AI 可执行开发计划（PLAN）

> 目标：在 `/Users/remixjc/Documents/Works/doubao/funny` 开发「节前摸鱼研究所」静态页，push 到 GitHub Pages 即上线。
> 状态标记：⬜ 未开始 ｜ 🔄 进行中 ｜ ✅ 完成（执行时更新）

## 执行进度快照（2026-09-30）

- T1 项目骨架 ✅　T2 开发计划 ✅　T3 结构与样式 ✅　T4 功能模块 ✅　T5 自检与修复 ✅　T6 提交与交付 ✅
- 自检结果：JS 语法 `node --check` 通过；shot.py 桌面/移动截图无 console 错误、无横向溢出、无死按钮；功能级验证（老板键开合与 favicon/title 切换、50 分映射摸鱼大师、报告卡绘制、理由生成、打卡 1/1）全部通过
- **v1.1 新增「摸鱼达人」小游戏**（2026-09-30）：30 秒限时用手摸鱼、连击每 5 次倍率 +1（最高 x5）、3 秒断连清零、锦鲤 +5 并触发 3 秒双倍、鲨鱼扣 3 分断连、鱼速随时间提升；Canvas 渲染 + WebAudio 连击音效（音调随连击升高）；成绩存档 `my_gbest/gplays/gfish/gcombo`。功能验证通过：连击 7→x2、鲨鱼扣分断连、锦鲤双倍、结算与存储正确；修复 switchView 路由白名单遗漏 game 的 bug

## 硬约束（全部必须满足）

| 编号 | 约束 |
|---|---|
| C1 | **单文件自包含**：所有代码在一个 `index.html` 内（CSS 内联 `<style>`、JS 内联 `<script>`），GitHub Pages 入口必须是 index.html |
| C2 | 零框架、零构建、零外部依赖、无 CDN 脚本、无图片素材（图标全部内联 SVG） |
| C3 | 不用 emoji，图标用内联 SVG；视觉记忆点 = 超大倒计时数字 |
| C4 | localStorage key 统一前缀 `my_` |
| C5 | 兼容 Chrome/Edge/Safari/Firefox 近两年版本；移动端 375px 起；深色模式（`prefers-color-scheme` + 手动切换） |
| C6 | 老板键默认快捷键 `~`（检测 `e.code === 'Backquote'`），假工作界面三选一（Excel/代码/周报），同步切换 `document.title` 与 favicon |
| C7 | 倒计时目标 `2026-10-01 00:00:00 +08:00`，假期结束 `2026-10-07 23:59:59 +08:00`，三态：放假前 / 假期中 / 假期后 |
| C8 | 全部文案自嘲向、无攻击性、无敏感内容；页脚含免责声明 |
| C9 | 不用 `fetch`/`XMLHttpRequest`（file:// 下会被浏览器拒绝），数据全部固化在 JS 内 |

## 数据规格（写入数据层）

| 数据 | 规格 |
|---|---|
| 语录 `QUOTES` | ≥ 30 条，每条 ≤ 20 字，自嘲 + 正能量收尾 |
| 理由 `EXCUSES` | ≥ 50 条，分 5 类：宠物 / 天气身体 / 玄学 / 网络设备 / 自嘲，各 ≥ 8 条 |
| 题目 `QUESTIONS` | 10 题 × 3 选项，选项分值 0 / 5 / 10（满分 100） |
| 签文 `FORTUNES` | ≥ 30 条，格式「宜：X ／ 忌：Y」 |
| 段位 `TIERS` | 6 档：0-15 摸鱼萌新 / 16-30 划水学徒 / 31-45 摸鱼老手 / 46-60 摸鱼大师 / 61-75 摸鱼王者 / 76-100 摸鱼天尊 |

## 任务分解与验收

### T1 项目骨架 ✅（部分）
- [x] `git init` + 分支改名 `main`
- [x] `README.md`（简介 / 部署步骤 / 免责声明）
- [x] `.gitignore`（忽略 `_shots/`、`.DS_Store`）
- [ ] 验收：`git status` 无异常

### T2 开发计划 ✅
- [x] 本文件 `PLAN.md`
- [x] 验收：约束 C1-C9 已列入

### T3 index.html 结构与样式
- [x] 头部：meta / title「节前摸鱼研究所 · 放假倒计时」/ 内联 SVG favicon / 内联样式
- [ ] 视图容器：首页（倒计时+今日签+入口+段位+打卡）/ 测试 / 理由 / 报告（含 canvas）/ 关于
- [ ] 底部 Tab 导航（首页 / 测试 / 理由 / 报告），无僵尸按钮
- [ ] 假工作界面 overlay：Excel / 代码 / 周报三模板
- [ ] CSS：国庆红金配色、倒计时大数字、卡片、Tab、老板键悬浮按钮、深色模式变量、响应式
- [ ] 验收：shot.py 桌面（1440×900）与移动（390×844）无 console 报错、无横向溢出、布局均衡

### T4 功能模块（全部内联 JS，分段注释组织）
- [ ] 数据层：QUOTES / EXCUSES / QUESTIONS / FORTUNES / TIERS / MY_CONFIG
- [ ] 倒计时：三态状态机、1s 刷新、状态文案随剩余时间切换
- [ ] 今日签：日期 seed 伪随机，当天固定；分享文案复制
- [ ] 摸鱼测试：10 题逐题渲染、进度条、段位结果、重测、存档 `my_rank` / `my_tests`
- [ ] 理由生成器：随机出条、换一条、复制（clipboard + execCommand 降级）
- [ ] 诊断报告：Canvas 绘制卡片（1080×1080 与 1200×630 两档）、toDataURL 下载 PNG
- [ ] 打卡：`my_streak` / `my_total_days` / `my_last_checkin`，连续 3 天解锁隐藏称号
- [ ] 老板键：快捷键 + 悬浮按钮、假界面三选一、title/favicon 切换、退出还原
- [ ] 深色模式：`my_theme` 记忆 + 跟随系统
- [ ] 路由：hash 路由或视图切换、前进后退可用
- [ ] 验收：功能清单逐项手动核对（见 T5 验证）

### T5 自检与修复
- [ ] `node --check`：提取 `<script>` 内容逐个做语法检查（用脚本从 html 抽取后执行）
- [ ] 运行 html skill 的 `scripts/shot.py` 生成桌面 + 移动截图，按 lint 报告修复（consoleErrors 优先）
- [ ] 视觉核对：倒计时大数字醒目、无 AI slop、移动端无溢出、卡片列数断点无「最后一行 1 个」
- [ ] 验收：报告无 consoleErrors；截图无布局问题

### T6 提交与交付
- [ ] `git add -A && git commit`（信息：feat: 节前摸鱼研究所 v1.0 全功能静态页）
- [ ] `present_files` 交付 index.html
- [ ] 验收：commit 成功、交付说明 ≤ 8 行

## 验证方式

1. 语法：从 index.html 抽取所有 `<script>` 内容 → `node --check`（写一次性脚本 `_check.js`，用完即弃，不入库）
2. 渲染：`python3 <html-skill-dir>/scripts/shot.py index.html`，读 lint 报告 + 桌面/移动截图
3. 功能：手动核对倒计时三态（用临时改时间/构造日期参数）、段位边界分数、复制降级路径
