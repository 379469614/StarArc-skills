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
- 只做以下两步修改
- 不要做过多的检查，只要指令有正确执行即可
- 导出包可以随时打包出来，不怕损坏，以效率和节省token为主

## Brotli压缩处理
- 使用Brotli压缩`index.js`,`index.pck`,`index.wasm`文件
- 压缩指令`-q 11`，压缩等级11级，不保留原文件的压缩方式
- 原先已有对应的`.br`文件的则不再执行该压缩
- 压缩时间限制为5分钟，超时则终止并报告情况

## html文件处理
将
```
		<script src="index.js"></script>
		<script>
```
替换为
```
		<script src="index.js.br"></script>
		<script>
// CrazyGames Brotli 适配：保持 Godot 的逻辑文件名不变，
// 仅在网络请求层把 WASM/PCK 重定向到对应的 .br 文件。
const originalFetch = window.fetch.bind(window);
window.fetch = function (resource, options) {
	if (typeof resource === 'string') {
		resource = resource
			.replace(/(^|\/)index\.wasm(?=([?#]|$))/, '$1index.wasm.br')
			.replace(/(^|\/)index\.pck(?=([?#]|$))/, '$1index.pck.br');
	}
	return originalFetch(resource, options);
};
```