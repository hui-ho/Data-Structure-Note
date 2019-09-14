# 索引查找（三）：倒排索引

百度、Google等搜索引擎为我们日常查找信息带来了巨大的方便，你是否思考过搜索引擎是如何从海量 HTML 文档中通过关键词查找资源的？今天给大家介绍最简单，也是最基础的搜索引擎技术 —— 倒排索引。

有倒排索引，就有正向索引，正向索引指的是通过文档 ID 找到对应的文档，如果通过文档ID查找对应文档，再在文档中匹配关键词，意味着要扫描所有文档，最后还要排序，对于互联网上的海量资源来说，显然是不可取的。

所以搜索引擎反其道行之，通过分析每个文档，提取其中的关键字，并建立关键词与文档 ID 的映射关系，每个关键词都对应着多个文档 ID。由于不是通过文档来确定属性（这里的属性是关键词），而是通过属性来确定文档，故而将其称作倒排索引。

倒排索引在很多开源搜索工具中，也有应用，比如 Elasticsearch、Lucene 等。