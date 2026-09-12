---
name: webpage-construction
description: 不可以主动调用这个技能，仅当用户说明处理网页导出包的时候才能调用这个技能
---

# 网页包构建处理
这个技能是为了处理Godot引擎导出网页包之后的压缩和调用，以减少网页包体体积

# 处理步骤

## Brolti压缩
- 使用brolti指令`.js`,`.pck`,`.wasm`后缀的文件
- 压缩指令`-q 11`，压缩等级11级
- 压缩后删除源文件

## html文件处理
- 在加载 Godot 配置前新增了浏览器 fetch 重定向：当请求`.js`,`.pck`,`.wasm`文件时，分别改为请求`.js.br`,`.pck.br`,`.wasm.br`，以加载 Brotli 压缩资源
- 其余 Godot 配置和启动逻辑保持不变
- 请基于这一差异检查资源命名、服务器响应头和兼容性风险