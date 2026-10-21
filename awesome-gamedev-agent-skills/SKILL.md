---
name: awesome-gamedev-agent-skills
description: 游戏开发技能路由。按任务匹配本目录的通用开发技能与Godot技能。适用于玩法、AI、UI、美术、音频、性能、测试与导出任务。
---

# 游戏开发技能路由

## 一、选择流程

1. 先确认任务目标、引擎、版本与目标平台
2. 根据任务选择下方的直接匹配项
3. 通过相对链接读取对应的`SKILL.md`
4. 需要设计方法时，选择通用技能
5. 需要Godot实现时，选择Godot技能
6. 跨领域任务可组合技能，避免全量加载
7. 子技能引用的资料，仅在需要时读取
8. 路由不改变用户授权与项目规范

## 二、Godot技能地图

1. GDScript语法、类型、注解、生命周期与异步流程
   读取[godot-gdscript](godot/godot-gdscript/SKILL.md)
2. 场景拆分、节点树、实例化与自动加载
   读取[godot-nodes-scenes](godot/godot-nodes-scenes/SKILL.md)
3. 信号连接、节点分组与事件解耦
   读取[godot-signals-groups](godot/godot-signals-groups/SKILL.md)
4. 自定义Resource、配置数据与资源加载
   读取[godot-resources](godot/godot-resources/SKILL.md)
5. 2D角色移动、跳跃、斜坡与地面判定
   读取[godot-2d-movement](godot/godot-2d-movement/SKILL.md)
6. 刚体、区域检测、碰撞层与射线查询
   读取[godot-physics](godot/godot-physics/SKILL.md)
7. TileMapLayer、TileSet、地形与格子读写
   读取[godot-tilemap](godot/godot-tilemap/SKILL.md)
8. Control布局、Container、Theme与焦点
   读取[godot-ui-control](godot/godot-ui-control/SKILL.md)
9. AnimationPlayer、AnimationTree与Tween
   读取[godot-animation](godot/godot-animation/SKILL.md)
10. Godot着色器语法、材质参数与屏幕采样
    读取[godot-shaders](godot/godot-shaders/SKILL.md)
11. 3D场景、相机、灯光、环境与GridMap
    读取[godot-3d-essentials](godot/godot-3d-essentials/SKILL.md)
12. 音频播放节点、音频总线与节拍同步
    读取[godot-audio](godot/godot-audio/SKILL.md)
13. ENet联机、RPC、节点权限与状态同步
    读取[godot-multiplayer](godot/godot-multiplayer/SKILL.md)
14. GDScript无窗口测试、CI与测试退出码
    读取[godot-gdscript-headless-testing](godot/godot-gdscript-headless-testing/SKILL.md)
15. 导出模板、平台预设、命令行构建与Web部署配置
    读取[godot-export](godot/godot-export/SKILL.md)

## 三、通用技能地图

1. 美术方向、精灵、图块、纹理与成套资产生产
   读取[create-game-assets](disciplines/create-game-assets/SKILL.md)
2. 按键映射、重绑定、多设备输入与输入缓冲
   读取[input-systems](disciplines/input-systems/SKILL.md)
3. 重力、阻尼、固定步长、抖动与穿透调校
   读取[physics-tuning](disciplines/physics-tuning/SKILL.md)
4. 跟随相机、死区、前瞻、平滑与多目标取景
   读取[camera-systems](disciplines/camera-systems/SKILL.md)
5. 状态机选型、寻路、转向与敌人决策
   读取[game-ai](disciplines/game-ai/SKILL.md)
6. 行为树运行时、黑板、效用评分与混合决策
   读取[ai-behavior-trees-utility-ai](disciplines/ai-behavior-trees-utility-ai/SKILL.md)
7. 关卡白盒、空间布局、节奏、门控与遭遇设计
   读取[level-design](disciplines/level-design/SKILL.md)
8. 随机种子、噪声、地牢算法与权重掉落
   读取[procedural-gen](disciplines/procedural-gen/SKILL.md)
9. HUD、菜单流程、安全区域与交互可用性
   读取[game-ui-ux](disciplines/game-ui-ux/SKILL.md)
10. 分支对话、条件变量、Ink与Yarn方案
    读取[dialogue-systems](disciplines/dialogue-systems/SKILL.md)
11. 存读档、原子写入、自动保存与版本迁移
    读取[save-systems](disciplines/save-systems/SKILL.md)
12. 混音架构、音量闪避、自适应音乐与音效变化
    读取[audio-design](disciplines/audio-design/SKILL.md)
13. 着色管线、坐标空间、UV与通用视觉效果
    读取[shader-programming](disciplines/shader-programming/SKILL.md)
14. 打击停顿、震屏、挤压拉伸与反馈打磨
    读取[game-feel](disciplines/game-feel/SKILL.md)
15. 性能测量、CPU/GPU定位、对象池与资源预算
    读取[performance-optimization](disciplines/performance-optimization/SKILL.md)

## 四、相近任务的选择边界

1. AI方案选型与寻路使用`game-ai`
   行为树或效用系统实现使用专项AI技能
2. UI流程与交互设计使用`game-ui-ux`
   Godot节点布局使用`godot-ui-control`
   UI图标与贴图生产使用`create-game-assets`
3. 碰撞节点与查询使用`godot-physics`
   稳定性与物理手感使用`physics-tuning`
   2D角色控制使用`godot-2d-movement`
4. 输入缓冲与土狼时间使用`input-systems`
   震屏与打击反馈使用`game-feel`
   相机跟随与取景使用`camera-systems`
5. 音乐结构与混音设计使用`audio-design`
   Godot播放与总线API使用`godot-audio`
6. 着色原理与效果算法使用`shader-programming`
   Godot语法与内置变量使用`godot-shaders`
7. 随机地图算法使用`procedural-gen`
   人工布局与节奏使用`level-design`
   Godot格子绘制使用`godot-tilemap`
8. 游戏状态持久化使用`save-systems`
   Godot资源建模与加载使用`godot-resources`
   Resource不替代完整的存档设计
9. 测试运行与退出码使用无窗口测试技能
   构建产物与导出预设使用`godot-export`
   两者均可使用无窗口模式，按目的选择
10. 卡顿先使用`performance-optimization`定位
    再按实测瓶颈补充对应领域技能

## 五、典型组合路线

1. Godot随机地牢：`procedural-gen`
   绘制补充`godot-tilemap`
2. Godot平台跳跃：`godot-2d-movement`
   输入容错补充`input-systems`
3. Godot菜单与HUD：`game-ui-ux`
   布局补充`godot-ui-control`
4. Godot发布流水线：`godot-export`
   需要逻辑测试时补充无窗口测试技能

## 六、适用范围与验证

1. 先核对项目版本与可用API
   不因子技能的示例版本自动升级项目
2. 技能不可用或任务无匹配项时，说明缺口
   不编造技能路径或接口
3. 无窗口测试只验证对应逻辑
   画面、手感、音频与触控需实际运行验收
