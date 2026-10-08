---
name: godot-mcp-rule
description: 使用godot引擎开发项目时调用此技能，计划制定、实际执行和验收阶段均可调用
---

## Godot MCP 使用规则
>开发 Godot 功能时，优先根据任务类型使用 godot-ai MCP

涉及以下内容时，应主动使用 godot-ai MCP，而不是仅通过读取或修改 .tscn/.tres 文件推测编辑器状态：
- 当前场景与场景树
- 节点创建、删除、移动与属性修改
- 信号连接
- UI、Camera、Animation、Material、Particle
- InputMap、Autoload 和项目设置
- Godot 编辑器错误与运行时错误
- 游戏能否正常启动与运行
- Plan模式下Godot MCP仅允许只读查询，所有写操作必须等待Act模式

完成涉及运行逻辑的修改后，优先执行：
1. 使用 Godot MCP 检查当前编辑器状态
2. 必要时运行项目，确认能否正常启动（仅用于检查是否能正常启动无报错，不可继续操作游戏内容）
3. 检查 Editor/Game 日志
4. 发现技术错误则继续修复并重新验证
5. 涉及连续操作、游戏手感、动态视觉、复杂交互、时序体验等内容时停止验收，交由人类开发者进行人工动态体验验收

纯 GDScript 代码编辑、算法修改、重构和文本资源修改，可以直接操作工程文件，不要求强制使用 MCP

如果 godot-ai MCP 不可用或连接失败，应明确向用户说明，而不是假设 Godot 当前状态

## Godot 无头启动规则

当需要为当前 Worktree 启动 Godot MCP 时：

1. 使用当前项目对应的 Godot 可执行文件，并通过绝对路径 `--path` 指向当前 Worktree。
2. 当前 Worktree 没有可复用 MCP session 时，使用 `--headless --editor --path <worktree>` 启动 Godot Editor。
3. 不得添加 `--quit`、`--quit-after`、`--import` 等会使编辑器退出的参数。
4. 启动成功后仍必须等待 MCP session 建立，并校验 `project_path` 与当前 Worktree 一致。
5. 保存对应 `session_id`，后续 MCP 调用显式指定该 session。
6. MCP 连接失败或超时时停止任务并报告，不得切换到其他 Worktree 的 session。
7. 仅清理本任务自行启动的 Godot 进程，不得关闭用户已有编辑器或其他 Worktree 的进程。
8. 无头模式只用于 MCP、运行检查和自动化验证，不能替代画面、输入、音频及游戏体验的人工验收。

## Godot MCP 启动规则
当任务需要使用 Godot MCP 时：

1. 查询当前已连接的 Godot sessions。
2. 根据 project_path 查找当前 Worktree 对应的 session。
3. 如果不存在，启动当前 Worktree 的 Godot Editor。
4. 等待对应 session 建立连接。
5. 再次校验 project_path，禁止使用其他 Worktree 的 session。
6. 保存对应 session_id。
7. 后续所有支持 session_id 的 MCP 调用必须显式指定。
8. 禁止依赖 global active session。
9. 如果 Godot 启动或 MCP 连接失败，停止任务并报告。