# 车辆工程课程大纲 Skill

面向日常教学工作的可查询 Skill，内置车辆工程 2025 版培养方案结构化数据，用于检索课程基础字段、课程—指标点支撑关系和课程—培养目标派生追踪。

它属于 [Teaching Works Lab 课程教学 Skill 体系](https://github.com/Teaching-Works-Lab)，由 `training-program-skill-factory` 生成，可作为 `course-teaching-workflows` 编制课程基座和课程大纲时的可选培养方案依据。**本仓库保留原始 DOCX/PDF 作为证据，属内部私有资料，未做公开匿名化。**

## 适合做什么

- 按课程名称或课程代码查询学分、学时、学期、考核方式与承担单位；
- 查询课程对毕业要求指标点的官方直接支撑关系；
- 沿“指标点 → 毕业要求 → 培养目标”查看派生追踪路径；
- 为课程大纲准备来源中已经提供的基础字段；
- 检查结构、关系端点、课时汇总和建议性警告。

来源未提供课程目标、周次内容、教材或考核细则时，结果保持 `待编制`，不会按课程名称补写。

## 给 AI 的入口

执行课程查询或大纲准备前先读取 [SKILL.md](SKILL.md)，并遵守以下边界：

- 官方课程—指标点关系与系统派生的课程—培养目标路径必须分开呈现；
- 数据只适用于车辆工程 2025 版（代码 080207），其他专业或版本转交 [training-program-skill-factory](https://github.com/Teaching-Works-Lab/training-program-skill-factory)；
- 结构校验、支撑关系数量和派生路径不能表述为培养质量或学习成效。

## 快速开始

```powershell
py -3.12 scripts/curriculum.py validate data/program.json
py -3.12 scripts/curriculum.py query data/program.json --course "汽车理论" --format markdown
py -3.12 scripts/curriculum.py syllabus data/program.json --course "25JD31208"
```

## 数据内容

- 4 个培养目标；
- 11 个毕业要求、23 个指标点；
- 111 个课程/占位行、11 个课程组；
- 348 条保留 provenance 的关系记录（22 条要求—目标 + 326 条课程—指标）。

## 主要文件

```text
SKILL.md                    AI 执行入口与回答边界
data/program.json           可查询的结构化主数据
data/manifest.json          数据版本、计数与证据摘要
data/validation-report.md   错误与建议性警告
generated-from.json         工厂提交与模板摘要
evidence/                   原始 DOCX 与 PDF（事实证据）
scripts/curriculum.py       独立查询与校验 CLI
references/program.schema.json
```

## 数据状态与限制

- 当前结构校验为 0 个错误、41 个建议性警告；警告不是课程质量结论。
- 车辆工程含“汽车工程 / 轨道车辆”两个方向，方向必修与方向选修按方向分别记录；学生实际只修读一个方向。方向备选课全部保留为可查询实体，因此“全部开设行机械求和”与学生选定修读口径不同。
- 集中实践环节的学时以“周”计；程序在 hours 分项用空值记录周式实践，并在课程对象中单独保留 `practice_weeks`。
- 毕业要求对培养目标支撑表（22 个 √）与课程体系支撑毕业要求矩阵（97 行 × 23 指标、326 个 ●）均保留 `official_direct` + `visually_verified` 关系及真实源哈希。

## 验证

项目在 Python 3.12 环境完成验证；结构校验使用 `jsonschema`。

```powershell
py -3.12 scripts/curriculum.py validate data/program.json
```
