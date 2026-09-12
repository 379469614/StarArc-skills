---
name: webpage-construction
description: 不可以主动调用这个技能，仅当用户说明处理网页导出包的时候才能调用这个技能
---

# 网页包构建处理
这个技能是为了处理Godot引擎导出网页包之后的压缩和调用，以减少网页包体体积

# 处理步骤

## 文件确认
- 先确认已有`index.html`,`index.js`,`index.pck`,`index.wasm`文件
- 如果没有则直接终止任务，并输出文件缺失情况
- 如果源文件不存在，但`.br`存在且`HTML`已引用`.br`，就提示“已经处理完成”

## 压缩处理
### Brotli压缩
- 使用Brotli压缩`index.js`,`index.pck`,`index.wasm`文件
- 压缩指令`-q 11 -k`，压缩等级11级，压缩后先不删除源文件
- 原先已有对应的`.br`文件的则不再执行该压缩
- 压缩时间限制为3分钟，超时则终止并报告情况
### br文件检查
- 压缩完成之后执行一次 Brotli 解压测试
  - 确认`.br`未损坏
  - 确认解压后的文件与源文件的一致性
- 如果有损坏或不一致则删除损坏的`br`文件，并重新执行压缩处理流程，最多重试2次则终止并报告损坏情况

## html文件处理
### index.js请求处理
- 将原本的`<script src="index.js"></script>`改为`<script src="index.js.br"></script>`
### pck和wasm请求处理
- 在加载 Godot 配置前新增了浏览器 fetch 重定向：当请求`index.pck`,`index.wasm`文件时，分别改为请求`index.pck.br`,`index.wasm.br`，以加载 Brotli 压缩资源
### html结果检查
- 确认HTML已经请求`index.js.br`
- 确认fetch重定向只存在一次
- 确认`index.pck`重定向到`index.pck.br`
- 确认`index.wasm`重定向到`index.wasm.br`
- 确认Godot原有配置与启动逻辑未被修改

## 其他内容
- 其余 Godot 配置和启动逻辑保持不变
- 请基于这一差异检查资源命名、服务器响应头和兼容性风险

## 删除源文件
- 以上br文件检查和html文件检查均通过之后，删除`index.js`,`index.pck`,`index.wasm`文件