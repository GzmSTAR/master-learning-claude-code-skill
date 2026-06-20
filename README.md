# Master Learning for Claude Code

![Master Learning 总览](docs/showcase/01-overview.png)

`master-learning` 是一个给 Claude Code 使用的前置学习 skill。它让 Claude Code 在真正实现之前，先单独完成一次调研和学习，产出 `Learning Brief` 后再交给主会话继续规划或编码。

它适合处理陌生领域、新框架、新 API、论文复现、GitHub 项目改造、标准规范和本地代码约束。核心理念是：大师永远怀着一颗学徒的心。

这个 Claude Code 版本使用：

```yaml
context: fork
agent: general-purpose
```

也就是说，学习过程会在 forked context 中完成，避免调研过程污染主会话的实现上下文。

![Master Learning 流程](docs/showcase/02-workflow.png)

## 它是干嘛的

`/master-learning <task>` 会让 Claude Code 先做一轮结构化学习：

- 先明确任务目标、目标环境、未知点、成功标准和风险等级。
- 读取本地项目文件、依赖、配置、测试和已有约定。
- 查官方文档、release notes、迁移说明、标准和规范。
- 查论文时提取方法、假设、评估设置、代码/数据可用性和工程限制。
- 查 GitHub 项目时检查许可证、活跃度、examples、tests、issues 和依赖健康度。
- 标记证据不足、来源冲突、网络降级、暂定结论和待确认问题。
- 返回一份可供主会话使用的 `Learning Brief`。

## 什么时候用

适合使用：

- 陌生领域项目启动。
- 新框架 / 新 API / 最新文档任务。
- 论文复现或研究型实现。
- GitHub 高星项目改造。
- 需要先读本地代码再实现的项目。
- 错误成本较高、不能靠猜的工程任务。

不适合使用：

- 修 typo。
- 明确的小 bug。
- 格式化。
- 用户明确要求不要调研。

## Learning Brief 包含什么

返回的 brief 会覆盖：

- `Task`：用户目标、运行环境、成功标准、研究深度、信心等级。
- `Sources`：来源表，包含链接/路径、类型、时效性、可信度和用途。
- `Domain Model`：关键概念、对象、数据、关系和术语。
- `Local Code Lessons`：本地项目结构、约定、配置、测试和限制。
- `GitHub/Code Lessons`：仓库、模式、许可证、examples、issues。
- `Paper/Standard Lessons`：论文/标准中的方法、假设、限制和要求。
- `Implementation Patterns`：架构、API 契约、数据流、测试方式。
- `Risks and Anti-Patterns`：风险、边界情况、反模式和弱假设。
- `Recommendation`：推荐方案、验收标准和下一步。
- `Open Questions`：仍需用户确认或继续调研的问题。

![Master Learning 训练验证](docs/showcase/03-training.png)

## SkillOpt-style 训练

这个仓库包含一个 Microsoft SkillOpt 启发的本地训练/验证流程。它把 `SKILL.md` 当作可训练的外部状态，通过场景 rollout、失败反思、有界编辑和 held-out validation 来优化 skill 文档。

包含文件：

- `.claude/skills/master-learning/references/skillopt-training.md`
- `.claude/skills/master-learning/scripts/skillopt_train.py`
- `.claude/skills/master-learning/training/benchmark-scenarios.json`
- `.claude/skills/master-learning/training/skillopt-run-2026-06-21.md`
- `.claude/skills/master-learning/training/skillopt-run-2026-06-21-round2.md`
- `.claude/skills/master-learning/training/skillopt-run-2026-06-21-128.md`

场景覆盖：

- 最新框架 / API 使用
- 论文复现
- GitHub 项目改造
- 本地项目优先
- 低风险任务跳过
- 网络降级调研

128 轮稳定性验证结果：`score 1.0`，release gate `PASS`。

![Master Learning 安装分享](docs/showcase/04-install.png)

## 安装

### 个人安装

```powershell
git clone https://github.com/GzmSTAR/master-learning-claude-code-skill.git
Copy-Item -Recurse -Force .\master-learning-claude-code-skill\.claude\skills\master-learning "$env:USERPROFILE\.claude\skills\master-learning"
```

### 项目安装

```powershell
git clone https://github.com/GzmSTAR/master-learning-claude-code-skill.git
Copy-Item -Recurse -Force .\master-learning-claude-code-skill\.claude\skills\master-learning .\.claude\skills\master-learning
```

如果 Claude Code 没有自动刷新 skill 列表，重启 Claude Code。

## 使用示例

```text
/master-learning Build a robot vision prototype. Study official docs, GitHub examples, papers, and local project constraints before planning.
```

```text
/master-learning Learn the current best implementation pattern for this new framework and produce a Learning Brief before coding.
```

## 目录结构

```text
.claude/
  skills/
    master-learning/
      SKILL.md
      references/
      scripts/
      training/
```

脚本全部只使用 Python 标准库。

## License

MIT
