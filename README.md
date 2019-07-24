# Pomment Document

Pomment 的 [文档](https://pomment.org/#!doc) 数据。

## 文档结构

文档的目录存放在 `content.json` 中：

```json
{
    "分类一": {
        "文档一（值为相对于本 repo 的 markdown 文件名，不需要写扩展名）": "test",
        "文档二": "sub_dir/test",
        "文档三": "sub_dir/test2"
    },
    "分类二": {
        "文档一": "test2",
        "文档二": "sub_dir/test3",
        "文档三": "sub_dir/test4"
    },
    "以此类推……": {
    }
}
```
