# NN 权重纯 CPU 完整育成验收（pilot 1527 条）——结论：显著弱于手写，不进主线

- 日期：2026-10-24
- 上游仓：`xf8410/umaai-rs`，分支 `workbench/nn-cpu-bench`，commit `085aa56`
- 运行：GitHub Actions `nn-cpu-eval` run [39999322276](https://github.com/xf8410/umaai-rs/actions/runs/39999322276)（push 触发，默认参数）
- 数据：`data/20261024_nn_cpu_fullgame_pilot_pairs.csv`（140 对逐局）、`data/20261024_nn_cpu_fullgame_pilot_summary.json`（汇总）

## 1. 结论

按 `scripts/ramen_nn/CPU_EVAL_TASK.md` 的权威口径（`teacher-game` 两臂 CRN 对拍，`search_n=128`）跑完 7 马娘 × 20 seed = **140 对**：

| 指标 | NN 臂 | 手写臂 | 差值 |
|---|---:|---:|---:|
| 平均 `score` | 52788.2 | 68116.0 | **−15327.8（−22.5%）** |
| 平均 `score_pt` | 63451.7 | 81482.9 | −18031.2（−22.1%） |
| 平均整局墙钟 | 392 s | 13 s | 约 30 倍 |

配对 t 检验：`t(139) = −71.86`，`p ≈ 8.4e−112`；Wilcoxon 符号秩 `p ≈ 1.0e−24`；95% CI `[−15746, −14910]`。**NN 臂 0/140 胜**，最好的一对仍差 9109 分，最差差 21051 分。

判定：**pilot 权重（1527 条）不进主线，剔除。** 差距方向一致、幅度远超噪声，且 `score_pt`（不含 Hint 折算）差值更大，说明不是 Hint 折算口径造成的假差距。

⚠️ 该结论只对 pilot 权重有效。8 万条正式数据到齐后必须用同一协议复验，不能沿用本结论。

## 2. 算法清单（报告铁律 1）

本轮是验收，不是新算法实验：

| 项 | 内容 |
|---|---|
| 被验算法 | NN rollout 基策：ONNX（tract CPU）policy 头（234 维）在合法候选上 argmax；choice 头未训练，事件选项回落手写策略 |
| 权重 | release `nn-ramen-v1`（`model.onnx` + `model.onnx.json`），训练集 1527 条，simple-attention 编码器（token 64 / 1 block / MLP 192×2） |
| 对照 | 手写 rollout 基策（`--handwritten-rollout`），同一搜索框架 |
| 搜索 | `ramen_root_bench --mode teacher-game`，`search_n=128`，`radical_factor_max=1.4`，`run_idx` 默认 1200 |
| 新增算法 | 无 |

## 3. 数据与噪声口径（报告铁律 2、3）

- 配对纪律：同 `seed` + 同 `plan_index` + 同 `search_n`，两臂各一局；只比同对。
- 规模：`plan_index ∈ {0, 85, 170, 220, 305, 390, 475}`（GEN1 空间 525 个计划中 7 个马娘的最小下标），每个计划 `seed 61444..61463` 共 20 局。
- 未换种子复评：本结论未做第二批 seed 复验；但效应量（−15.3k，约 6 个配对差的标准差之外）与 0/140 胜率表明翻转可能性极低。
- 原始数据取自 CI artifact `results_plan_*`（7 份，保留 7 天），已转存为本仓 CSV。

### 逐计划

| plan_index | 马娘 | n | NN 均分 | 手写均分 | d(score) | d 相对 | d(score_pt) | t | p | NN 墙钟 | 手写墙钟 |
|---:|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| 0 | [灰姑娘]小栗帽 (100603) | 20 | 52633 | 66980 | −14347 | −21.4% | −17117 | −26.72 | 1.6e−16 | 224s | 10.3s |
| 85 | [Rock in☆MewMeow]摩耶重炮 (102403) | 20 | 53982 | 68692 | −14710 | −21.4% | −17385 | −27.85 | 7.2e−17 | 423s | 12.0s |
| 170 | [The Changer]杏目 (112901) | 20 | 53177 | 69156 | −15978 | −23.1% | −18856 | −34.30 | 1.5e−18 | 391s | 18.0s |
| 220 | [快乐小音符]菱钻奇宝 (110602) | 20 | 53269 | 68585 | −15316 | −22.3% | −18175 | −23.47 | 1.7e−15 | 378s | 13.8s |
| 305 | [保持微笑・我的道路！]放声欢呼 (113101) | 20 | 52886 | 68023 | −15137 | −22.3% | −17737 | −21.19 | 1.1e−14 | 392s | 12.2s |
| 390 | [不融化的糖果]真弓快车 (108702) | 20 | 52074 | 68099 | −16025 | −23.5% | −18730 | −32.05 | 5.3e−18 | 400s | 13.5s |
| 475 | [无上喜悦]东海帝王 (100301) | 20 | 51495 | 67276 | −15781 | −23.5% | −18218 | −33.01 | 3.0e−18 | 440s | 17.1s |

七个计划各自单独检验也全部显著为负（p ≤ 1.6e−14），没有「某个马娘上 NN 更好」的分化。

## 4. 成本

- 单局 NN 臂 224–440 s（tract CPU），手写臂 9.0–18.0 s。
- 140 局累计：NN 14.72 h、手写 0.54 h；7 个 matrix job 并行，CI 墙钟 2 h 39 min。
- 同协议扩到 8 万条复验前，建议先做根因诊断，避免重复烧 15 h/140 局的 CPU。

## 5. 局限（结论边界）

1. **只有 pilot 口径**：1527 条训练，不能外推到 8 万条正式权重。
2. **只有 `search_n=128`**：未做其它 n 的敏感性；小 n 下 NN 可能相对不那么差，但非本验收口径。
3. **只有 7 个马娘/计划**：GEN1 空间共 525 个计划，本批只覆盖 7 个马娘各 1 个下标，未覆盖同马娘不同卡组/形状。
4. **根因未定位**：本批没跑 `--steps-csv` / `--decision-csv`，无法回答「NN 在哪个阶段、哪个动作开始分叉」。−22.5% 的幅度提示基策本身接近无效（1527 条不足以学到可用 policy），而非某个后处理环节的单点问题。
5. **事件选项仍走手写**：两臂差异只在 `RamenSelect` 系根，事件决策同源，不是全链路策略差。

## 6. 复现

```bash
cargo build --release -p umasim --bin ramen_root_bench --features cli,onnx

# NN 臂
cargo run --release -p umasim --bin ramen_root_bench --features cli,onnx -- \
  --mode teacher-game --rollout-model /tmp/nn/model.onnx --cpu-only \
  --search-n 128 --seed 61444 --plan-index 0

# 手写臂（即使不接网络也必须传 --rollout-model）
cargo run --release -p umasim --bin ramen_root_bench --features cli,onnx -- \
  --mode teacher-game --rollout-model /tmp/nn/model.onnx --handwritten-rollout \
  --search-n 128 --seed 61444 --plan-index 0
```

权重下载：`https://github.com/xf8410/umaai-rs/releases/download/nn-ramen-v1/{model.onnx,model.onnx.json}`

## 7. 下一步建议

1. **8 万条正式权重到齐后**，用完全相同的协议（7 计划 × 20 seed × `search_n=128`）复验，并按需要扩计划/种子。
2. **复验前先做一次逐决策诊断**（1 个 plan × 1 seed × `search_n=32`，两臂加 `--steps-csv`/`--decision-csv`），定位首次分叉的阶段与动作；若起点就分叉，先查特征编码/归一化对齐，再谈训练。
3. pilot 权重不再投入任何整局预算；若要保留对照价值，只作为「链路已验证」的最小权重。
