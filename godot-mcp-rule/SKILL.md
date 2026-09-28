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

如果 godot-ai MCP 不可用或连接失败，应明确说明，而不是假设 Godot 当前状态
