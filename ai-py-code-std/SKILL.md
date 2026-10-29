---
name: ai-py-code-std
description: 创建、修改、审查或重构 Python（.py）文件时调用
---

# ai-py-code-std

Python 全中文编码规范（AI 必须严格遵守）

## 强制规范
- Python 语言原生特殊文件保持用自己的命名，如`__init__.py`、`__main__.py`、`__pycache__`和内部 .pyc 字节码文件、`py.typed`
- Python原生内容则保持自己的命名方式，如`class`、`def`、`if`等
- 所有到进入的第三方库的调用，使用对应库内的接口名称，即使为英文
- 除上三条以外所有自定义名称（文件、变量、函数、类、方法、参数、模块）**必须用中文**，见名知意
- 注释、文档字符串也是用中文
- 常量：前缀 `常量_`，如 `常量_超时`。  
- 私有成员：以`_`开头，如 `_密钥`。 
- 缩进4空格
- 导入：标准库→第三方→本地，用 `as` 起中文别名，格式为对应库中文名+`_库`。
- 异常消息使用中文，如 `raise ValueError("金额无效")`。
  
## 注释规范
- 复杂代码段使用一句话注释讲清楚功能，其他情况使用纯中文命名来讲清楚功能



## 示例
```python
"""用户管理模块"""
from typing import List
import numpy as 数值计算_库

常量_最大失败次数 = 5

class 用户:
    def __init__(self, 姓名: str, 邮箱: str, 年龄: int):
        self.姓名 = 姓名
        self.邮箱 = 邮箱
        self.年龄 = 年龄
        self._失败次数 = 0

    def 验证登录(self, 密码: str) -> bool:
        if self._失败次数 >= 常量_最大失败次数:
            raise PermissionError("账户已锁定")
        return True

def 获取活跃用户(用户列表: List[用户], 最小年龄: int) -> List[用户]:
    return [u for u in 用户列表 if u.年龄 >= 最小年龄]
```