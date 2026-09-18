# GA 提升实验 E2/E2b 收账（残血考场自搜 vs E1 双包基线）

**日期**: 2026-09-19（北京）　**实验**: algo-lab 仓 ga-optimize.yml（commit 0fc32ab 后首跑）
**E2 run**: [35348152028](https://github.com/xf8410/uma-algo-lab/actions/runs/35348152028) ✅　**E2b run**: [35348158629](https://github.com/xf8410/uma-algo-lab/actions/runs/35348158629) ✅

## 一、本轮跑了哪些算法（铁律清单）

| 算法 | 配置 | 轮数 | 状态 |
|---|---|---|---|
| GA 自搜 gens8（E2） | pop8/gens8/elitism2，双包种子（r8champ+tpe_best 注入），uma=random，--seed 每轮独立 | 10151 | 本轮 |
| GA 自搜 gens16（E2b） | 同上但 gens 翻倍、loop180min | 7344（有效收账 3672 轮精评+holdout 双口径齐） | 本轮 |
| 新加算法 | **无**。本轮为 GA 引擎算力/代数扫描，未引入 MPC/GBDT/RL | — | — |

对照基线 E1（run 35344765431，9213 轮，固定权重直接考）：r8champ 51821.3±4985.5、tpe_best 52097.5±4746.4、71k 锚 71415.6（R8 老家口径）。

## 二、结果（同尺残血考场）

| 指标 | E1-r8champ | E1-tpe_best | **E2 (gens8)** | **E2b (gens16)** |
|---|---|---|---|---|
| best_fitness 均值 | 51821.3 | 52097.5 | **58693.7** | **59808.0** |
| vs E1-r8 | — | — | **+6872.4（z=+112）** | **+7986.7（z=+107）** |
| p50 / p90 / max | — | — | 58927 / 62771 / 69033 | 60079 / 63835 / 68681 |
| holdout 均值（40r seed43） | — | — | 58465.5 | 59547.3 |
| best−holdout gap（过拟合度） | — | — | +228.2（0.4%） | +260.7（0.4%） |
| 71k 折算* | 71415.6 | 71692 | **78288.0** | **79402.3** |

\* 折算 = 71415.6 − (51821.3 − mean)。受「考场变严疑点」影响（定标实验见下），绝对折算值仅供参考；**相对 E1 同尺提升是铁的**（z>100）。

- E2b vs E2：+1114.3（z≈+17.7，显著）→ gens 翻倍仍有正收益，算力未饱和
- 轮间独立种子（--seed $i，0fc32ab 修复生效）；E1 无法与之做轮级 CRN（E1 全轮 ga_seed=42），故采用分布级 z 检验

## 三、结论

1. **GA 路线能提升，实锤**。残血考场自搜均值比 E1 两包基线高 +6600~+8000 分（z>100），71k 折算过 71000 锚。不需要立刻转第二档算法。
2. **算力还有红利**：gens 8→16 再拿 +1114。下一步可试 pop 16 / gens 32（loop 时间按比例放）。
3. 定标实验（当前 master 重放 R8 冠军 vs 8e9f7a5 锚值）用于钉死「考场变严疑点」→ 折算口径的绝对值可信度；实验已派发，报告另出。
4. E2b 冠军基因组（best_genome.toml×3672）已随 artifact 归档，可做 None 基因占比与收敛共性分析，喂给下一轮 pop/gens 扫描。

## 复现

```bash
gh workflow run ga-optimize.yml -R xf8410/uma-algo-lab \
  -f pop=8 -f generations=16 -f elitism=2 \
  -f seeds=r8_best_genome.toml,seed_tpe_best.toml \
  -f uma=random -f loop_minutes=180 -f tag=e2b_gens16
# 收账: artifact ga-e2b_gens16 → run_N/ga_generations.csv 末行 best_fitness
```
