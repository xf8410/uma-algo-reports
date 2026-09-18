# GA r8 收账报告（20260917 2320 场次）

**Run**: 35188122064 | tag=ga-loop-r8 | **HEAD=7c983a0** | uma=random, pop=50, gens=100, loop_minutes=240
**结论**: conclusion=cancelled = 240 分钟 timeout 截断（14:02:24 启动 → 18:03:48 结束，241 分钟，属正常）
**有效轮数**: 120 轮完整（第 121 轮开始即截断，解析已跳过）——注意 r7 是 180 轮，r8 轮数下降原因见第三节
**产物**: `ga_loop_r8_runs.json`（120轮）、`ga_loop_r8_genomes.json`（120个基因组TOML）、`ga_r8_cardparse.json`（120轮卡组解析）、`ga_r8_raw.log`/`ga_r8_clean.log`（原始+清洗日志）、`replay_r8/`（top3 育成过程回放，见第五节）

## 一、本轮跑了什么算法 & 与基线对比（算法清单铁律）

**本轮算法 = 原有 GA 主线（无新增算法）**：随机抽马 + GA 优化器（pop=50 / gens=100 / elitism=4 / 锦标赛k=3 / cx=0.90 / σ 0.15→0.03 / 停滞5 重启），评估协议同前：初筛 3build×20runs(seed=42) → 精评 7build×60runs(seed=42) → holdout 40runs(seed=43)。马匹范围=umaDB 随机池 267 骑，育成马娘本体卡自动剔除。

| 指标 | r8（120轮/102骑） | 三 run 合并锚点 r5+r6+r7（494轮/225骑） | 四 run 合并账（614轮/242骑） |
|---|---|---|---|
| fitness max | **71415.6** | 71415.6 | 71415.6 |
| fitness avg | 69553.0 | 69566.3 | 69563.7 |
| holdout max | 71328.9 | 71368.0 | 71368.0 |
| holdout avg | 69434.7 | 69440.5 | 69439.4 |
| gap avg（精评−holdout） | 118.3 | 125.8 | 124.3 |
| holdout≥精评轮占比 | 21.7% | 17.8% | 18.6% |

- **r8 最优轮 = #65 赤心的驯鹿小姐 目白善信（106402）fitness=71415.6 / holdout=71328.9（gap 86.7）**——与 r5 打出的历史最高分 71415.6 逐位同分、同基因组哈希（9d8ce67d58616c83），= 历史最优在新 HEAD 上原样复现
- r8 holdout 最优同为此轮 71328.9；新光风的 holdout 历史最高 71368.0 本轮未复现（马没抽到），合并账不变
- **新加算法线 = GA 实验室（uma-algo-lab）四优化器**（CMA-ES / TPE / SA / CEM，bench_base CLI 黑盒口径），本日赛马结果见第六节

## 二、确定性复现：r8 与 r5/r6/r7 同马交集校验全零差异 ✅

**重点校验**：r8 跑在新 HEAD 7c983a0（scalar! 宏修复 + local_ramen_trainer/bench_base +140 行 parse_override_toml），任务要求确认评估链路未被碰。

| 对比 | 同马交集（每马最好轮） | fitness 分差>0.05 | holdout 分差>0.05 | GA 基因组哈希不一致 |
|---|---|---|---|---|
| r8∩r5 | 54 骑 | 0 | 0 | 0 |
| r8∩r6 | 38 骑 | 0 | 0 | 0 |
| r8∩r7 | 50 骑 | 0 | 0 | 0 |
| 三交集 | 14 骑 | 0 | 0 | 0 |

**结论**：142 骑次对比全部逐位一致（含目白善信 71415.6 的精确复现），**7c983a0 未影响 GA 评估链路，无重大信号**。
（解析备注：交集马 TOML 内容 sha256 在 r6 对比时出现"不一致"，实为两次收账解析脚本末尾换行处理差 1 字节，非参数差异；以 GA 程序原生输出的"基因组哈希"字段为准，全一致。）

## 三、r8 轮均耗时上升（值得注意但无证据影响结果）

- r8 轮均 **118s**（min 98 / max 128，来自逐轮"耗时 XXXXms"），r7 同口径约 80s/轮 → **慢 ~47%**，240 分钟只跑出 120 轮（r7=180）
- 7c983a0 改动只是宏修复 + genome TOML 覆盖层输出（输出在轮末，不在评估热路径），且第二节已证明分数逐位不变——**慢的原因更可能是 Actions runner 负载波动**，暂按"链路行为无变化、吞吐下降"记账
- **r9 起预期轮数按 ~120 轮/4h 记账**（若 r9 恢复 180 轮则说明是 runner 负载）

## 四、合并账：四 run（r5-r8，614 轮 / 242 骑）卡组骨架

- **速2耐1智2 = 593/614 = 96.6%**（r8 单独 117/120 = 97.5%，锚点 96.4%，继续维持 96%+ ✓）；次高 速3耐1智1=11 轮、速2力1智2=10 轮
- **top25% 高分轮（fitness≥70337.0，31 轮）100% 速2耐1智2 且 100% 恰好五卡**——连续第三个 run 维持极致收敛
- **万能卡组五卡**（302894 智 / 303124 速 / 303174 速 / 303064 智 / 303044 耐）：
  - 恰好收敛到这组五卡：**568/614 = 92.5%**（r8 单独 95.0%，为历轮最高）
  - 单卡出现率（合并）：302894=100.0%、303124=99.2%、303174=99.0%、303064=98.2%、303044=95.1%
- **马匹覆盖**：r8 覆盖 102 骑、其中 17 骑全新 → 四 run 累计 **242 骑**。r8 新增马最高分：蔷薇之梦 米浴 71011.8（holdout 70903.3），次高 Neige Émeraude 目白阿尔丹 70512.3、万王之王 鲁道夫象征 70458.4

**结论**："速2耐1智2 + 万能五卡"骨架经**四个独立 run（累计 614 轮）验证稳定**，卡组通解地位继续加固。

## 五、新增交付：top3 育成过程回放报告 ✅

- 取 r8 fitness top3 基因组 → 写 TOML（`replay_r8/genome_top1~3.toml`）→ 沙箱现装 rustup 编译 bench_base（master 8e9f7a5，评估核心与 7c983a0 同源；release 编译在 2GB 内存沙箱 OOM，改 debug 编译成功，debug/release 数值语义一致）→ `bench_base --uma <该轮马> --trainer handwritten --genome-file <toml> --log --runs 1 --seed 1001`
- **报告**：`replay_r8/育成过程报告.md`（大白话逐回合表格：每马 7 卡组分数汇总 + 最优卡组全程 ~198 回合逐回合记录）
- top3 逐回合 CSV 原始产物在 `replay_r8/top1~top3/`（每 build 一份）
- 口径提醒（报告内已写）：GA fitness=7build×60runs 均值，回放=每 build 单局 seed=1001，单局分数低于 GA fitness 属正常，对比看走势不看绝对值

| 回放 | 马 | 来源轮 | GA fitness | 回放最优卡组 | 回放单局分 |
|---|---|---|---|---|---|
| top1 | 赤心的驯鹿小姐 目白善信 | #65 | 71415.6 | speed_wisdom | 69642 |
| top2 | 栖花绮裁 机伶金花 | #60 | 71329.9 | speed_wisdom | 70010 |
| top3 | 红涂疾驱具足 莫名其妙 | #7 | 71147.0 | speed_wisdom | 72480 |

## 六、lab 赛马线（CMA-ES / TPE / SA / CEM）本日结果

- **run 35191902291（14:53 主赛马）= failure**（82 秒即失败，无产物，未出结果）
- **run 35230292332（21:56 快验，budget=16，cmaes+cem）= success**：uma=111501 空中救世主、smoke 档、seed=1001 单局口径
  - **CEM best = 63451.8** / **CMA-ES best = 63339.1**（GA center 同口径实测 63301.6 → CEM +150.2 / CMA-ES +37.5）
  - 两条优化器在浅预算（16 次评估）下小幅跑赢 center，**远未达进主线标准**（按算法噪声纪律需 CRN 配对显著提升）；TPE / SA 线本日未出成绩
- 早前 17:45 快验 run 35206281937（budget=4）：Δ−3.4 良性，无变化

## 七、r9 已派发 + 一个必须盯的信号

- **r9 Run: 35240018089**（23:24:24 北京 queued，uma=random, pop=50, gens=100, loop_minutes=240, tag=ga-loop-r9），**r9 收账日程建议挂 23:55 起每 20 分钟巡检 + 明晨 03:40 收账**（按 120 轮节奏预计 03:24 跑满 240min）
- ⚠️ **r9 跑在 master 53227d4（又前进 5 个 commit）**：其中 **875dd2c 合并了 upstream/master，触碰 umasim 评估核心**（game/ramen/policy.rs +201 行、game.rs +49、local_ramen_trainer.rs +144、ramen_mcts_trainer.rs +121、flat_search.rs、gamedata/default_config.toml 与 game_config.toml 均有变更）；53227d4 只清理 bench_base 重复定义
- **r9 收账时必须重做同马交集校验**：若交集马不再逐位一致 = upstream 合并改变了评估口径，r9 与 r5-r8 合并账**不可直接混算**，届时需按"新口径首跑"独立记账并立刻上报主人

## 八、解析备忘（r8 实操新增）

- 本轮改用 Actions API 下载 job 日志（`/actions/jobs/{id}/logs`），行前缀为 ISO 时间戳（`2026-09-17T06:04:06.xxxZ `），剥离正则吃掉时间戳+1 空格；**holdout 行首有 2 个空格**，正则须 `^\s*\[holdout\]`（r7 用 gh --log 格式无此坑）
- artifact 285MB：gh api 卡死时直接 curl API 拿 302（**fresh signed URL 有效期 ~10 分钟**，16 段并行下载 15 段成功后补段需重新取 URL）
- artifact 内只有 `run_1~run_120/` 目录（best_genome.toml / ga_generations.csv / ga_detail.csv / preset_baseline.toml），**无主日志**；主日志走 job logs 接口
- 沙箱编译坑：2GB 内存 1 核，`cargo build --release` 编 umasim 必 OOM（加 swap 失败 Operation not permitted）→ **debug profile 可过**（数值语义一致）；crates.io 走 rsproxy.cn 镜像 60s 拉完依赖；云盘拷源码有幽灵行（cp 出的 local_ramen_trainer.rs 与源 md5 不符）→ **源码必须从 GitHub sparse clone 拉干净版**
