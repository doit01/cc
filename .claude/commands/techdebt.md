---
description: 扫描并记录技术债务
---

请执行以下步骤：
1. 运行 `npm run lint` 和 `npm run type-check`
2. 搜索 `console.log`、`any`、`TODO` 注释
3. 列出所有没有try-catch的异步函数
4. 生成表格：优先级 | 文件:行号 | 问题描述 | 建议修复