# CrazyGames网页打包处理

## 用途与范围

1. 本文用于处理Godot导出的网页包。
2. 目标是压缩资源并适配加载路径。
3. 本文不处理运行时掉帧问题。
4. 本任务只压缩资源并调整HTML加载。
5. 保留既有SDK、性能修复和页面功能。

## 文件确认

1. 确认当次导出包含以下四个文件。
   - `index.html`
   - `index.js`
   - `index.pck`
   - `index.wasm`
2. 缺少任一文件时，停止并报告缺失项。
3. 使用当次导出的JS、WASM和PCK。
4. 保留当次生成的引擎配置和文件尺寸。
5. 不复制旧包的引擎文件或压缩资源。
6. 仅有压缩包时，不将其视为新导出。

## Brotli压缩处理

1. 使用Brotli压缩JS、PCK和WASM。
2. 压缩参数使用`-q 11`。
3. 每次均从当次原文件重新压缩。
4. 已有同名`.br`文件不能作为跳过依据。
5. 先输出临时文件，验证后替换旧压缩包。
6. 压缩阶段总时限为5分钟。
7. 超时或失败时，停止并报告具体文件。
8. 失败时，不将部分产物标记为可交付。
9. 解压比对须确认内容与原文件一致。
10. 三个压缩包全部通过后，再调整HTML。
11. 原文件保留至全部验证完成。
12. 验证完成后，移除三个未压缩原文件。

## HTML文件处理

1. 将引擎脚本路径改为`index.js.br`。
2. 保持引擎配置中的逻辑文件名不变。
3. 不给配置中的WASM和PCK名称追加`.br`。
4. 仅在请求层重定向WASM和PCK路径。
5. 在引擎开始加载资源前安装下列适配。
6. 已有等效适配时，复用现有实现。
7. 重复执行时，不重复插入脚本。
8. 无法定位加载入口时，停止并报告。
9. 不用旧HTML覆盖当次导出的配置。
10. 不修改版本号文字来冒充新构建。

```html
<script src="index.js.br"></script>
<script>
// 保持逻辑文件名，仅调整网络请求路径。
(function () {
	const marker = Symbol.for('godot.web.crazygames-brotli');
	if (window.fetch[marker]) {
		return;
	}
	const originalFetch = window.fetch.bind(window);
	const fetch = function (resource, options) {
		if (typeof resource === 'string') {
			resource = resource
				.replace(/(^|\/)index\.wasm(?=([?#]|$))/, '$1index.wasm.br')
				.replace(/(^|\/)index\.pck(?=([?#]|$))/, '$1index.pck.br');
		}
		return originalFetch(resource, options);
	};
	Object.defineProperty(fetch, marker, { value: true });
	window.fetch = fetch;
})();
// 此后保留当次导出的引擎配置和启动代码。
</script>
```

11. 上述适配仅重写字符串形式的请求。
12. 它不改写URL对象或Request对象。
13. 若实际请求使用对象，先核查现有加载方式。
14. 不把此示例直接当作完整HTML模板。

## 最小验证与交付

1. 确认三个压缩包均通过解压比对。
2. 确认HTML只加载一次引擎脚本。
3. 确认请求适配位于资源加载之前。
4. 确认既有SDK和性能修复仍然保留。
5. 在目标托管环境检查资源请求。
6. 确认三个`.br`资源均成功加载。
7. 确认响应使用正确的Brotli编码头。
8. 检查控制台中的加载和解压错误。
9. 确认游戏进入可操作场景。
10. 未做浏览器验证时，注明尚未验证。
11. 本地加载通过不等于CrazyGames验收通过。
12. 压缩成功不等于触屏或帧率验收通过。
13. 交付时报告压缩结果和验证范围。

## 相关问题

1. 图形查询掉帧见[网页游戏掉帧原因与修复指南](网页游戏掉帧原因与修复指南.md)。
2. 触屏输入掉帧见[Godot网页触屏掉帧复盘与规避指南](Godot网页触屏掉帧复盘与规避指南.md)。
