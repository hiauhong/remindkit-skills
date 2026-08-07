# remindkit-skills · 方法论协议集合（agent 端）

> remindkit 生态的**方法论层**：把"如何看待 Apple Reminders 任务数据"沉淀为可执行协议，agent 按协议承担全部认知劳动，用户只做记录与两键审批。

```
remindkit（数据管道 · 无观点）→ remindkit-skills（方法论协议）→ agent（按协议执行）→ 用户（呈现 + 裁决）
```

## 架构关系

| 项目 | 角色 | 消费者 |
|---|---|---|
| remindkit | 管道：数据原语 + 写操作（无观点） | agent / skill / 前端 |
| **remindkit-skills**（本仓库） | 方法论：检测标准 + 流程编排 | agent（装进 agent 的 skills 目录） |
| remindscope | 视角：呈现决策面 + 两键审批 | 用户 |

依赖单向：前端 → 方法论 → 管道。

## 包含的方法论（一个方法论一个文件夹）

| 文件夹 | 方法论 | 安装 |
|---|---|---|
| `skills/gtd/` | 承诺循环（必装）：体检 → 聚焦 → 复盘 → 迁移，任务库健康为前提的规划循环 | 必装 |
| `skills/okr/` | 目标管理（可选）：列表→目标(O)→关键结果(KR)→行动 四层结构 + 目标体检/进度/季度检视 | 可选，用 OKR 时装 |

新方法论 = 新增一个文件夹，不修改现有 skill（方法论可插拔，互不耦合）。

## 安装

```bash
# 1. 先装 remindkit（数据管道）：https://github.com/hiauhong/remindkit-cli

# 2. 软链到 agent 的 skills 目录（软链 = 仓库更新即时生效，不会分叉）
mkdir -p ~/.agents/skills
ln -s "$PWD/skills/gtd" ~/.agents/skills/gtd      # 必装
ln -s "$PWD/skills/okr" ~/.agents/skills/okr      # 可选

# 3. 验证
ls -l ~/.agents/skills/gtd/SKILL.md
```

> 软链（而非拷贝）是本仓库的默认安装方式：方法论在仓库里迭代，agent 环境即时消费，避免"源"与"已安装版"悄悄分叉。

## 与相关项目的关系

- **remindkit**（数据管道）—— 所有 skill 只通过 `remindkit` 命令读写 Apple Reminders
- **remindscope**（前端视角）—— 与这些 skill 共享同一套方法论概念（agent 端 / 人端投影），随产品同步演进但独立发布

## 免责声明

任务数据通过 remindkit 读取，底层依赖苹果私有框架 ReminderKit（非官方 API，可能随 macOS 更新失效）。仅供个人使用与学习研究。
