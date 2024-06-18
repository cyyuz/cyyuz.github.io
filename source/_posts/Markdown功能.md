---
title: Markdown功能
date: 2024-06-18 15:01:23
tags: [markdown, html]
categories:
- [code, markdown]
---

# HTML表格

Markdown 本身不支持表格的单元格合并，但允许嵌入 HTML 代码实现更复杂的表格功能。

- 表格由 `<table>` 标签定义，行由 `<tr>` 标签定义，单元格由 `<th>` 或 `<td>` 定义， `<th>` 用于表头单元格，它们会以粗体显示， `<td>` 用于数据单元格。
- `colspan` 属性用于合并列。例如，`colspan="2"` 表示该单元格将横跨两列。
- `rowspan` 属性用于合并行。例如，`rowspan="2"` 表示该单元格将横跨两行。

以下是一个包含列合并和行合并的表格示例：

```html
<table>  
  <tr>  
    <th>表头1</th>  
    <th colspan="2">合并的表头2和表头3</th>  
  </tr>  
  <tr>  
    <td>数据1</td>  
    <td>数据2</td>  
    <td>数据3</td>  
  </tr>  
  <tr>  
    <td rowspan="2">跨两行数据1</td>  
    <td>数据4</td>  
    <td>数据5</td>  
  </tr>  
  <tr>  
    <!-- 注释：此行不需要第一个单元格，因为上面的单元格已经横跨了两行 -->  
    <td>数据6</td>  
    <td>数据7</td>  
  </tr>  
</table>
```