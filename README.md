# 1 组 · 软件复杂性及度量方法 · 工作说明

分析对象：小米便签开源版 **MiCode/Notes**（Java / Android）。
基线：`v0.0-baseline`（39 个 Java 文件，7395 行代码，含内部类 45 个）。

> **两条硬规则**
> 1. 只在**自己的分支**干活，**不要直接改 main**；合并由组长做完 review 后进行。
> 2. 注释**只加中文注释、不改业务逻辑**；每注释完一个文件就提交一次。

---

## 一、五人分工（各占总工作量 20%）

| 成员 | 工作包 | 代码范围 | 分支 | 复核人 |
|---|---|---|---|---|
| 阿班（组长） | P1 data + 统稿 | `src/net/micode/notes/data`（4 文件 / 628 行） | `feature/P1-data` | 总审全部 |
| 韩家阳 | P3 ui 列表与设置 | `ui` 列表/设置相关 6 文件（约 1500 行） | `feature/P3-ui-list` | 谢鸿 |
| 谢鸿 | P4 ui 编辑与提醒 | `ui` 编辑/提醒相关 8 文件（约 1500 行） | `feature/P4-ui-edit` | 韩家阳 |
| 王一帆 | P5 gtask + widget | `gtask` + `widget`（15 文件 / 1433 行） | `feature/P5-gtask-widget` | 孙浩 |
| 孙浩 | P2 model + tool | `model` + `tool`（6 文件 / 1133 行） | `feature/P2-model-tool` | 王一帆 |

---

## 二、把下面这段发给你的 AI 助手（复制整段，替换 `[ ]`）

### 韩家阳 —— P3 ui 列表与设置

```
我在做《软件复杂性及度量方法》小组作业，分析 MiCode/Notes（Java/Android）。
我负责 P3：ui 包的列表与设置部分，共 6 个文件（NotesListActivity、NotesListAdapter、
FoldersListAdapter、NotesListItem、DropdownMenu、NotesPreferenceActivity），约 1500 行。
分支：feature/P3-ui-list。复核人：谢鸿。

请你：
1) 先读这 6 个文件和仓库 README.md，画出类与方法的调用关系，不要先给结论；
2) 规划并撰写约 375 行新增中文注释（只加注释，不改任何业务逻辑），
   注释要说明"这段代码在做什么、为什么这样做、边界条件"，不要逐行翻译；
3) 梳理便签列表查询、文件夹切换、搜索、设置四条流程，输出文字版流程步骤（我要据此画流程图）；
4) 整理"模块组织结构图"所需信息：6 个包之间的依赖与职责。
每完成一个文件就提醒我 commit，提交信息格式 annot(P3): 说明。
```

### 谢鸿 —— P4 ui 编辑与提醒

```
我在做《软件复杂性及度量方法》小组作业，分析 MiCode/Notes（Java/Android）。
我负责 P4：ui 包的编辑与提醒部分，共 8 个文件（NoteEditActivity、NoteEditText、
NoteItemData、DateTimePicker、DateTimePickerDialog、Alarm 相关 3 个），约 1500 行。
分支：feature/P4-ui-edit。复核人：韩家阳。

请你：
1) 先读这 8 个文件，说明便签编辑保存的完整链路（界面 → 数据 → 存储）；
2) 规划并撰写约 375 行新增中文注释（只加注释，不改逻辑），重点解释嵌套较深的逻辑；
3) 梳理"编辑便签"与"设置提醒"两条流程，输出文字版步骤供画流程图；
4) 找出至少 2 个代码质量问题（仓库里有 12 处 TODO Auto-generated 空实现可作素材），
   每条写清：现象 + 源码位置 + 原因 + 改进建议。
每完成一个文件就提醒我 commit，格式 annot(P4): 说明。
```

### 王一帆 —— P5 gtask + widget

```
我在做《软件复杂性及度量方法》小组作业，分析 MiCode/Notes（Java/Android）。
我负责 P5：gtask 包（同步）与 widget 包（桌面小部件），共 15 个文件 1433 行。
分支：feature/P5-gtask-widget。复核人：孙浩。

请你：
1) 先读这 15 个文件，讲清 Google Tasks 同步链路：登录 → 拉取 → 本地写入 → 冲突处理；
2) 规划并撰写约 360 行新增中文注释（只加注释，不改逻辑）；
3) 输出 5 个方法的控制流图（用文字描述节点与边），并算出圈复杂度 V(G) 与独立路径数，
   优先选代码量大的方法（SqlNote.setContent 132 行、GTaskManager.syncFolder 124 行、syncContent 103 行）；
4) 画出 gtask、widget 与其他包的依赖关系（ui 与 gtask.remote 存在双向耦合，要指出）。
每完成一个文件就提醒我 commit，格式 annot(P5): 说明。
```

### 孙浩 —— P2 model + tool

```
我在做《软件复杂性及度量方法》小组作业，分析 MiCode/Notes（Java/Android）。
我负责 P2：model 包（2 文件）与 tool 包（4 文件），共 1133 行。
分支：feature/P2-model-tool。复核人：王一帆。

请你：
1) 先读这 6 个文件，讲清 WorkingNote 的状态与生命周期；
2) 规划并撰写约 285 行新增中文注释（只加注释，不改逻辑）；
3) 写一个统计脚本：输出每个方法的有效代码行（不含空行与注释）、全体均值、
   以及超过均值的候选方法清单（我要从中挑 5 个）；
4) 设计一个"认知复杂度"评分量表（维度：模块间依赖关系 + 代码隐晦程度），
   每个维度 1–5 分并给出判定依据，用于给 5 个方法打分。
每完成一个文件就提醒我 commit，格式 annot(P2): 说明。
```

### 阿班（组长） —— P1 data + 统稿

```
我在做《软件复杂性及度量方法》小组作业，分析 MiCode/Notes（Java/Android）。
我负责 P1：data 包 4 个文件（Notes、NotesDatabaseHelper、NotesProvider、Contact），628 行，
另外负责统稿与提交。分支：feature/P1-data。

请你：
1) 先读这 4 个文件，输出数据契约表：URI、MIME 类型、字段、Provider 路由；
2) 规划并撰写约 160 行新增中文注释（只加注释，不改逻辑）；
3) 起草第 1 章（项目来源、代码基线、技术栈、统计口径、工具环境）。
每完成一个文件就提醒我 commit，格式 annot(P1): 说明。
```

---

## 三、四步流程

```bash
git checkout feature/Px-xxx          # 1. 切到自己的分支（只做一次）
#  …改代码 / 写注释…
git add <改动的文件>
git commit -m "annot(Px): 注释便签列表查询流程"     # 2. 提交
git push origin feature/Px-xxx                     # 3. 推送
# 4. 在 GitHub 上开 Pull Request，Reviewer 填你的复核人，等组长合并
```

## 四、提交信息规范

`type(scope): subject`

- type：`annot` 注释 / `doc` 文档 / `metric` 度量数据 / `fig` 图表 / `fix` 修复 / `chore` 杂项
- scope：`P1`–`P5` 或 `REPORT`
- 例：`metric(P2): 统一 LOC 统计脚本并输出 5 个超均方法`

## 五、时间节点

| 日期 | 节点 | 交付 |
|---|---|---|
| 11/17 | 口径会 | 分支就位、注释规范统一 |
| 11/19 | 中期检查 | 各自模块注释过半 |
| 11/21 | 交叉复核会 | 注释完成、图表初稿 |
| 11/22 | 度量完成 | 5 张控制流图、三法数据 |
| 11/24 | 终稿会签 | 报告初稿 + 复核记录 |
| 11/25 | 提交 | docx + PDF 交班长 |

## 六、注意事项

- 注释量按"所负责代码行 × 25%"配置（含冗余），最终报告按 20% 口径验收。
- 不要提交 `bin/`、`gen/`、`project.properties`（已在 `.gitignore`）。
- 未通过复核人 review 的分支，不要自己合并到 `main`。
- 用了 AI 辅助的环节，在 PR 描述里写明"用了什么工具、用在哪、谁验证"，报告附录 A 要逐条对应。
