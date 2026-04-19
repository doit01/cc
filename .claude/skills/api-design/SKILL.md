---
description: 当设计REST API端点时触发
---

## 标准响应格式
成功: HTTP/1.1 200 
Content-Type: application/json
{
   result 
}

失败: HTTP/1.1 403 Forbidden
Content-Type: application/json

{
    "code": "INSUFFICIENT_PERMISSIONS",
    "message": "您需要管理员权限才能删除此用户。"
}

## 命名规范
- GET /todos - 列表
- POST /todos - 创建
- PUT /todos/:id - 全量更新
- PATCH /todos/:id - 部分更新

## 分页参数
?page=1&limit=20&sortBy=createdAt&order=desc

## Gotchas（常见错误）
- ❌ 不要返回数据库原始错误给客户端
- ❌ 不要使用数字作为状态码（用HTTP标准码）
- ✅ 始终验证UUID格式的:id参数