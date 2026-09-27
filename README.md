# 高维鲁棒的能量稳定变分移动网格算法研究及其应用

本科毕业论文研究仓库，以 FEALPy 为主要计算平台。当前研究底座已经覆盖二维有向几何、一维等分布、固定网格 Poisson 制造解和现有 GFMMPDE 最小基线。


## 仓库结构

```text
moving-mesh-thesis/
├── docs/           # 研究主档、环境审查、源码地图、计划与交接
├── experiments/    # 可独立运行的编号实验
├── references/     # 文献索引与公开参考实现说明，不存放无权分发的原文
├── results/        # 实验输出说明；可重复生成的数据和图片默认不提交
├── src/            # 自有的可复用几何、网格与算法模块
├── tests/          # 数学性质和回归测试
├── requirements.txt
└── requirements-lock-windows-py313.txt
```


## 最短运行

```powershell
cd D:\桌面\moving-mesh-thesis
.\.venv\Scripts\python.exe -m pytest -q
.\.venv\Scripts\python.exe -m experiments.a_geometry
.\.venv\Scripts\python.exe -m experiments.b_equidistribution_1d
.\.venv\Scripts\python.exe -m experiments.c_poisson_manufactured
.\.venv\Scripts\python.exe -m experiments.d_mmesher_baseline
```

运行结果写入 `results/`。环境、源码地图、实验口径和本轮交接分别见 `docs/environment_audit.md`、`docs/fealpy_code_map.md`、`docs/experiment_protocol.md` 和 `docs/session_handoff.md`。

## 当前验证状态

| 项目 | 状态 | 主要证据 |
| --- | --- | --- |
| 有向三角形几何 | 通过 | 翻转为负、退化为零、单位方形总面积为 1 |
| 一维等分布 E0 | 通过 | 40 段监控质量最大相对偏差约 `1.92e-9` |
| P1 Poisson 制造解 | 通过 | L2 约二阶、H1 半范数约一阶 |
| GFMMPDE 最小二维路径 | 通过 | 移动后单元保持正定向、总面积为 1 |

## 当前边界

- FEALPy 基线来自本机 `C:\Users\10251\fealpy` 的 3.4.0 源码；精确提交与 dirty 状态见环境审计。
- GFMMPDE 最小基线没有暴露可比较的离散网格能量历史；当前只报告有向面积、位移、插值误差和耗时。
- 未把示例运行、质量指标或能量曲线解释为新的算法贡献。
- 当前没有三维、Burgers 或全离散能量稳定结论。

## 参考来源

- FEALPy: <https://github.com/weihuayi/fealpy>
- Huang and Kamenski, *A geometric discretization and a simple implementation for variational mesh generation and adaptation*, 2015.
- Huang and Kamenski, *On the mesh nonsingularity of the moving mesh PDE method*, 2018.
- 项目规划依据：`docs/高维鲁棒能量稳定变分移动网格_研究主档.md`。
