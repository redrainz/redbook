### 全文查询使您可以搜索已分析的文本字段，例如电子邮件的正文。使用在索引期间应用于字段的同一分析器来处理查询字符串。

---
1. intervals
   1. 为了更加简单灵活的控制查询时字符串在文本中匹配的距离与先后顺序，官方在es7.0引入了intervals query，用户可单一或者组合多个规则集合在某一个特定的text field上进行操作。
2. match
    1. 返回与提供的文本，数字，日期或布尔值匹配的文档。匹配之前分析提供的文本。match查询是用于执行全文搜索的标准查询，包括用于模糊匹配的选项。
3. match boolean prefix
4. match phrase
5. match phrase prefix
6. multi-match
7. common Terms Query
8. query string
9. simple query string