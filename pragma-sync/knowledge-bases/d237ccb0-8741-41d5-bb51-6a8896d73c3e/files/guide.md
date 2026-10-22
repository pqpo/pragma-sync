# Context Store 省 token 使用规范

Expert Context Store 工具的实操规范。目标是少读、少写、少回显，同时让条目可被正确发现。

## 适用场景

- 查询、读取、编辑或新建 Context Store 条目
- 评估记忆条目的上下文 token 成本
- 决定新条目应放在哪个命名空间

## 基本约定

- 用户使用简体中文交流，条目正文使用简体中文；工具名、命名空间与 id 保留英文原文。
- 用户关注 token 效率，优先选择返回信息更少、可续读或可增量修改的调用方式。

## 低 token 工作流

1. 枚举：用较小 limit 的列表调用，只取元数据（id、描述、trigger、revision）与各 namespace 的 itemCount。
2. 定位：用搜索缩小范围，再读取命中的具体条目，避免全量浏览。
3. 读取：需要正文时按字节切片读取并按需续读，不整篇加载。
4. 写入：用片段编辑并携带最新 revision/etag，避免整篇替换。
5. 复用：再次修改同一条目前重新读取以获得最新 revision/etag，不使用过期令牌。

## 导航

- `tools.md`：列表、搜索、读取、编辑各工具的低 token 用法与回执语义。
- `write-policy.md`：可写命名空间、memory 只读约束与 id 后缀要求。
- `loading-cost.md`：trigger 的预载成本与选择建议。
