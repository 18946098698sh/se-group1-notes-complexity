# 1组 · 软件复杂性及度量方法（MiCode/Notes）

软件系统与工程课程作业。分析对象为小米便签开源版 MiCode/Notes，基线 commit 见 `git log`，tag `v0.0-baseline`。

## 五人分工（各 20%）

| 成员 | 工作包 | 代码范围 | 主责任务 | 分支 |
|---|---|---|---|---|
| 阿班（组长） | P1 data + 统稿 | `src/net/micode/notes/data` | 基线、注释规范、数据契约表、第 1 章、统稿、AI 声明、提交 | `feature/P1-data` |
| 韩家阳 | P3 ui 列表与设置 | `ui` 的列表/设置相关 6 文件 | 注释、列表/文件夹/搜索/设置流程、组织结构图、流程图之一 | `feature/P3-ui-list` |
| 谢鸿 | P4 ui 编辑与提醒 | `ui` 的编辑/提醒相关 8 文件 | 注释、编辑与提醒流程、代码质量问题清单、流程图之二 | `feature/P4-ui-edit` |
| 王一帆 | P5 gtask + widget | `gtask` + `widget` | 注释、同步链路、模块依赖图、5 张控制流图与 V(G) | `feature/P5-gtask-widget` |
| 孙浩 | P2 model + tool | `model` + `tool` | 注释、WorkingNote 状态模型、统计脚本、5 个超均方法、认知复杂度评分 | `feature/P2-model-tool` |

复核配对：韩家阳 ↔ 谢鸿，王一帆 ↔ 孙浩，组长总审合入 `main`。

## 协作流程（每人 4 步）

```bash
git checkout feature/Px-xxx        # 1. 切到自己的分支
#  …改代码/写注释…
git add <改动的文件>
git commit -m "annot(Px): 注释便签列表查询流程"   # 2. 提交（格式见下）
git push origin feature/Px-xxx                   # 3. 推送
#  4. 在 GitHub 上开 Pull Request → 指定复核人 → 通过后由组长合并
```

## 提交信息规范

`type(scope): subject`

- type：`annot` 注释 / `doc` 文档 / `metric` 度量数据 / `fig` 图表 / `fix` 修复 / `chore` 杂项
- scope：`P1`–`P5` 或 `REPORT`
- 例：`metric(P2): 统一 LOC 统计脚本并输出 5 个超均方法`

## 时间节点

| 日期 | 节点 | 交付 |
|---|---|---|
| 11/17 | 口径会 | 注释规范、分支就位 |
| 11/19 | 中期检查 | 注释过半 |
| 11/21 | 交叉复核会 | 注释完成、图表初稿 |
| 11/22 | 度量完成 | 5 张 CFG、三法数据 |
| 11/24 | 终稿会签 | 报告初稿 + 复核记录 |
| 11/25 | 提交 | docx + PDF 交班长 |

## 注意

- 只提交源码与文档，不要提交 `bin/`、`gen/`（已在 `.gitignore`）。
- 未经复核人 review 的分支不要自己合并到 `main`。
