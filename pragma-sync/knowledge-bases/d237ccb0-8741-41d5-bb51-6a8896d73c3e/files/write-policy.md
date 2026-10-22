# 写入约束

## 只能写入已配置的命名空间

- Context Store 只接受已配置的命名空间（如 memory、mission-board、pragma.handoff）。
- 自行创建命名空间会导致 store_unavailable 失败，系统不会隐式创建。

## memory 为只读

- 按 Memory Guide，memory 命名空间只读，禁止新增、编辑或删除。
- 需要写入演示时使用可写的私有命名空间（如 mission-board-private），并在测试后删除条目、恢复原状。

## 带 metadata 的条目 id 必须以 .md 结尾

- Context Store 中带 metadata 的条目，其 id 必须以 `.md` 结尾，否则 metadata 不受支持。
- 新建条目时先确定 `.md` 后缀，再写入正文与元数据。
