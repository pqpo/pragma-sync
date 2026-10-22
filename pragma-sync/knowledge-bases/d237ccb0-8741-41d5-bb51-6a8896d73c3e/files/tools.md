# 工具用法与回执

## 列表

- 列表只返回元数据（id、描述、trigger、revision）与各 namespace 的 itemCount，不含正文。
- 用较小的 limit 分页浏览，需要正文时再单独读取。

## 搜索

- 路径搜索为字面匹配且只返回路径；目录前缀（如 `episodic`）不会命中，需用文件名片段（如 `summary.md`）。
- 内容搜索返回带行号的片段，可用 contextLines 与 maxResults 收紧结果。
- 先搜索定位再读取，避免盲目读取整批条目。

## 读取

- 读取支持 start/offset 字节切片，返回 contentRange、nextStart 与 continuation，可按需续读。
- 大文档分段读取，只读当前判断所需的部分。

## 编辑

- 只传变更片段：search_replace 做精确替换，append/prepend 在已有内容前后追加；append/prepend 必须显式指定 separator。
- 整篇 replace 仅用于确知需要重写的条目。
- 携带 expectedRevision/expectedEtag 做乐观并发控制；发生冲突后先重读，再基于最新值修改。
- 回执紧凑：只返回 status、revision、sizeBytes 或 replacementCount，不回显正文，无需再读全文确认。

## 新增与删除

- 新增条目需提供完整正文与元数据，内容以 Markdown 编写。
- 删除用于清理不再需要的条目；删除后可用列表复核结果。
