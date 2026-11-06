# RoboTwin 2.0 · VLA Leaderboard

RoboTwin 2.0 的 VLA-only 榜单页面：只收录 Vision-Language-Action 策略，按
`Average = (Clean→Random + Clean→Clean) / 2` 排序。

静态单页、样式内联、无 JS、无构建依赖，直接由 GitHub Pages 托管。

## 页面内容

- `index.html` — 全部内容与样式，单文件
- 14 条 VLA 方法，其余方法数据来自 RoboTwin 2.0 官方榜 **2026-10-30** 快照（共 33 条）
- Novaxis（Nova-M 1.0）条目：Clean→Random 51.10%、Clean→Clean 84.50%、Average 67.80%，
  按官方协议评测（2026-10-20）。该条目尚未出现在上述官方快照中，收录状态以官方榜为准

## 收录口径

只保留推理时以视觉 + 语言为条件、直接输出动作的策略，排除：

- 世界-动作模型 / 世界模型策略：GO-3 Nano Preview（智元 WRAM）、ViGAR、ME-Dex-1.0、
  WorldScape Policy 2.0，以及 PrismWAM / PICA-WAM / PatchWAM / EWAM / UniWAM / 4D-WAM / X-WAM /
  FastWAM / AHA-WAM / CloudRobo-WM / MWA-Phoenix
- 非 VLA 基线：DP / DP3 / ACT / RDT

容易误判的几条及其判定依据：

| 方法 | 归类 | 依据 |
|---|---|---|
| WorldLA | 计入 VLA | 论文《WorldLA: Bridging World Action Models and Efficient VLAs…》，把 Fast-WAM 路由蒸馏进 π0.5，推理不跑世界模型 |
| Abot-M0 | 计入 VLA | 论文《ABot-M0: VLA Foundation Model for Robotic Manipulation…》，阿里高德 AMAP CV Lab |
| Discrete Forcing | 计入 VLA | 面向 VLA action expert 的少步去噪方法（OpenHelix） |
| GO-3 Nano Preview | 不计入 | 智元 WRAM 架构，RoboDojo 将其归为“智能体 + 世界-动作模型” |

> 官方总榜不区分 VLA / WAM。GO-3 Nano Preview 的 85.01% 来自 WRAM（世界-动作）架构，因此不入本表；
> 这也是本页排名与官方总榜不同的原因。

本页是官方总榜的 VLA 子集视图，**非 RoboTwin 官方页面**，样式仅作参考。

## 本地预览

```bash
python3 -m http.server 8000
# 打开 http://localhost:8000
```

## 部署到 GitHub Pages

Pages 使用分支部署，不依赖 GitHub Actions：

1. 仓库 **Settings → Pages**
2. Build and deployment → Source: **Deploy from a branch**
3. Branch: **main** / **(root)** → **Save**

- 站点：<https://zyfan1228.github.io/robotwin-vla-leaderboard/>
- 仓库：<https://github.com/zyfan1228/robotwin-vla-leaderboard>

## 更新数据

直接编辑 `index.html` 的 `<tbody>`：

1. 保持行按 Average 降序；
2. 子分数需满足 `(Clean→Random + Clean→Clean) / 2 = Average`；
3. 同步页头 `Latest update` 与页脚快照日期。

## 参考

- 官方榜：<https://robotwin-platform.github.io/leaderboard>
- 官方收录要求：公开代码 + 权重 + 技术报告（提交方式见官方页）