# r8 最优个体（fitness top1=71415.6）新口径逐回合回放报告

> **怎么读这份报告**：本页是 Markdown 版，GitHub 点开直接看，不用下载。

> 同目录还有同内容 HTML 版（`20260918_replay_buy_top1_逐回合回放报告.html`），下载后用浏览器打开，支持折叠/展开等交互；GitHub 网页里点 HTML 只会显示源代码，这是 GitHub 的限制不是文件坏了。

> 逐回合完整择优明细（全部候选、全部评分项）见 `data/replay_buy_top1/` 下各卡组 CSV。


---

## 口径说明

```
            与 bench_base 结果逐位一致：本仓库口径推荐表 = 模拟器终局实际买入清单）

新口径公式 : 总分 = URA属性分(ura_status_to_point 表) + 固有技能 510 + Σ买到技能Grade + 结余总PT×2
             结余总PT = skill_pt + hints×6.5；1 技能点 = 2 评价点（pt_score_rate=2.0）
             育成全程攒 Pt 不学技能；终局 finalize_skill_purchase 按净增分(Grade−价格×2)>0 贪心买入（deck-hint 池含折扣）
```

跑法：与 r8 回放完全同套（bench_base --uma 106402 --trainer handwritten --genome-file genome_top1.toml --seed 1001），7 种卡组各 1 局；代码 umaai-rs @ 62a797c。

## 一、总成绩

| # | 卡组 | 新口径总分 | 评价 | 旧口径对照 | 五维（速/耐/力/根/智） |
|---|------|-----------|------|-----------|----------------------|
| 1 | speed | **86294** | LG16 | 66884 | 速3337 耐2199 力1767 根1395 智1519 |
| 2 | stamina | **90613** | LG23 | 67129 | 速3313 耐2400 力1144 根1540 智1978 |
| 3 | power_wisdom | **88393** | LG19 | 56002 | 速2175 耐1766 力2200 根626 智2445 |
| 4 | speed_wisdom | **98286** | LF11 | 70758 | 速3337 耐2400 力1154 根1381 智2422 |
| 5 | wisdom | **87417** | LG18 | 62707 | 速3161 耐2064 力910 根1172 智2445 |
| 6 | sta0_wis2 | **85846** | LG15 | 61184 | 速3050 耐924 力1744 根1585 智2445 |
| 7 | spd2_gut0 | **91879** | LF | 68080 | 速3309 耐2400 力1970 根1197 智1594 |

**7 卡组新口径均分 = 89818.3**（r8 原回放 7 卡组旧口径均分 64815.4，为 GA 初筛口径，不可直接对比）

## 二、评分分解与终局买技能

### [1] speed — 总分 86294（LG16）

- 评分分解：属性分 64881 + 技能分 727(固有510+买入217) + 结余PT分 20686(总PT 10343×2) = 86294
- Pt 账目：育成攒得后结余 skill_pt=8731，hints=248(折算 1612 Pt)；终局买入 1 个技能，花费 108 Pt，加 217 分
- 终局买入 1 个技能：

  | 技能 | 价格 | Grade | 净增分 |
  |------|------|-------|--------|
  | 打头阵 | 108 | 217 | 1 |
- 对照 r8 原回放：轨迹一致（4/7 卡组因 875dd2c 上游合并+新口径小幅漂移，属预期）

### [2] stamina — 总分 90613（LG23）

- 评分分解：属性分 70402 + 技能分 727(固有510+买入217) + 结余PT分 19484(总PT 9742×2) = 90613
- Pt 账目：育成攒得后结余 skill_pt=8410，hints=205(折算 1332 Pt)；终局买入 1 个技能，花费 90 Pt，加 217 分
- 终局买入 1 个技能：

  | 技能 | 价格 | Grade | 净增分 |
  |------|------|-------|--------|
  | 长距离直线○ | 90 | 217 | 37 |
- 对照 r8 原回放：轨迹一致（4/7 卡组因 875dd2c 上游合并+新口径小幅漂移，属预期）

### [3] power_wisdom — 总分 88393（LG19）

- 评分分解：属性分 69924 + 技能分 1595(固有510+买入1085) + 结余PT分 16874(总PT 8437×2) = 88393
- Pt 账目：育成攒得后结余 skill_pt=7235，hints=185(折算 1202 Pt)；终局买入 5 个技能，花费 504 Pt，加 1085 分
- 终局买入 5 个技能：

  | 技能 | 价格 | Grade | 净增分 |
  |------|------|-------|--------|
  | 打好基础 | 90 | 217 | 37 |
  | 翘尾巴 | 90 | 217 | 37 |
  | 直滑降 | 108 | 217 | 1 |
  | 俯冲 | 108 | 217 | 1 |
  | 趁势而上 | 108 | 217 | 1 |
- 对照 r8 原回放：轨迹一致（4/7 卡组因 875dd2c 上游合并+新口径小幅漂移，属预期）

### [4] speed_wisdom — 总分 98286（LF11）

- 评分分解：属性分 77142 + 技能分 944(固有510+买入434) + 结余PT分 20200(总PT 10100×2) = 98286
- Pt 账目：育成攒得后结余 skill_pt=8677，hints=219(折算 1423 Pt)；终局买入 2 个技能，花费 180 Pt，加 434 分
- 终局买入 2 个技能：

  | 技能 | 价格 | Grade | 净增分 |
  |------|------|-------|--------|
  | 打好基础 | 90 | 217 | 37 |
  | 翘尾巴 | 90 | 217 | 37 |
- 对照 r8 原回放：轨迹有漂移（4/7 卡组因 875dd2c 上游合并+新口径小幅漂移，属预期）

### [5] wisdom — 总分 87417（LG18）

- 评分分解：属性分 68060 + 技能分 1161(固有510+买入651) + 结余PT分 18196(总PT 9098×2) = 87417
- Pt 账目：育成攒得后结余 skill_pt=7850，hints=192(折算 1248 Pt)；终局买入 3 个技能，花费 288 Pt，加 651 分
- 终局买入 3 个技能：

  | 技能 | 价格 | Grade | 净增分 |
  |------|------|-------|--------|
  | 打好基础 | 90 | 217 | 37 |
  | 翘尾巴 | 90 | 217 | 37 |
  | 俯冲 | 108 | 217 | 1 |
- 对照 r8 原回放：轨迹有漂移（4/7 卡组因 875dd2c 上游合并+新口径小幅漂移，属预期）

### [6] sta0_wis2 — 总分 85846（LG15）

- 评分分解：属性分 66857 + 技能分 1161(固有510+买入651) + 结余PT分 17828(总PT 8914×2) = 85846
- Pt 账目：育成攒得后结余 skill_pt=7718，hints=184(折算 1196 Pt)；终局买入 3 个技能，花费 270 Pt，加 651 分
- 终局买入 3 个技能：

  | 技能 | 价格 | Grade | 净增分 |
  |------|------|-------|--------|
  | 英里弯道○ | 90 | 217 | 37 |
  | 打好基础 | 90 | 217 | 37 |
  | 翘尾巴 | 90 | 217 | 37 |
- 对照 r8 原回放：轨迹有漂移（4/7 卡组因 875dd2c 上游合并+新口径小幅漂移，属预期）

### [7] spd2_gut0 — 总分 91879（LF）

- 评分分解：属性分 71297 + 技能分 510(固有510+买入0) + 结余PT分 20072(总PT 10036×2) = 91879
- Pt 账目：育成攒得后结余 skill_pt=8697，hints=206(折算 1339 Pt)；终局买入 0 个技能，花费 0 Pt，加 0 分
- 终局未买入技能
- 对照 r8 原回放：轨迹有漂移（4/7 卡组因 875dd2c 上游合并+新口径小幅漂移，属预期）

---

## 三、逐回合育成过程（7 卡组全量）

每回合列出：回合号、阶段、AI 最终决定（含择优值）以及前 4 名候选择优摘要；完整候选与逐项评分见 `data/replay_buy_top1/` CSV 的 score_breakdown 列。

### [1] speed（196 个决策回合）

| 回合 | 阶段 | AI 决定 | 候选择优（前 4） |
|------|------|---------|----------------|
| 0 | Train | **智训练** | 7 |
| 1 | Train | **7** | 7 |
| 2 | RegionSelect | **地区[札幌-速,函馆-耐,东京-智]** | 10 |
| 2 | RamenSelect | **吃面/札幌-速** | 4 |
| 2 | SpecialSelect | **9** | 9 |
| 2 | Train | **7** | 7 |
| 3 | RamenSelect | **3** | 3 |
| 3 | Train | **7** | 7 |
| 4 | RamenSelect | **吃面/东京-智** | 4 |
| 4 | SpecialSelect | **8** | 8 |
| 4 | Train | **7** | 7 |
| 5 | RamenSelect | **1** | 1 |
| 5 | Train | **休息** | 7 |
| 6 | RamenSelect | **吃面/札幌-速** | 4 |
| 6 | SpecialSelect | **4** | 4 |
| 6 | Train | **根训练** | 7 |
| 7 | RamenSelect | **1** | 1 |
| 7 | Train | **智训练** | 7 |
| 8 | RamenSelect | **1** | 1 |
| 8 | Train | **7** | 7 |
| 9 | Event | **事件#5005 马娘事件5:  智20  /  20pt** | 2 |
| 9 | RamenSelect | **吃面/札幌-速** | 3 |
| 9 | SpecialSelect | **1** | 1 |
| 9 | Train | **7** | 7 |
| 10 | RamenSelect | **1** | 1 |
| 10 | Train | **根训练** | 7 |
| 10 | Event | **2** | 2 |
| 11 | Event | **事件#830305103 友人解锁:  智5 5pt 体力25 羁绊+5 干劲1 +休息心得(1回合) /  速5 智5 5pt 羁绊+5 干劲1 Hint+5 +休息心得(1回合)** | 2 |
| 11 | RamenSelect | **1** | 1 |
| 11 | Train | **1** | 1 |
| 12 | RamenSelect | **3** | 3 |
| 12 | Train | **智训练** | 8 |
| 12 | Event | **2** | 2 |
| 13 | RamenSelect | **吃面/札幌-速** | 4 |
| 13 | SpecialSelect | **1** | 1 |
| 13 | Train | **9** | 9 |
| 14 | Event | **事件#5003 马娘事件3:  力20  /  根20 ** | 2 |
| 14 | RamenSelect | **2** | 2 |
| 14 | Train | **根训练** | 9 |
| 15 | Event | **事件#5002 马娘事件2:  耐20  /  力20 ** | 2 |
| 15 | RamenSelect | **3** | 3 |
| 15 | Train | **9** | 9 |
| 16 | RamenSelect | **4** | 4 |
| 16 | Train | **休息** | 9 |
| 17 | RamenSelect | **吃面/东京-智** | 4 |
| 17 | SpecialSelect | **1** | 1 |
| 17 | Train | **智训练** | 9 |
| 18 | RamenSelect | **吃面/札幌-速** | 4 |
| 18 | SpecialSelect | **1** | 1 |
| 18 | Train | **9** | 9 |
| 19 | Event | **2** | 2 |
| 19 | RamenSelect | **1** | 1 |
| 19 | Train | **智训练** | 9 |
| 20 | RamenSelect | **吃面/札幌-速** | 4 |
| 20 | SpecialSelect | **1** | 1 |
| 20 | Train | **9** | 9 |
| 21 | RamenSelect | **1** | 1 |
| 21 | Train | **9** | 9 |
| 22 | RamenSelect | **3** | 3 |
| 22 | Train | **9** | 9 |
| 23 | RamenSelect | **4** | 4 |
| 23 | Train | **休息** | 9 |
| 23 | RegionSelect | **地区[中山-全,京都-耐根,小仓-智]** | 10 |
| 24 | Event | **事件#4009 经典年-新年:  速25  /   体力20 /  20pt** | 3 |
| 24 | RamenSelect | **吃面/京都-耐根** | 4 |
| 24 | SpecialSelect | **3** | 3 |
| 24 | Train | **耐训练** | 9 |
| 25 | RamenSelect | **1** | 1 |
| 25 | Train | **9** | 9 |
| 26 | RamenSelect | **1** | 1 |
| 26 | Train | **耐训练** | 9 |
| 27 | RamenSelect | **2** | 2 |
| 27 | Train | **9** | 9 |
| 28 | RamenSelect | **4** | 4 |
| 28 | Train | **友人出行** | 9 |
| 29 | RamenSelect | **吃面/京都-耐根** | 4 |
| 29 | SpecialSelect | **吃面/京都-耐根(替换Cx1)** | 6 |
| 29 | Train | **耐训练** | 9 |
| 30 | RamenSelect | **吃面/中山-全** | 2 |
| 30 | SpecialSelect | **3** | 3 |
| 30 | Train | **耐训练** | 9 |
| 31 | RamenSelect | **1** | 1 |
| 31 | Train | **9** | 9 |
| 32 | RamenSelect | **2** | 2 |
| 32 | Train | **友人出行** | 9 |
| 33 | RamenSelect | **4** | 4 |
| 33 | Train | **比赛** | 9 |
| 33 | Event | **2** | 2 |
| 34 | RamenSelect | **吃面/小仓-智** | 4 |
| 34 | SpecialSelect | **吃面/小仓-智(替换Bx1)** | 8 |
| 34 | Train | **智训练** | 9 |
| 35 | RamenSelect | **吃面/中山-全** | 4 |
| 35 | SpecialSelect | **3** | 3 |
| 35 | Train | **9** | 9 |
| 35 | Event | **2** | 2 |
| 36 | RamenSelect | **4** | 4 |
| 36 | Train | **1** | 1 |
| 37 | RamenSelect | **吃面/中山-全** | 4 |
| 37 | SpecialSelect | **吃面/中山-全(替换Cx2)** | 3 |
| 37 | Train | **7** | 7 |
| 38 | RamenSelect | **吃面/小仓-智** | 4 |
| 38 | SpecialSelect | **4** | 4 |
| 38 | Train | **智训练** | 7 |
| 39 | RamenSelect | **吃面/中山-全** | 2 |
| 39 | SpecialSelect | **3** | 3 |
| 39 | Train | **7** | 7 |
| 40 | RamenSelect | **吃面/中山-全** | 2 |
| 40 | SpecialSelect | **1** | 1 |
| 40 | Train | **9** | 9 |
| 41 | RamenSelect | **1** | 1 |
| 41 | Train | **休息** | 9 |
| 42 | RamenSelect | **1** | 1 |
| 42 | Train | **9** | 9 |
| 43 | RamenSelect | **1** | 1 |
| 43 | Train | **9** | 9 |
| 44 | RamenSelect | **3** | 3 |
| 44 | Train | **休息** | 9 |
| 45 | RamenSelect | **4** | 4 |
| 45 | Train | **普通出行** | 9 |
| 46 | RamenSelect | **吃面/中山-全** | 4 |
| 46 | SpecialSelect | **1** | 1 |
| 46 | Train | **9** | 9 |
| 47 | Event | **2** | 2 |
| 47 | RamenSelect | **1** | 1 |
| 47 | Train | **9** | 9 |
| 47 | RegionSelect | **地区[函馆-耐,东京-智,京都-速耐智]** | 120 |
| 48 | Event | **事件#4010 古马年-新年:   体力30 /  速8 耐8 力8 根8 智8  /  35pt** | 3 |
| 48 | RamenSelect | **4** | 4 |
| 48 | Train | **1** | 1 |
| 49 | RamenSelect | **吃面/京都-速耐智** | 4 |
| 49 | SpecialSelect | **6** | 6 |
| 49 | Train | **9** | 9 |
| 49 | Event | **2** | 2 |
| 50 | RamenSelect | **1** | 1 |
| 50 | Train | **9** | 9 |
| 51 | RamenSelect | **吃面/东京-智** | 4 |
| 51 | SpecialSelect | **4** | 4 |
| 51 | Train | **智训练** | 9 |
| 52 | RamenSelect | **1** | 1 |
| 52 | Train | **友人出行** | 9 |
| 52 | Event | **事件#830305113 友人出行3:   体力50 羁绊+5 干劲1 /  速10 力10 根10 20pt 羁绊+5 干劲1** | 2 |
| 53 | RamenSelect | **吃面/函馆-耐** | 3 |
| 53 | SpecialSelect | **1** | 1 |
| 53 | Train | **耐训练** | 9 |
| 54 | RamenSelect | **1** | 1 |
| 54 | Train | **智训练** | 9 |
| 54 | Event | **2** | 2 |
| 55 | RamenSelect | **1** | 1 |
| 55 | Train | **1** | 1 |
| 56 | RamenSelect | **4** | 4 |
| 56 | Train | **友人出行** | 9 |
| 57 | RamenSelect | **吃面/京都-速耐智** | 4 |
| 57 | SpecialSelect | **3** | 3 |
| 57 | Train | **9** | 9 |
| 58 | RamenSelect | **3** | 3 |
| 58 | Train | **友人出行** | 9 |
| 59 | RamenSelect | **3** | 3 |
| 59 | Train | **1** | 1 |
| 60 | RamenSelect | **吃面/函馆-耐** | 4 |
| 60 | SpecialSelect | **吃面/函馆-耐(替换Bx1+Cx1)** | 9 |
| 60 | Train | **耐训练** | 7 |
| 61 | RamenSelect | **吃面/东京-智** | 4 |
| 61 | SpecialSelect | **4** | 4 |
| 61 | Train | **智训练** | 7 |
| 62 | RamenSelect | **吃面/函馆-耐** | 4 |
| 62 | SpecialSelect | **4** | 4 |
| 62 | Train | **耐训练** | 7 |
| 63 | RamenSelect | **吃面/函馆-耐** | 3 |
| 63 | SpecialSelect | **1** | 1 |
| 63 | Train | **耐训练** | 7 |
| 64 | RamenSelect | **1** | 1 |
| 64 | Train | **耐训练** | 8 |
| 65 | RamenSelect | **1** | 1 |
| 65 | Train | **智训练** | 8 |
| 66 | RamenSelect | **吃面/京都-速耐智** | 4 |
| 66 | SpecialSelect | **1** | 1 |
| 66 | Train | **8** | 8 |
| 67 | RamenSelect | **1** | 1 |
| 67 | Train | **1** | 1 |
| 68 | RamenSelect | **1** | 1 |
| 68 | Train | **智训练** | 8 |
| 69 | RamenSelect | **2** | 2 |
| 69 | Train | **智训练** | 8 |
| 70 | RamenSelect | **吃面/函馆-耐** | 2 |
| 70 | SpecialSelect | **1** | 1 |
| 70 | Train | **耐训练** | 8 |
| 71 | RamenSelect | **1** | 1 |
| 71 | Train | **1** | 1 |
| 71 | SuperRamenSelect | **超级拉面选项 2** | 3 |
| 72 | Train | **7** | 7 |
| 72 | Event | **2** | 2 |
| 73 | Train | **1** | 1 |
| 74 | Train | **耐训练** | 7 |
| 75 | Train | **1** | 1 |
| 76 | Train | **耐训练** | 7 |
| 77 | Train | **1** | 1 |

### [2] stamina（199 个决策回合）

| 回合 | 阶段 | AI 决定 | 候选择优（前 4） |
|------|------|---------|----------------|
| 0 | Train | **智训练** | 7 |
| 1 | Train | **7** | 7 |
| 2 | RegionSelect | **地区[札幌-速,函馆-耐,东京-智]** | 10 |
| 2 | RamenSelect | **吃面/札幌-速** | 4 |
| 2 | SpecialSelect | **9** | 9 |
| 2 | Train | **7** | 7 |
| 3 | RamenSelect | **吃面/东京-智** | 3 |
| 3 | SpecialSelect | **1** | 1 |
| 3 | Train | **智训练** | 7 |
| 4 | RamenSelect | **1** | 1 |
| 4 | Train | **7** | 7 |
| 5 | RamenSelect | **1** | 1 |
| 5 | Train | **力训练** | 7 |
| 6 | RamenSelect | **1** | 1 |
| 6 | Train | **根训练** | 7 |
| 7 | RamenSelect | **吃面/函馆-耐** | 3 |
| 7 | SpecialSelect | **1** | 1 |
| 7 | Train | **耐训练** | 7 |
| 8 | RamenSelect | **1** | 1 |
| 8 | Train | **休息** | 7 |
| 9 | Event | **事件#5005 马娘事件5:  智20  /  20pt** | 2 |
| 9 | RamenSelect | **1** | 1 |
| 9 | Train | **7** | 7 |
| 10 | RamenSelect | **1** | 1 |
| 10 | Train | **休息** | 7 |
| 11 | Event | **事件#830305103 友人解锁:  智5 5pt 体力25 羁绊+5 干劲1 +休息心得(1回合) /  速5 智5 5pt 羁绊+5 干劲1 Hint+5 +休息心得(1回合)** | 2 |
| 11 | RamenSelect | **3** | 3 |
| 11 | Train | **1** | 1 |
| 12 | RamenSelect | **吃面/东京-智** | 4 |
| 12 | SpecialSelect | **1** | 1 |
| 12 | Train | **智训练** | 8 |
| 12 | Event | **2** | 2 |
| 13 | RamenSelect | **1** | 1 |
| 13 | Train | **9** | 9 |
| 14 | Event | **事件#5003 马娘事件3:  力20  /  根20 ** | 2 |
| 14 | RamenSelect | **2** | 2 |
| 14 | Train | **耐训练** | 9 |
| 15 | Event | **2** | 2 |
| 15 | RamenSelect | **吃面/札幌-速** | 3 |
| 15 | SpecialSelect | **1** | 1 |
| 15 | Train | **9** | 9 |
| 16 | RamenSelect | **1** | 1 |
| 16 | Train | **耐训练** | 9 |
| 17 | RamenSelect | **吃面/东京-智** | 4 |
| 17 | SpecialSelect | **1** | 1 |
| 17 | Train | **智训练** | 9 |
| 18 | RamenSelect | **1** | 1 |
| 18 | Train | **根训练** | 9 |
| 19 | Event | **2** | 2 |
| 19 | RamenSelect | **2** | 2 |
| 19 | Train | **耐训练** | 9 |
| 20 | RamenSelect | **3** | 3 |
| 20 | Train | **休息** | 9 |
| 21 | RamenSelect | **吃面/札幌-速** | 3 |
| 21 | SpecialSelect | **1** | 1 |
| 21 | Train | **9** | 9 |
| 22 | RamenSelect | **吃面/函馆-耐** | 3 |
| 22 | SpecialSelect | **1** | 1 |
| 22 | Train | **耐训练** | 9 |
| 22 | Event | **2** | 2 |
| 23 | RamenSelect | **1** | 1 |
| 23 | Train | **比赛** | 9 |
| 23 | Event | **2** | 2 |
| 23 | RegionSelect | **地区[中山-全,京都-耐根,小仓-智]** | 10 |
| 24 | Event | **事件#4009 经典年-新年:  速25  /   体力20 /  20pt** | 3 |
| 24 | RamenSelect | **吃面/京都-耐根** | 4 |
| 24 | SpecialSelect | **3** | 3 |
| 24 | Train | **耐训练** | 9 |
| 25 | RamenSelect | **1** | 1 |
| 25 | Train | **友人出行** | 9 |
| 26 | RamenSelect | **吃面/中山-全** | 3 |
| 26 | SpecialSelect | **1** | 1 |
| 26 | Train | **耐训练** | 9 |
| 27 | RamenSelect | **1** | 1 |
| 27 | Train | **9** | 9 |
| 28 | RamenSelect | **2** | 2 |
| 28 | Train | **友人出行** | 9 |
| 29 | RamenSelect | **吃面/京都-耐根** | 4 |
| 29 | SpecialSelect | **3** | 3 |
| 29 | Train | **耐训练** | 9 |
| 30 | RamenSelect | **吃面/中山-全** | 2 |
| 30 | SpecialSelect | **1** | 1 |
| 30 | Train | **耐训练** | 9 |
| 31 | RamenSelect | **1** | 1 |
| 31 | Train | **9** | 9 |
| 32 | RamenSelect | **1** | 1 |
| 32 | Train | **智训练** | 9 |
| 32 | Event | **2** | 2 |
| 33 | RamenSelect | **1** | 1 |
| 33 | Train | **比赛** | 9 |
| 33 | Event | **2** | 2 |
| 34 | RamenSelect | **3** | 3 |
| 34 | Train | **休息** | 9 |
| 35 | RamenSelect | **吃面/京都-耐根** | 4 |
| 35 | SpecialSelect | **1** | 1 |
| 35 | Train | **耐训练** | 9 |
| 35 | Event | **2** | 2 |
| 36 | RamenSelect | **4** | 4 |
| 36 | Train | **1** | 1 |
| 37 | RamenSelect | **吃面/京都-耐根** | 4 |
| 37 | SpecialSelect | **3** | 3 |
| 37 | Train | **耐训练** | 7 |
| 38 | RamenSelect | **吃面/中山-全** | 4 |
| 38 | SpecialSelect | **3** | 3 |
| 38 | Train | **耐训练** | 7 |
| 39 | RamenSelect | **吃面/中山-全** | 4 |
| 39 | SpecialSelect | **1** | 1 |
| 39 | Train | **7** | 7 |
| 40 | RamenSelect | **3** | 3 |
| 40 | Train | **9** | 9 |
| 41 | RamenSelect | **3** | 3 |
| 41 | Train | **休息** | 9 |
| 42 | RamenSelect | **吃面/中山-全** | 4 |
| 42 | SpecialSelect | **1** | 1 |
| 42 | Train | **9** | 9 |
| 43 | RamenSelect | **2** | 2 |
| 43 | Train | **9** | 9 |
| 44 | RamenSelect | **2** | 2 |
| 44 | Train | **休息** | 9 |
| 45 | RamenSelect | **3** | 3 |
| 45 | Train | **普通出行** | 9 |
| 46 | RamenSelect | **3** | 3 |
| 46 | Train | **9** | 9 |
| 47 | Event | **事件#5001 马娘事件1:  速20  /  耐20 ** | 2 |
| 47 | RamenSelect | **吃面/中山-全** | 4 |
| 47 | SpecialSelect | **1** | 1 |
| 47 | Train | **9** | 9 |
| 47 | RegionSelect | **地区[东京-智,中山-速力智,京都-速耐智]** | 120 |
| 48 | Event | **事件#4010 古马年-新年:   体力30 /  速8 耐8 力8 根8 智8  /  35pt** | 3 |
| 48 | RamenSelect | **4** | 4 |
| 48 | Train | **1** | 1 |
| 49 | RamenSelect | **吃面/京都-速耐智** | 4 |
| 49 | SpecialSelect | **6** | 6 |
| 49 | Train | **耐训练** | 9 |
| 50 | RamenSelect | **3** | 3 |
| 50 | Train | **友人出行** | 9 |
| 50 | Event | **事件#830305113 友人出行3:   体力50 羁绊+5 干劲1 /  速10 力10 根10 20pt 羁绊+5 干劲1** | 2 |
| 51 | RamenSelect | **吃面/东京-智** | 4 |
| 51 | SpecialSelect | **吃面/东京-智(替换Bx1+Cx1)** | 8 |
| 51 | Train | **智训练** | 9 |
| 52 | RamenSelect | **3** | 3 |
| 52 | Train | **友人出行** | 9 |
| 53 | RamenSelect | **4** | 4 |
| 53 | Train | **友人出行** | 9 |
| 54 | RamenSelect | **吃面/东京-智** | 4 |
| 54 | SpecialSelect | **吃面/东京-智(替换Cx2)** | 4 |
| 54 | Train | **智训练** | 8 |
| 54 | Event | **2** | 2 |
| 55 | RamenSelect | **4** | 4 |
| 55 | Train | **1** | 1 |
| 56 | RamenSelect | **吃面/东京-智** | 4 |
| 56 | SpecialSelect | **8** | 8 |
| 56 | Train | **智训练** | 8 |
| 57 | RamenSelect | **1** | 1 |
| 57 | Train | **8** | 8 |
| 57 | Event | **2** | 2 |
| 58 | RamenSelect | **吃面/中山-速力智** | 4 |
| 58 | SpecialSelect | **1** | 1 |
| 58 | Train | **8** | 8 |
| 59 | RamenSelect | **1** | 1 |
| 59 | Train | **1** | 1 |
| 60 | RamenSelect | **吃面/京都-速耐智** | 4 |
| 60 | SpecialSelect | **6** | 6 |
| 60 | Train | **耐训练** | 7 |
| 61 | RamenSelect | **吃面/东京-智** | 3 |
| 61 | SpecialSelect | **1** | 1 |
| 61 | Train | **智训练** | 7 |
| 62 | RamenSelect | **3** | 3 |
| 62 | Train | **耐训练** | 7 |
| 63 | RamenSelect | **吃面/京都-速耐智** | 4 |
| 63 | SpecialSelect | **3** | 3 |
| 63 | Train | **耐训练** | 7 |
| 64 | RamenSelect | **3** | 3 |
| 64 | Train | **休息** | 8 |
| 65 | RamenSelect | **吃面/东京-智** | 3 |
| 65 | SpecialSelect | **1** | 1 |
| 65 | Train | **智训练** | 8 |
| 66 | RamenSelect | **1** | 1 |
| 66 | Train | **8** | 8 |
| 67 | RamenSelect | **1** | 1 |
| 67 | Train | **1** | 1 |
| 68 | RamenSelect | **吃面/东京-智** | 3 |
| 68 | SpecialSelect | **1** | 1 |
| 68 | Train | **智训练** | 8 |
| 69 | RamenSelect | **1** | 1 |
| 69 | Train | **智训练** | 8 |
| 70 | RamenSelect | **1** | 1 |
| 70 | Train | **8** | 8 |
| 70 | Event | **2** | 2 |
| 71 | RamenSelect | **2** | 2 |
| 71 | Train | **1** | 1 |
| 71 | SuperRamenSelect | **超级拉面选项 2** | 3 |
| 72 | Train | **7** | 7 |
| 72 | Event | **2** | 2 |
| 73 | Train | **1** | 1 |
| 74 | Train | **智训练** | 7 |
| 75 | Train | **1** | 1 |
| 76 | Train | **7** | 7 |
| 77 | Train | **1** | 1 |

### [3] power_wisdom（203 个决策回合）

| 回合 | 阶段 | AI 决定 | 候选择优（前 4） |
|------|------|---------|----------------|
| 0 | Train | **智训练** | 7 |
| 1 | Train | **力训练** | 7 |
| 2 | RegionSelect | **地区[札幌-速,新潟-力,东京-智]** | 10 |
| 2 | RamenSelect | **吃面/东京-智** | 4 |
| 2 | SpecialSelect | **4** | 4 |
| 2 | Train | **智训练** | 7 |
| 3 | Event | **事件#830305103 友人解锁:  智5 5pt 体力25 羁绊+5 干劲1 +休息心得(1回合) /  速5 智5 5pt 羁绊+5 干劲1 Hint+5 +休息心得(1回合)** | 2 |
| 3 | RamenSelect | **1** | 1 |
| 3 | Train | **智训练** | 8 |
| 4 | RamenSelect | **3** | 3 |
| 4 | Train | **耐训练** | 8 |
| 5 | Event | **事件#5004 马娘事件4:  根20  /  智20 ** | 2 |
| 5 | RamenSelect | **吃面/新潟-力** | 3 |
| 5 | SpecialSelect | **4** | 4 |
| 5 | Train | **力训练** | 8 |
| 6 | RamenSelect | **1** | 1 |
| 6 | Train | **智训练** | 8 |
| 7 | Event | **2** | 2 |
| 7 | RamenSelect | **吃面/东京-智** | 2 |
| 7 | SpecialSelect | **1** | 1 |
| 7 | Train | **智训练** | 8 |
| 8 | RamenSelect | **1** | 1 |
| 8 | Train | **力训练** | 8 |
| 9 | Event | **2** | 2 |
| 9 | RamenSelect | **2** | 2 |
| 9 | Train | **根训练** | 8 |
| 10 | Event | **2** | 2 |
| 10 | RamenSelect | **3** | 3 |
| 10 | Train | **根训练** | 8 |
| 10 | Event | **2** | 2 |
| 11 | RamenSelect | **3** | 3 |
| 11 | Train | **1** | 1 |
| 12 | RamenSelect | **吃面/东京-智** | 4 |
| 12 | SpecialSelect | **1** | 1 |
| 12 | Train | **智训练** | 8 |
| 12 | Event | **2** | 2 |
| 13 | RamenSelect | **1** | 1 |
| 13 | Train | **智训练** | 9 |
| 14 | Event | **事件#5005 马娘事件5:  智20  /  20pt** | 2 |
| 14 | RamenSelect | **吃面/新潟-力** | 3 |
| 14 | SpecialSelect | **1** | 1 |
| 14 | Train | **力训练** | 9 |
| 15 | RamenSelect | **1** | 1 |
| 15 | Train | **力训练** | 9 |
| 16 | RamenSelect | **2** | 2 |
| 16 | Train | **比赛** | 9 |
| 16 | Event | **2** | 2 |
| 17 | RamenSelect | **2** | 2 |
| 17 | Train | **休息** | 9 |
| 18 | RamenSelect | **吃面/札幌-速** | 3 |
| 18 | SpecialSelect | **1** | 1 |
| 18 | Train | **9** | 9 |
| 19 | RamenSelect | **1** | 1 |
| 19 | Train | **智训练** | 9 |
| 20 | RamenSelect | **吃面/札幌-速** | 2 |
| 20 | SpecialSelect | **1** | 1 |
| 20 | Train | **9** | 9 |
| 21 | RamenSelect | **1** | 1 |
| 21 | Train | **智训练** | 9 |
| 22 | RamenSelect | **1** | 1 |
| 22 | Train | **力训练** | 9 |
| 22 | Event | **2** | 2 |
| 23 | RamenSelect | **2** | 2 |
| 23 | Train | **智训练** | 9 |
| 23 | RegionSelect | **地区[中京-力根,阪神-耐力,小仓-智]** | 10 |
| 24 | Event | **事件#4009 经典年-新年:  速25  /   体力20 /  20pt** | 3 |
| 24 | RamenSelect | **吃面/小仓-智** | 4 |
| 24 | SpecialSelect | **4** | 4 |
| 24 | Train | **智训练** | 9 |
| 25 | RamenSelect | **2** | 2 |
| 25 | Train | **友人出行** | 9 |
| 26 | RamenSelect | **吃面/阪神-耐力** | 4 |
| 26 | SpecialSelect | **9** | 9 |
| 26 | Train | **力训练** | 9 |
| 27 | RamenSelect | **1** | 1 |
| 27 | Train | **力训练** | 9 |
| 28 | RamenSelect | **吃面/阪神-耐力** | 4 |
| 28 | SpecialSelect | **4** | 4 |
| 28 | Train | **力训练** | 9 |
| 29 | RamenSelect | **1** | 1 |
| 29 | Train | **友人出行** | 9 |
| 30 | RamenSelect | **吃面/小仓-智** | 3 |
| 30 | SpecialSelect | **1** | 1 |
| 30 | Train | **智训练** | 9 |
| 30 | Event | **2** | 2 |
| 31 | RamenSelect | **1** | 1 |
| 31 | Train | **智训练** | 9 |
| 32 | RamenSelect | **吃面/小仓-智** | 4 |
| 32 | SpecialSelect | **4** | 4 |
| 32 | Train | **智训练** | 9 |
| 32 | Event | **2** | 2 |
| 33 | RamenSelect | **1** | 1 |
| 33 | Train | **比赛** | 9 |
| 33 | Event | **2** | 2 |
| 34 | RamenSelect | **1** | 1 |
| 34 | Train | **智训练** | 9 |
| 35 | RamenSelect | **吃面/中京-力根** | 4 |
| 35 | SpecialSelect | **1** | 1 |
| 35 | Train | **力训练** | 9 |
| 35 | Event | **2** | 2 |
| 36 | RamenSelect | **2** | 2 |
| 36 | Train | **1** | 1 |
| 37 | RamenSelect | **2** | 2 |
| 37 | Train | **智训练** | 7 |
| 38 | RamenSelect | **3** | 3 |
| 38 | Train | **智训练** | 7 |
| 39 | RamenSelect | **3** | 3 |
| 39 | Train | **智训练** | 7 |
| 40 | RamenSelect | **吃面/阪神-耐力** | 3 |
| 40 | SpecialSelect | **3** | 3 |
| 40 | Train | **力训练** | 9 |
| 41 | RamenSelect | **吃面/阪神-耐力** | 4 |
| 41 | SpecialSelect | **吃面/阪神-耐力(替换Bx1)** | 9 |
| 41 | Train | **力训练** | 9 |
| 42 | RamenSelect | **吃面/小仓-智** | 4 |
| 42 | SpecialSelect | **4** | 4 |
| 42 | Train | **智训练** | 9 |
| 43 | RamenSelect | **1** | 1 |
| 43 | Train | **力训练** | 9 |
| 44 | RamenSelect | **3** | 3 |
| 44 | Train | **比赛** | 9 |
| 44 | Event | **2** | 2 |
| 45 | RamenSelect | **3** | 3 |
| 45 | Train | **休息** | 9 |
| 46 | RamenSelect | **4** | 4 |
| 46 | Train | **普通出行** | 9 |
| 47 | RamenSelect | **吃面/小仓-智** | 4 |
| 47 | SpecialSelect | **1** | 1 |
| 47 | Train | **智训练** | 9 |
| 47 | RegionSelect | **地区[札幌-速,新潟-力,东京-智]** | 120 |
| 48 | Event | **事件#4010 古马年-新年:   体力30 /  速8 耐8 力8 根8 智8  /  35pt** | 3 |
| 48 | RamenSelect | **4** | 4 |
| 48 | Train | **1** | 1 |
| 49 | RamenSelect | **吃面/新潟-力** | 4 |
| 49 | SpecialSelect | **4** | 4 |
| 49 | Train | **力训练** | 9 |
| 50 | RamenSelect | **3** | 3 |
| 50 | Train | **友人出行** | 9 |
| 50 | Event | **事件#830305113 友人出行3:   体力50 羁绊+5 干劲1 /  速10 力10 根10 20pt 羁绊+5 干劲1** | 2 |
| 51 | RamenSelect | **吃面/东京-智** | 4 |
| 51 | SpecialSelect | **吃面/东京-智(替换Cx1)** | 8 |
| 51 | Train | **智训练** | 9 |
| 52 | RamenSelect | **吃面/东京-智** | 4 |
| 52 | SpecialSelect | **1** | 1 |
| 52 | Train | **智训练** | 9 |
| 53 | RamenSelect | **1** | 1 |
| 53 | Train | **智训练** | 9 |
| 54 | RamenSelect | **1** | 1 |
| 54 | Train | **智训练** | 9 |
| 54 | Event | **2** | 2 |
| 55 | RamenSelect | **3** | 3 |
| 55 | Train | **1** | 1 |
| 56 | RamenSelect | **吃面/东京-智** | 3 |
| 56 | SpecialSelect | **1** | 1 |
| 56 | Train | **智训练** | 9 |
| 57 | RamenSelect | **2** | 2 |
| 57 | Train | **力训练** | 9 |
| 57 | Event | **2** | 2 |
| 58 | RamenSelect | **2** | 2 |
| 58 | Train | **友人出行** | 9 |
| 59 | RamenSelect | **4** | 4 |
| 59 | Train | **1** | 1 |
| 60 | RamenSelect | **吃面/东京-智** | 4 |
| 60 | SpecialSelect | **吃面/东京-智(替换Cx1)** | 8 |
| 60 | Train | **智训练** | 7 |
| 61 | RamenSelect | **吃面/新潟-力** | 4 |
| 61 | SpecialSelect | **吃面/新潟-力(替换Ax1)** | 8 |
| 61 | Train | **力训练** | 7 |
| 62 | RamenSelect | **吃面/东京-智** | 4 |
| 62 | SpecialSelect | **吃面/东京-智(替换Cx2)** | 4 |
| 62 | Train | **智训练** | 7 |
| 63 | RamenSelect | **吃面/新潟-力** | 4 |
| 63 | SpecialSelect | **4** | 4 |
| 63 | Train | **力训练** | 7 |
| 64 | RamenSelect | **4** | 4 |
| 64 | Train | **友人出行** | 9 |
| 65 | RamenSelect | **吃面/新潟-力** | 4 |
| 65 | SpecialSelect | **1** | 1 |
| 65 | Train | **力训练** | 8 |
| 66 | RamenSelect | **吃面/新潟-力** | 4 |
| 66 | SpecialSelect | **1** | 1 |
| 66 | Train | **力训练** | 8 |
| 67 | RamenSelect | **1** | 1 |
| 67 | Train | **1** | 1 |
| 68 | RamenSelect | **1** | 1 |
| 68 | Train | **比赛** | 8 |
| 68 | Event | **2** | 2 |
| 69 | RamenSelect | **1** | 1 |
| 69 | Train | **智训练** | 8 |
| 69 | Event | **2** | 2 |
| 70 | RamenSelect | **2** | 2 |
| 70 | Train | **比赛** | 8 |
| 70 | Event | **2** | 2 |
| 71 | RamenSelect | **4** | 4 |
| 71 | Train | **1** | 1 |
| 71 | SuperRamenSelect | **超级拉面选项 2** | 3 |
| 72 | Train | **智训练** | 7 |
| 72 | Event | **2** | 2 |
| 73 | Train | **1** | 1 |
| 74 | Train | **智训练** | 7 |
| 75 | Train | **1** | 1 |
| 76 | Train | **智训练** | 7 |
| 77 | Train | **1** | 1 |

### [4] speed_wisdom（197 个决策回合）

| 回合 | 阶段 | AI 决定 | 候选择优（前 4） |
|------|------|---------|----------------|
| 0 | Train | **智训练** | 7 |
| 1 | Train | **7** | 7 |
| 2 | RegionSelect | **地区[札幌-速,函馆-耐,东京-智]** | 10 |
| 2 | RamenSelect | **吃面/札幌-速** | 4 |
| 2 | SpecialSelect | **9** | 9 |
| 2 | Train | **7** | 7 |
| 3 | RamenSelect | **吃面/东京-智** | 3 |
| 3 | SpecialSelect | **1** | 1 |
| 3 | Train | **智训练** | 7 |
| 4 | RamenSelect | **1** | 1 |
| 4 | Train | **7** | 7 |
| 5 | RamenSelect | **1** | 1 |
| 5 | Train | **力训练** | 7 |
| 6 | RamenSelect | **1** | 1 |
| 6 | Train | **智训练** | 7 |
| 7 | Event | **2** | 2 |
| 7 | RamenSelect | **吃面/函馆-耐** | 4 |
| 7 | SpecialSelect | **1** | 1 |
| 7 | Train | **耐训练** | 7 |
| 8 | RamenSelect | **1** | 1 |
| 8 | Train | **休息** | 7 |
| 9 | Event | **事件#5004 马娘事件4:  根20  /  智20 ** | 2 |
| 9 | RamenSelect | **1** | 1 |
| 9 | Train | **根训练** | 7 |
| 10 | RamenSelect | **1** | 1 |
| 10 | Train | **根训练** | 7 |
| 10 | Event | **2** | 2 |
| 11 | Event | **事件#830305103 友人解锁:  智5 5pt 体力25 羁绊+5 干劲1 +休息心得(1回合) /  速5 智5 5pt 羁绊+5 干劲1 Hint+5 +休息心得(1回合)** | 2 |
| 11 | RamenSelect | **2** | 2 |
| 11 | Train | **1** | 1 |
| 12 | RamenSelect | **吃面/东京-智** | 2 |
| 12 | SpecialSelect | **1** | 1 |
| 12 | Train | **智训练** | 8 |
| 12 | Event | **2** | 2 |
| 13 | RamenSelect | **1** | 1 |
| 13 | Train | **智训练** | 9 |
| 14 | Event | **2** | 2 |
| 14 | RamenSelect | **吃面/函馆-耐** | 3 |
| 14 | SpecialSelect | **1** | 1 |
| 14 | Train | **耐训练** | 9 |
| 15 | Event | **2** | 2 |
| 15 | RamenSelect | **1** | 1 |
| 15 | Train | **9** | 9 |
| 16 | RamenSelect | **1** | 1 |
| 16 | Train | **比赛** | 9 |
| 16 | Event | **2** | 2 |
| 17 | RamenSelect | **3** | 3 |
| 17 | Train | **智训练** | 9 |
| 18 | RamenSelect | **吃面/札幌-速** | 4 |
| 18 | SpecialSelect | **1** | 1 |
| 18 | Train | **9** | 9 |
| 19 | Event | **事件#5005 马娘事件5:  智20  /  20pt** | 2 |
| 19 | RamenSelect | **1** | 1 |
| 19 | Train | **智训练** | 9 |
| 20 | RamenSelect | **2** | 2 |
| 20 | Train | **9** | 9 |
| 21 | RamenSelect | **4** | 4 |
| 21 | Train | **休息** | 9 |
| 22 | RamenSelect | **吃面/函馆-耐** | 4 |
| 22 | SpecialSelect | **1** | 1 |
| 22 | Train | **耐训练** | 9 |
| 23 | RamenSelect | **1** | 1 |
| 23 | Train | **智训练** | 9 |
| 23 | RegionSelect | **地区[中山-全,京都-耐根,阪神-耐力]** | 10 |
| 24 | Event | **事件#4009 经典年-新年:  速25  /   体力20 /  20pt** | 3 |
| 24 | RamenSelect | **吃面/阪神-耐力** | 4 |
| 24 | SpecialSelect | **9** | 9 |
| 24 | Train | **耐训练** | 9 |
| 25 | RamenSelect | **2** | 2 |
| 25 | Train | **9** | 9 |
| 26 | RamenSelect | **吃面/中山-全** | 4 |
| 26 | SpecialSelect | **1** | 1 |
| 26 | Train | **智训练** | 9 |
| 27 | RamenSelect | **1** | 1 |
| 27 | Train | **9** | 9 |
| 28 | RamenSelect | **1** | 1 |
| 28 | Train | **9** | 9 |
| 29 | RamenSelect | **3** | 3 |
| 29 | Train | **友人出行** | 9 |
| 30 | RamenSelect | **吃面/京都-耐根** | 4 |
| 30 | SpecialSelect | **6** | 6 |
| 30 | Train | **耐训练** | 9 |
| 31 | RamenSelect | **吃面/中山-全** | 4 |
| 31 | SpecialSelect | **3** | 3 |
| 31 | Train | **9** | 9 |
| 32 | RamenSelect | **1** | 1 |
| 32 | Train | **智训练** | 9 |
| 32 | Event | **2** | 2 |
| 33 | RamenSelect | **3** | 3 |
| 33 | Train | **友人出行** | 9 |
| 34 | RamenSelect | **吃面/中山-全** | 4 |
| 34 | SpecialSelect | **1** | 1 |
| 34 | Train | **智训练** | 9 |
| 35 | RamenSelect | **吃面/京都-耐根** | 3 |
| 35 | SpecialSelect | **1** | 1 |
| 35 | Train | **耐训练** | 9 |
| 35 | Event | **2** | 2 |
| 36 | RamenSelect | **3** | 3 |
| 36 | Train | **1** | 1 |
| 37 | RamenSelect | **吃面/阪神-耐力** | 4 |
| 37 | SpecialSelect | **9** | 9 |
| 37 | Train | **耐训练** | 7 |
| 38 | RamenSelect | **1** | 1 |
| 38 | Train | **智训练** | 7 |
| 39 | RamenSelect | **1** | 1 |
| 39 | Train | **7** | 7 |
| 40 | RamenSelect | **吃面/中山-全** | 2 |
| 40 | SpecialSelect | **1** | 1 |
| 40 | Train | **9** | 9 |
| 41 | RamenSelect | **1** | 1 |
| 41 | Train | **耐训练** | 9 |
| 42 | RamenSelect | **3** | 3 |
| 42 | Train | **9** | 9 |
| 43 | RamenSelect | **4** | 4 |
| 43 | Train | **休息** | 9 |
| 44 | RamenSelect | **4** | 4 |
| 44 | Train | **比赛** | 9 |
| 44 | Event | **2** | 2 |
| 45 | RamenSelect | **4** | 4 |
| 45 | Train | **普通出行** | 9 |
| 46 | RamenSelect | **吃面/中山-全** | 4 |
| 46 | SpecialSelect | **6** | 6 |
| 46 | Train | **9** | 9 |
| 47 | RamenSelect | **4** | 4 |
| 47 | Train | **休息** | 9 |
| 47 | RegionSelect | **地区[函馆-耐,京都-速耐智,阪神-速耐力]** | 120 |
| 48 | Event | **事件#4010 古马年-新年:   体力30 /  速8 耐8 力8 根8 智8  /  35pt** | 3 |
| 48 | RamenSelect | **4** | 4 |
| 48 | Train | **1** | 1 |
| 49 | RamenSelect | **吃面/函馆-耐** | 4 |
| 49 | SpecialSelect | **吃面/函馆-耐(替换Cx1)** | 9 |
| 49 | Train | **耐训练** | 9 |
| 50 | RamenSelect | **吃面/阪神-速耐力** | 4 |
| 50 | SpecialSelect | **4** | 4 |
| 50 | Train | **9** | 9 |
| 51 | RamenSelect | **吃面/京都-速耐智** | 4 |
| 51 | SpecialSelect | **1** | 1 |
| 51 | Train | **智训练** | 9 |
| 52 | RamenSelect | **1** | 1 |
| 52 | Train | **友人出行** | 9 |
| 52 | Event | **事件#830305113 友人出行3:   体力50 羁绊+5 干劲1 /  速10 力10 根10 20pt 羁绊+5 干劲1** | 2 |
| 53 | RamenSelect | **3** | 3 |
| 53 | Train | **智训练** | 9 |
| 54 | RamenSelect | **吃面/京都-速耐智** | 4 |
| 54 | SpecialSelect | **1** | 1 |
| 54 | Train | **智训练** | 9 |
| 54 | Event | **2** | 2 |
| 55 | RamenSelect | **1** | 1 |
| 55 | Train | **1** | 1 |
| 56 | RamenSelect | **1** | 1 |
| 56 | Train | **友人出行** | 9 |
| 57 | RamenSelect | **吃面/阪神-速耐力** | 4 |
| 57 | SpecialSelect | **9** | 9 |
| 57 | Train | **9** | 9 |
| 58 | RamenSelect | **吃面/阪神-速耐力** | 2 |
| 58 | SpecialSelect | **1** | 1 |
| 58 | Train | **9** | 9 |
| 59 | RamenSelect | **1** | 1 |
| 59 | Train | **1** | 1 |
| 60 | RamenSelect | **吃面/函馆-耐** | 4 |
| 60 | SpecialSelect | **4** | 4 |
| 60 | Train | **耐训练** | 7 |
| 61 | RamenSelect | **3** | 3 |
| 61 | Train | **智训练** | 7 |
| 62 | RamenSelect | **吃面/函馆-耐** | 4 |
| 62 | SpecialSelect | **9** | 9 |
| 62 | Train | **耐训练** | 7 |
| 63 | RamenSelect | **吃面/函馆-耐** | 3 |
| 63 | SpecialSelect | **1** | 1 |
| 63 | Train | **耐训练** | 7 |
| 64 | RamenSelect | **3** | 3 |
| 64 | Train | **友人出行** | 9 |
| 65 | RamenSelect | **3** | 3 |
| 65 | Train | **智训练** | 8 |
| 66 | RamenSelect | **吃面/京都-速耐智** | 4 |
| 66 | SpecialSelect | **3** | 3 |
| 66 | Train | **智训练** | 8 |
| 67 | RamenSelect | **2** | 2 |
| 67 | Train | **1** | 1 |
| 68 | RamenSelect | **吃面/函馆-耐** | 4 |
| 68 | SpecialSelect | **4** | 4 |
| 68 | Train | **耐训练** | 8 |
| 69 | RamenSelect | **1** | 1 |
| 69 | Train | **智训练** | 8 |
| 70 | RamenSelect | **吃面/阪神-速耐力** | 3 |
| 70 | SpecialSelect | **4** | 4 |
| 70 | Train | **8** | 8 |
| 71 | RamenSelect | **1** | 1 |
| 71 | Train | **1** | 1 |
| 71 | SuperRamenSelect | **超级拉面选项 2** | 3 |
| 72 | Train | **7** | 7 |
| 72 | Event | **2** | 2 |
| 73 | Train | **1** | 1 |
| 74 | Train | **智训练** | 7 |
| 75 | Train | **1** | 1 |
| 76 | Train | **耐训练** | 7 |
| 77 | Train | **1** | 1 |

### [5] wisdom（204 个决策回合）

| 回合 | 阶段 | AI 决定 | 候选择优（前 4） |
|------|------|---------|----------------|
| 0 | Train | **智训练** | 7 |
| 1 | Train | **智训练** | 7 |
| 2 | RegionSelect | **地区[札幌-速,函馆-耐,东京-智]** | 10 |
| 2 | RamenSelect | **吃面/札幌-速** | 4 |
| 2 | SpecialSelect | **9** | 9 |
| 2 | Train | **7** | 7 |
| 3 | RamenSelect | **吃面/东京-智** | 3 |
| 3 | SpecialSelect | **1** | 1 |
| 3 | Train | **智训练** | 7 |
| 4 | RamenSelect | **1** | 1 |
| 4 | Train | **耐训练** | 7 |
| 5 | Event | **事件#5004 马娘事件4:  根20  /  智20 ** | 2 |
| 5 | RamenSelect | **1** | 1 |
| 5 | Train | **力训练** | 7 |
| 6 | Event | **事件#830305103 友人解锁:  智5 5pt 体力25 羁绊+5 干劲1 +休息心得(1回合) /  速5 智5 5pt 羁绊+5 干劲1 Hint+5 +休息心得(1回合)** | 2 |
| 6 | RamenSelect | **1** | 1 |
| 6 | Train | **智训练** | 8 |
| 7 | RamenSelect | **吃面/东京-智** | 2 |
| 7 | SpecialSelect | **1** | 1 |
| 7 | Train | **智训练** | 8 |
| 8 | RamenSelect | **1** | 1 |
| 8 | Train | **智训练** | 8 |
| 8 | Event | **2** | 2 |
| 9 | Event | **事件#5005 马娘事件5:  智20  /  20pt** | 2 |
| 9 | RamenSelect | **吃面/札幌-速** | 2 |
| 9 | SpecialSelect | **1** | 1 |
| 9 | Train | **8** | 8 |
| 10 | RamenSelect | **1** | 1 |
| 10 | Train | **智训练** | 8 |
| 10 | Event | **2** | 2 |
| 11 | RamenSelect | **1** | 1 |
| 11 | Train | **1** | 1 |
| 12 | RamenSelect | **3** | 3 |
| 12 | Train | **智训练** | 8 |
| 12 | Event | **2** | 2 |
| 13 | RamenSelect | **吃面/札幌-速** | 3 |
| 13 | SpecialSelect | **1** | 1 |
| 13 | Train | **9** | 9 |
| 14 | Event | **2** | 2 |
| 14 | RamenSelect | **1** | 1 |
| 14 | Train | **耐训练** | 9 |
| 15 | RamenSelect | **3** | 3 |
| 15 | Train | **9** | 9 |
| 16 | RamenSelect | **4** | 4 |
| 16 | Train | **比赛** | 9 |
| 16 | Event | **2** | 2 |
| 17 | RamenSelect | **吃面/东京-智** | 4 |
| 17 | SpecialSelect | **1** | 1 |
| 17 | Train | **智训练** | 9 |
| 18 | RamenSelect | **吃面/札幌-速** | 3 |
| 18 | SpecialSelect | **1** | 1 |
| 18 | Train | **9** | 9 |
| 19 | Event | **2** | 2 |
| 19 | RamenSelect | **1** | 1 |
| 19 | Train | **智训练** | 9 |
| 20 | RamenSelect | **1** | 1 |
| 20 | Train | **耐训练** | 9 |
| 21 | RamenSelect | **吃面/东京-智** | 4 |
| 21 | SpecialSelect | **1** | 1 |
| 21 | Train | **智训练** | 9 |
| 22 | RamenSelect | **吃面/札幌-速** | 2 |
| 22 | SpecialSelect | **1** | 1 |
| 22 | Train | **9** | 9 |
| 23 | RamenSelect | **1** | 1 |
| 23 | Train | **休息** | 9 |
| 23 | RegionSelect | **地区[中山-全,京都-耐根,阪神-耐力]** | 10 |
| 24 | Event | **事件#4009 经典年-新年:  速25  /   体力20 /  20pt** | 3 |
| 24 | RamenSelect | **吃面/中山-全** | 4 |
| 24 | SpecialSelect | **3** | 3 |
| 24 | Train | **智训练** | 9 |
| 25 | RamenSelect | **1** | 1 |
| 25 | Train | **9** | 9 |
| 26 | RamenSelect | **3** | 3 |
| 26 | Train | **智训练** | 9 |
| 27 | RamenSelect | **3** | 3 |
| 27 | Train | **9** | 9 |
| 28 | RamenSelect | **4** | 4 |
| 28 | Train | **友人出行** | 9 |
| 29 | RamenSelect | **吃面/阪神-耐力** | 4 |
| 29 | SpecialSelect | **吃面/阪神-耐力(替换Cx1)** | 9 |
| 29 | Train | **耐训练** | 9 |
| 30 | RamenSelect | **吃面/中山-全** | 4 |
| 30 | SpecialSelect | **3** | 3 |
| 30 | Train | **智训练** | 9 |
| 31 | RamenSelect | **1** | 1 |
| 31 | Train | **智训练** | 9 |
| 32 | RamenSelect | **3** | 3 |
| 32 | Train | **智训练** | 9 |
| 32 | Event | **2** | 2 |
| 33 | RamenSelect | **3** | 3 |
| 33 | Train | **友人出行** | 9 |
| 34 | RamenSelect | **吃面/中山-全** | 4 |
| 34 | SpecialSelect | **3** | 3 |
| 34 | Train | **智训练** | 9 |
| 35 | RamenSelect | **吃面/京都-耐根** | 4 |
| 35 | SpecialSelect | **3** | 3 |
| 35 | Train | **耐训练** | 9 |
| 35 | Event | **2** | 2 |
| 36 | RamenSelect | **4** | 4 |
| 36 | Train | **1** | 1 |
| 37 | RamenSelect | **吃面/中山-全** | 4 |
| 37 | SpecialSelect | **吃面/中山-全(替换Cx2)** | 3 |
| 37 | Train | **智训练** | 7 |
| 38 | RamenSelect | **吃面/中山-全** | 4 |
| 38 | SpecialSelect | **1** | 1 |
| 38 | Train | **智训练** | 7 |
| 39 | RamenSelect | **2** | 2 |
| 39 | Train | **智训练** | 7 |
| 40 | RamenSelect | **3** | 3 |
| 40 | Train | **智训练** | 9 |
| 40 | Event | **2** | 2 |
| 41 | RamenSelect | **吃面/京都-耐根** | 4 |
| 41 | SpecialSelect | **6** | 6 |
| 41 | Train | **耐训练** | 9 |
| 42 | RamenSelect | **3** | 3 |
| 42 | Train | **智训练** | 9 |
| 43 | RamenSelect | **吃面/中山-全** | 4 |
| 43 | SpecialSelect | **3** | 3 |
| 43 | Train | **智训练** | 9 |
| 44 | RamenSelect | **1** | 1 |
| 44 | Train | **比赛** | 9 |
| 44 | Event | **2** | 2 |
| 45 | RamenSelect | **2** | 2 |
| 45 | Train | **普通出行** | 9 |
| 46 | RamenSelect | **吃面/京都-耐根** | 3 |
| 46 | SpecialSelect | **1** | 1 |
| 46 | Train | **耐训练** | 9 |
| 46 | Event | **2** | 2 |
| 47 | Event | **2** | 2 |
| 47 | RamenSelect | **1** | 1 |
| 47 | Train | **智训练** | 9 |
| 47 | RegionSelect | **地区[札幌-速,京都-速耐智,阪神-速耐力]** | 120 |
| 48 | Event | **事件#4010 古马年-新年:   体力30 /  速8 耐8 力8 根8 智8  /  35pt** | 3 |
| 48 | RamenSelect | **4** | 4 |
| 48 | Train | **1** | 1 |
| 49 | RamenSelect | **4** | 4 |
| 49 | Train | **友人出行** | 9 |
| 49 | Event | **事件#830305113 友人出行3:   体力50 羁绊+5 干劲1 /  速10 力10 根10 20pt 羁绊+5 干劲1** | 2 |
| 50 | RamenSelect | **吃面/阪神-速耐力** | 4 |
| 50 | SpecialSelect | **9** | 9 |
| 50 | Train | **耐训练** | 9 |
| 51 | RamenSelect | **吃面/京都-速耐智** | 4 |
| 51 | SpecialSelect | **1** | 1 |
| 51 | Train | **智训练** | 9 |
| 52 | RamenSelect | **3** | 3 |
| 52 | Train | **友人出行** | 9 |
| 53 | RamenSelect | **3** | 3 |
| 53 | Train | **友人出行** | 9 |
| 54 | RamenSelect | **吃面/京都-速耐智** | 4 |
| 54 | SpecialSelect | **吃面/京都-速耐智(替换Bx1+Cx1)** | 3 |
| 54 | Train | **智训练** | 8 |
| 54 | Event | **2** | 2 |
| 55 | RamenSelect | **3** | 3 |
| 55 | Train | **1** | 1 |
| 56 | RamenSelect | **4** | 4 |
| 56 | Train | **比赛** | 8 |
| 56 | Event | **2** | 2 |
| 57 | RamenSelect | **吃面/阪神-速耐力** | 4 |
| 57 | SpecialSelect | **9** | 9 |
| 57 | Train | **耐训练** | 8 |
| 58 | RamenSelect | **吃面/阪神-速耐力** | 4 |
| 58 | SpecialSelect | **9** | 9 |
| 58 | Train | **8** | 8 |
| 59 | RamenSelect | **3** | 3 |
| 59 | Train | **1** | 1 |
| 60 | RamenSelect | **3** | 3 |
| 60 | Train | **根训练** | 7 |
| 61 | RamenSelect | **吃面/京都-速耐智** | 4 |
| 61 | SpecialSelect | **吃面/京都-速耐智(替换Bx1+Cx1)** | 3 |
| 61 | Train | **7** | 7 |
| 62 | RamenSelect | **吃面/京都-速耐智** | 4 |
| 62 | SpecialSelect | **1** | 1 |
| 62 | Train | **耐训练** | 7 |
| 63 | RamenSelect | **3** | 3 |
| 63 | Train | **休息** | 7 |
| 64 | RamenSelect | **吃面/札幌-速** | 4 |
| 64 | SpecialSelect | **9** | 9 |
| 64 | Train | **8** | 8 |
| 65 | RamenSelect | **3** | 3 |
| 65 | Train | **休息** | 8 |
| 66 | RamenSelect | **吃面/阪神-速耐力** | 4 |
| 66 | SpecialSelect | **9** | 9 |
| 66 | Train | **耐训练** | 8 |
| 67 | RamenSelect | **1** | 1 |
| 67 | Train | **1** | 1 |
| 68 | RamenSelect | **吃面/札幌-速** | 3 |
| 68 | SpecialSelect | **4** | 4 |
| 68 | Train | **8** | 8 |
| 69 | RamenSelect | **1** | 1 |
| 69 | Train | **智训练** | 8 |
| 69 | Event | **2** | 2 |
| 70 | RamenSelect | **吃面/札幌-速** | 3 |
| 70 | SpecialSelect | **1** | 1 |
| 70 | Train | **8** | 8 |
| 71 | RamenSelect | **1** | 1 |
| 71 | Train | **1** | 1 |
| 71 | SuperRamenSelect | **超级拉面选项 2** | 3 |
| 72 | Train | **耐训练** | 7 |
| 72 | Event | **2** | 2 |
| 73 | Train | **1** | 1 |
| 74 | Train | **7** | 7 |
| 75 | Train | **1** | 1 |
| 76 | Train | **7** | 7 |
| 77 | Train | **1** | 1 |

### [6] sta0_wis2（204 个决策回合）

| 回合 | 阶段 | AI 决定 | 候选择优（前 4） |
|------|------|---------|----------------|
| 0 | Train | **智训练** | 7 |
| 1 | Train | **根训练** | 7 |
| 2 | RegionSelect | **地区[札幌-速,新潟-力,东京-智]** | 10 |
| 2 | RamenSelect | **吃面/札幌-速** | 4 |
| 2 | SpecialSelect | **9** | 9 |
| 2 | Train | **7** | 7 |
| 3 | RamenSelect | **吃面/东京-智** | 4 |
| 3 | SpecialSelect | **4** | 4 |
| 3 | Train | **智训练** | 7 |
| 4 | RamenSelect | **1** | 1 |
| 4 | Train | **耐训练** | 7 |
| 5 | Event | **事件#5004 马娘事件4:  根20  /  智20 ** | 2 |
| 5 | RamenSelect | **吃面/新潟-力** | 3 |
| 5 | SpecialSelect | **1** | 1 |
| 5 | Train | **力训练** | 7 |
| 6 | Event | **事件#830305103 友人解锁:  智5 5pt 体力25 羁绊+5 干劲1 +休息心得(1回合) /  速5 智5 5pt 羁绊+5 干劲1 Hint+5 +休息心得(1回合)** | 2 |
| 6 | RamenSelect | **1** | 1 |
| 6 | Train | **智训练** | 8 |
| 7 | RamenSelect | **1** | 1 |
| 7 | Train | **智训练** | 8 |
| 8 | RamenSelect | **1** | 1 |
| 8 | Train | **8** | 8 |
| 8 | Event | **2** | 2 |
| 9 | Event | **事件#5005 马娘事件5:  智20  /  20pt** | 2 |
| 9 | RamenSelect | **吃面/札幌-速** | 3 |
| 9 | SpecialSelect | **1** | 1 |
| 9 | Train | **8** | 8 |
| 10 | RamenSelect | **1** | 1 |
| 10 | Train | **根训练** | 8 |
| 10 | Event | **2** | 2 |
| 11 | RamenSelect | **2** | 2 |
| 11 | Train | **1** | 1 |
| 12 | RamenSelect | **吃面/东京-智** | 3 |
| 12 | SpecialSelect | **1** | 1 |
| 12 | Train | **智训练** | 8 |
| 12 | Event | **2** | 2 |
| 13 | RamenSelect | **1** | 1 |
| 13 | Train | **智训练** | 9 |
| 14 | Event | **事件#5002 马娘事件2:  耐20  /  力20 ** | 2 |
| 14 | RamenSelect | **2** | 2 |
| 14 | Train | **智训练** | 9 |
| 15 | RamenSelect | **吃面/札幌-速** | 2 |
| 15 | SpecialSelect | **1** | 1 |
| 15 | Train | **9** | 9 |
| 16 | RamenSelect | **1** | 1 |
| 16 | Train | **比赛** | 9 |
| 16 | Event | **2** | 2 |
| 17 | RamenSelect | **1** | 1 |
| 17 | Train | **智训练** | 9 |
| 18 | RamenSelect | **吃面/札幌-速** | 3 |
| 18 | SpecialSelect | **1** | 1 |
| 18 | Train | **9** | 9 |
| 19 | Event | **2** | 2 |
| 19 | RamenSelect | **1** | 1 |
| 19 | Train | **智训练** | 9 |
| 20 | RamenSelect | **吃面/东京-智** | 3 |
| 20 | SpecialSelect | **1** | 1 |
| 20 | Train | **智训练** | 9 |
| 21 | RamenSelect | **1** | 1 |
| 21 | Train | **智训练** | 9 |
| 22 | RamenSelect | **2** | 2 |
| 22 | Train | **力训练** | 9 |
| 22 | Event | **2** | 2 |
| 23 | RamenSelect | **2** | 2 |
| 23 | Train | **智训练** | 9 |
| 23 | RegionSelect | **10** | 10 |
| 24 | Event | **事件#4009 经典年-新年:  速25  /   体力20 /  20pt** | 3 |
| 24 | RamenSelect | **吃面/中京-力根** | 4 |
| 24 | SpecialSelect | **3** | 3 |
| 24 | Train | **根训练** | 9 |
| 25 | RamenSelect | **1** | 1 |
| 25 | Train | **9** | 9 |
| 26 | RamenSelect | **吃面/中山-全** | 2 |
| 26 | SpecialSelect | **1** | 1 |
| 26 | Train | **智训练** | 9 |
| 27 | RamenSelect | **1** | 1 |
| 27 | Train | **友人出行** | 9 |
| 28 | RamenSelect | **吃面/中京-力根** | 4 |
| 28 | SpecialSelect | **3** | 3 |
| 28 | Train | **力训练** | 9 |
| 29 | RamenSelect | **1** | 1 |
| 29 | Train | **友人出行** | 9 |
| 30 | RamenSelect | **吃面/京都-耐根** | 4 |
| 30 | SpecialSelect | **3** | 3 |
| 30 | Train | **根训练** | 9 |
| 30 | Event | **2** | 2 |
| 31 | RamenSelect | **1** | 1 |
| 31 | Train | **智训练** | 9 |
| 32 | RamenSelect | **吃面/中山-全** | 4 |
| 32 | SpecialSelect | **3** | 3 |
| 32 | Train | **智训练** | 9 |
| 32 | Event | **2** | 2 |
| 33 | RamenSelect | **1** | 1 |
| 33 | Train | **比赛** | 9 |
| 33 | Event | **2** | 2 |
| 34 | RamenSelect | **1** | 1 |
| 34 | Train | **智训练** | 9 |
| 35 | RamenSelect | **吃面/中京-力根** | 3 |
| 35 | SpecialSelect | **1** | 1 |
| 35 | Train | **力训练** | 9 |
| 35 | Event | **2** | 2 |
| 36 | RamenSelect | **3** | 3 |
| 36 | Train | **1** | 1 |
| 37 | RamenSelect | **吃面/中山-全** | 4 |
| 37 | SpecialSelect | **6** | 6 |
| 37 | Train | **智训练** | 7 |
| 38 | RamenSelect | **1** | 1 |
| 38 | Train | **智训练** | 7 |
| 39 | RamenSelect | **吃面/中山-全** | 4 |
| 39 | SpecialSelect | **3** | 3 |
| 39 | Train | **智训练** | 7 |
| 40 | RamenSelect | **1** | 1 |
| 40 | Train | **智训练** | 9 |
| 40 | Event | **2** | 2 |
| 41 | RamenSelect | **吃面/中京-力根** | 3 |
| 41 | SpecialSelect | **1** | 1 |
| 41 | Train | **力训练** | 9 |
| 42 | RamenSelect | **1** | 1 |
| 42 | Train | **比赛** | 9 |
| 42 | Event | **2** | 2 |
| 43 | RamenSelect | **2** | 2 |
| 43 | Train | **智训练** | 9 |
| 44 | RamenSelect | **4** | 4 |
| 44 | Train | **比赛** | 9 |
| 44 | Event | **2** | 2 |
| 45 | RamenSelect | **4** | 4 |
| 45 | Train | **普通出行** | 9 |
| 46 | RamenSelect | **吃面/中京-力根** | 4 |
| 46 | SpecialSelect | **3** | 3 |
| 46 | Train | **力训练** | 9 |
| 47 | Event | **2** | 2 |
| 47 | RamenSelect | **2** | 2 |
| 47 | Train | **9** | 9 |
| 47 | RegionSelect | **地区[中山-速力智,中京-速力根,小仓-速根智]** | 120 |
| 48 | Event | **事件#4010 古马年-新年:   体力30 /  速8 耐8 力8 根8 智8  /  35pt** | 3 |
| 48 | RamenSelect | **4** | 4 |
| 48 | Train | **1** | 1 |
| 49 | RamenSelect | **4** | 4 |
| 49 | Train | **友人出行** | 9 |
| 49 | Event | **事件#830305113 友人出行3:   体力50 羁绊+5 干劲1 /  速10 力10 根10 20pt 羁绊+5 干劲1** | 2 |
| 50 | RamenSelect | **吃面/小仓-速根智** | 4 |
| 50 | SpecialSelect | **吃面/小仓-速根智(替换Bx1)** | 8 |
| 50 | Train | **智训练** | 9 |
| 51 | RamenSelect | **吃面/中山-速力智** | 4 |
| 51 | SpecialSelect | **3** | 3 |
| 51 | Train | **智训练** | 9 |
| 52 | RamenSelect | **吃面/小仓-速根智** | 4 |
| 52 | SpecialSelect | **4** | 4 |
| 52 | Train | **智训练** | 9 |
| 53 | RamenSelect | **1** | 1 |
| 53 | Train | **智训练** | 9 |
| 54 | RamenSelect | **吃面/中山-速力智** | 2 |
| 54 | SpecialSelect | **1** | 1 |
| 54 | Train | **智训练** | 9 |
| 54 | Event | **2** | 2 |
| 55 | RamenSelect | **1** | 1 |
| 55 | Train | **1** | 1 |
| 56 | RamenSelect | **1** | 1 |
| 56 | Train | **友人出行** | 9 |
| 57 | RamenSelect | **4** | 4 |
| 57 | Train | **友人出行** | 9 |
| 58 | RamenSelect | **吃面/小仓-速根智** | 4 |
| 58 | SpecialSelect | **吃面/小仓-速根智(替换Bx2)** | 4 |
| 58 | Train | **8** | 8 |
| 59 | RamenSelect | **4** | 4 |
| 59 | Train | **1** | 1 |
| 60 | RamenSelect | **吃面/小仓-速根智** | 4 |
| 60 | SpecialSelect | **吃面/小仓-速根智(替换Ax1+Bx1)** | 8 |
| 60 | Train | **根训练** | 7 |
| 61 | RamenSelect | **吃面/中山-速力智** | 4 |
| 61 | SpecialSelect | **3** | 3 |
| 61 | Train | **智训练** | 7 |
| 62 | RamenSelect | **吃面/小仓-速根智** | 4 |
| 62 | SpecialSelect | **8** | 8 |
| 62 | Train | **根训练** | 7 |
| 63 | RamenSelect | **吃面/中京-速力根** | 4 |
| 63 | SpecialSelect | **1** | 1 |
| 63 | Train | **根训练** | 7 |
| 64 | RamenSelect | **吃面/小仓-速根智** | 3 |
| 64 | SpecialSelect | **1** | 1 |
| 64 | Train | **根训练** | 8 |
| 65 | RamenSelect | **1** | 1 |
| 65 | Train | **力训练** | 8 |
| 66 | RamenSelect | **1** | 1 |
| 66 | Train | **休息** | 8 |
| 67 | RamenSelect | **1** | 1 |
| 67 | Train | **1** | 1 |
| 68 | RamenSelect | **吃面/中山-速力智** | 2 |
| 68 | SpecialSelect | **1** | 1 |
| 68 | Train | **8** | 8 |
| 69 | RamenSelect | **1** | 1 |
| 69 | Train | **根训练** | 8 |
| 70 | RamenSelect | **2** | 2 |
| 70 | Train | **休息** | 8 |
| 71 | RamenSelect | **2** | 2 |
| 71 | Train | **1** | 1 |
| 71 | SuperRamenSelect | **超级拉面选项 2** | 3 |
| 72 | Train | **根训练** | 7 |
| 72 | Event | **2** | 2 |
| 73 | Train | **1** | 1 |
| 74 | Train | **7** | 7 |
| 75 | Train | **1** | 1 |
| 76 | Train | **7** | 7 |
| 77 | Train | **1** | 1 |

### [7] spd2_gut0（199 个决策回合）

| 回合 | 阶段 | AI 决定 | 候选择优（前 4） |
|------|------|---------|----------------|
| 0 | Train | **智训练** | 7 |
| 1 | Train | **7** | 7 |
| 2 | RegionSelect | **10** | 10 |
| 2 | RamenSelect | **吃面/札幌-速** | 4 |
| 2 | SpecialSelect | **9** | 9 |
| 2 | Train | **7** | 7 |
| 3 | RamenSelect | **吃面/函馆-耐** | 4 |
| 3 | SpecialSelect | **4** | 4 |
| 3 | Train | **耐训练** | 7 |
| 4 | RamenSelect | **1** | 1 |
| 4 | Train | **7** | 7 |
| 5 | Event | **2** | 2 |
| 5 | RamenSelect | **1** | 1 |
| 5 | Train | **智训练** | 7 |
| 6 | Event | **事件#830305103 友人解锁:  智5 5pt 体力25 羁绊+5 干劲1 +休息心得(1回合) /  速5 智5 5pt 羁绊+5 干劲1 Hint+5 +休息心得(1回合)** | 2 |
| 6 | RamenSelect | **吃面/函馆-耐** | 3 |
| 6 | SpecialSelect | **1** | 1 |
| 6 | Train | **耐训练** | 8 |
| 7 | RamenSelect | **1** | 1 |
| 7 | Train | **智训练** | 8 |
| 8 | RamenSelect | **1** | 1 |
| 8 | Train | **8** | 8 |
| 9 | Event | **事件#5005 马娘事件5:  智20  /  20pt** | 2 |
| 9 | RamenSelect | **2** | 2 |
| 9 | Train | **智训练** | 8 |
| 10 | RamenSelect | **3** | 3 |
| 10 | Train | **根训练** | 8 |
| 10 | Event | **2** | 2 |
| 11 | RamenSelect | **4** | 4 |
| 11 | Train | **1** | 1 |
| 12 | RamenSelect | **4** | 4 |
| 12 | Train | **智训练** | 8 |
| 12 | Event | **2** | 2 |
| 13 | RamenSelect | **吃面/函馆-耐** | 4 |
| 13 | SpecialSelect | **1** | 1 |
| 13 | Train | **耐训练** | 9 |
| 14 | Event | **2** | 2 |
| 14 | RamenSelect | **4** | 4 |
| 14 | Train | **休息** | 9 |
| 15 | RamenSelect | **吃面/新潟-力** | 4 |
| 15 | SpecialSelect | **1** | 1 |
| 15 | Train | **力训练** | 9 |
| 16 | RamenSelect | **2** | 2 |
| 16 | Train | **力训练** | 9 |
| 17 | RamenSelect | **吃面/函馆-耐** | 2 |
| 17 | SpecialSelect | **1** | 1 |
| 17 | Train | **耐训练** | 9 |
| 18 | RamenSelect | **1** | 1 |
| 18 | Train | **根训练** | 9 |
| 19 | Event | **2** | 2 |
| 19 | RamenSelect | **3** | 3 |
| 19 | Train | **休息** | 9 |
| 20 | RamenSelect | **吃面/札幌-速** | 3 |
| 20 | SpecialSelect | **1** | 1 |
| 20 | Train | **9** | 9 |
| 21 | RamenSelect | **1** | 1 |
| 21 | Train | **9** | 9 |
| 22 | Event | **2** | 2 |
| 22 | RamenSelect | **吃面/函馆-耐** | 2 |
| 22 | SpecialSelect | **1** | 1 |
| 22 | Train | **耐训练** | 9 |
| 23 | RamenSelect | **1** | 1 |
| 23 | Train | **休息** | 9 |
| 23 | RegionSelect | **地区[中山-全,阪神-耐力,小仓-智]** | 10 |
| 24 | Event | **事件#4009 经典年-新年:  速25  /   体力20 /  20pt** | 3 |
| 24 | RamenSelect | **吃面/阪神-耐力** | 4 |
| 24 | SpecialSelect | **9** | 9 |
| 24 | Train | **耐训练** | 9 |
| 25 | RamenSelect | **1** | 1 |
| 25 | Train | **9** | 9 |
| 26 | RamenSelect | **4** | 4 |
| 26 | Train | **比赛** | 9 |
| 26 | Event | **2** | 2 |
| 27 | RamenSelect | **吃面/中山-全** | 4 |
| 27 | SpecialSelect | **1** | 1 |
| 27 | Train | **9** | 9 |
| 28 | RamenSelect | **2** | 2 |
| 28 | Train | **友人出行** | 9 |
| 29 | RamenSelect | **4** | 4 |
| 29 | Train | **友人出行** | 9 |
| 30 | RamenSelect | **吃面/阪神-耐力** | 4 |
| 30 | SpecialSelect | **吃面/阪神-耐力(替换Cx2)** | 9 |
| 30 | Train | **耐训练** | 9 |
| 31 | RamenSelect | **吃面/中山-全** | 4 |
| 31 | SpecialSelect | **3** | 3 |
| 31 | Train | **9** | 9 |
| 32 | RamenSelect | **吃面/小仓-智** | 2 |
| 32 | SpecialSelect | **1** | 1 |
| 32 | Train | **智训练** | 9 |
| 33 | RamenSelect | **1** | 1 |
| 33 | Train | **比赛** | 9 |
| 33 | Event | **2** | 2 |
| 34 | RamenSelect | **1** | 1 |
| 34 | Train | **智训练** | 9 |
| 35 | RamenSelect | **吃面/阪神-耐力** | 3 |
| 35 | SpecialSelect | **1** | 1 |
| 35 | Train | **耐训练** | 9 |
| 35 | Event | **2** | 2 |
| 36 | RamenSelect | **2** | 2 |
| 36 | Train | **1** | 1 |
| 37 | RamenSelect | **吃面/阪神-耐力** | 3 |
| 37 | SpecialSelect | **1** | 1 |
| 37 | Train | **耐训练** | 7 |
| 38 | RamenSelect | **1** | 1 |
| 38 | Train | **耐训练** | 7 |
| 39 | RamenSelect | **2** | 2 |
| 39 | Train | **7** | 7 |
| 40 | RamenSelect | **3** | 3 |
| 40 | Train | **休息** | 9 |
| 41 | RamenSelect | **吃面/阪神-耐力** | 4 |
| 41 | SpecialSelect | **4** | 4 |
| 41 | Train | **耐训练** | 9 |
| 42 | RamenSelect | **2** | 2 |
| 42 | Train | **9** | 9 |
| 43 | RamenSelect | **吃面/中山-全** | 4 |
| 43 | SpecialSelect | **3** | 3 |
| 43 | Train | **9** | 9 |
| 44 | RamenSelect | **2** | 2 |
| 44 | Train | **休息** | 9 |
| 45 | RamenSelect | **2** | 2 |
| 45 | Train | **普通出行** | 9 |
| 46 | RamenSelect | **3** | 3 |
| 46 | Train | **9** | 9 |
| 47 | RamenSelect | **吃面/中山-全** | 4 |
| 47 | SpecialSelect | **1** | 1 |
| 47 | Train | **9** | 9 |
| 47 | RegionSelect | **地区[中山-速力智,京都-速耐智,阪神-速耐力]** | 120 |
| 48 | Event | **事件#4010 古马年-新年:   体力30 /  速8 耐8 力8 根8 智8  /  35pt** | 3 |
| 48 | RamenSelect | **4** | 4 |
| 48 | Train | **1** | 1 |
| 49 | RamenSelect | **4** | 4 |
| 49 | Train | **友人出行** | 9 |
| 49 | Event | **事件#830305113 友人出行3:   体力50 羁绊+5 干劲1 /  速10 力10 根10 20pt 羁绊+5 干劲1** | 2 |
| 50 | RamenSelect | **吃面/中山-速力智** | 4 |
| 50 | SpecialSelect | **吃面/中山-速力智(替换Cx2)** | 6 |
| 50 | Train | **9** | 9 |
| 51 | RamenSelect | **吃面/京都-速耐智** | 4 |
| 51 | SpecialSelect | **6** | 6 |
| 51 | Train | **智训练** | 9 |
| 52 | RamenSelect | **4** | 4 |
| 52 | Train | **友人出行** | 9 |
| 53 | RamenSelect | **4** | 4 |
| 53 | Train | **友人出行** | 9 |
| 54 | RamenSelect | **吃面/中山-速力智** | 4 |
| 54 | SpecialSelect | **吃面/中山-速力智(替换Cx2)** | 6 |
| 54 | Train | **智训练** | 8 |
| 54 | Event | **2** | 2 |
| 55 | RamenSelect | **4** | 4 |
| 55 | Train | **1** | 1 |
| 56 | RamenSelect | **吃面/阪神-速耐力** | 4 |
| 56 | SpecialSelect | **9** | 9 |
| 56 | Train | **力训练** | 8 |
| 56 | Event | **2** | 2 |
| 57 | RamenSelect | **吃面/京都-速耐智** | 3 |
| 57 | SpecialSelect | **6** | 6 |
| 57 | Train | **8** | 8 |
| 58 | RamenSelect | **1** | 1 |
| 58 | Train | **8** | 8 |
| 59 | RamenSelect | **3** | 3 |
| 59 | Train | **1** | 1 |
| 60 | RamenSelect | **吃面/阪神-速耐力** | 4 |
| 60 | SpecialSelect | **4** | 4 |
| 60 | Train | **力训练** | 7 |
| 61 | RamenSelect | **3** | 3 |
| 61 | Train | **休息** | 7 |
| 62 | RamenSelect | **吃面/阪神-速耐力** | 4 |
| 62 | SpecialSelect | **吃面/阪神-速耐力(替换Ax1+Cx1)** | 9 |
| 62 | Train | **力训练** | 7 |
| 63 | RamenSelect | **吃面/京都-速耐智** | 4 |
| 63 | SpecialSelect | **吃面/京都-速耐智(替换Cx1)** | 6 |
| 63 | Train | **耐训练** | 7 |
| 64 | RamenSelect | **4** | 4 |
| 64 | Train | **休息** | 8 |
| 65 | RamenSelect | **吃面/中山-速力智** | 4 |
| 65 | SpecialSelect | **3** | 3 |
| 65 | Train | **智训练** | 8 |
| 66 | RamenSelect | **1** | 1 |
| 66 | Train | **8** | 8 |
| 67 | RamenSelect | **4** | 4 |
| 67 | Train | **1** | 1 |
| 68 | RamenSelect | **吃面/京都-速耐智** | 4 |
| 68 | SpecialSelect | **3** | 3 |
| 68 | Train | **耐训练** | 8 |
| 69 | RamenSelect | **1** | 1 |
| 69 | Train | **智训练** | 8 |
| 70 | RamenSelect | **吃面/阪神-速耐力** | 2 |
| 70 | SpecialSelect | **1** | 1 |
| 70 | Train | **力训练** | 8 |
| 70 | Event | **2** | 2 |
| 71 | RamenSelect | **1** | 1 |
| 71 | Train | **1** | 1 |
| 71 | SuperRamenSelect | **超级拉面选项 2** | 3 |
| 72 | Train | **7** | 7 |
| 72 | Event | **2** | 2 |
| 73 | Train | **1** | 1 |
| 74 | Train | **智训练** | 7 |
| 75 | Train | **1** | 1 |
| 76 | Train | **7** | 7 |
| 77 | Train | **1** | 1 |


（7 卡组合计 1402 个决策回合，与 HTML 版同源数据）
