# Pair Programmer

一个用于“跟得上、看得懂”的 AI 结对编程 Skill。

AI 编码 Agent 往往实现得太快，用户还没理解当前修改，它就已经继续扩展范围。`pair-programmer` 让 AI 继续承担主要编码工作，但采用小而完整的改动，说明重要技术决策，如实报告验证情况，并明确下一步方向。

## 安装

### 推荐：skills CLI

```bash
npx skills add Nicander93/pair-programmer-skill
```

常用选项：

```bash
# 全局安装（所有项目可用）
npx skills add Nicander93/pair-programmer-skill -g

# 安装到指定 Agent
npx skills add Nicander93/pair-programmer-skill -a cursor -a claude-code

# 非交互安装
npx skills add Nicander93/pair-programmer-skill -g -y
```

### 备选：npm

```bash
npm install pair-programmer-skill
npx skills experimental_sync
```

### 手动安装

将 `skills/pair-programmer/` 目录复制到编码 Agent 支持的 Skills 目录中。不要修改目录名，因为目录名需要与 `SKILL.md` 中声明的 `name` 保持一致。

该 Skill 不需要脚本、第三方依赖、网络访问或外部服务，只要求 Agent 能读取代码库，并在获得授权时修改代码。

## 它解决什么问题

该 Skill 会要求编码 Agent：

- 修改前理解相关代码和调用关系；
- 优先完成最小、可审查、易回退的改动；
- 避免无关重构和过早抽象；
- 自主处理常规实现决策，不让用户审批每个细节；
- 说明真正重要的实现与架构决策；
- 在历史项目没有测试时，使用当前可行的验证证据；
- 每个阶段完成后说明修改、验证、风险和下一步。

它不会引入僵硬的审批流程，不限制固定代码行数，不要求每一步确认，也不强制为了流程而建设完整测试体系。

## 目录

```text
pair-programmer-skill/
├── package.json
├── README.md
├── README.zh-CN.md
├── CHANGELOG.md
├── LICENSE
└── skills/
    └── pair-programmer/
        └── SKILL.md
```

真正提供给 Agent 执行的是 `SKILL.md`，其余文件用于项目发布和说明。

## 使用示例

```text
使用 pair-programmer 和我一起阅读并逐步优化这个模块。
```

```text
和我结对解决这个 Bug。保持改动易于审查，并说明关键决策。
```

```text
继续完成下一个边界清晰的改动。
```

适合以下场景：

- 阅读和改进陌生或历史代码库；
- 增量开发功能；
- 调整架构；
- 定位并修复 Bug；
- 持续进行代码阅读与重构；
- 希望 AI 主要负责编码，但自己仍然掌握项目理解和方向。

## 设计原则

1. **AI 负责实现，但不失控扩张**  
   AI 可以自主编码和处理常规决策，但不能把有限任务悄悄扩大成全面重写。

2. **以可审查性判断“小步”**  
   小步不是固定限制文件数或代码行数，而是改动目的清晰、容易解释和回退。

3. **输出决策摘要，而不是冗长思维过程**  
   说明假设、证据、关键替代方案和取舍，帮助用户审查实际决策。

4. **验证方式适应代码库现状**  
   有测试时运行测试；没有测试时，可以采用编译、类型检查、静态分析、临时脚本、行为对比和调用链检查。

5. **沟通深度与改动风险匹配**  
   小修改只需简要说明，重要修改再详细展开。

## 边界

该 Skill 只定义结对协作方式，不规定语言、框架、架构、分支策略、提交格式或测试技术栈。

项目特有的代码规范应继续放在仓库说明或其他独立 Skill 中。

## 版本

项目遵循语义化版本。详见 [CHANGELOG.md](CHANGELOG.md)。

## 许可证

MIT
