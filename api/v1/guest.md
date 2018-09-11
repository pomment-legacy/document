# 访客 API

* 除非特别说明，所有 HTTP 请求均使用 POST。
* 如果 `success` 为 `false`，则其它参数不会被返回。

## 获取系统信息

地址：`/`

### 提交参数

该 API 不需要提交参数。

### 返回参数

为 JSON 格式，具体信息如下：

| 参数名 | 类型 | 说明 |
| - | - | - |
| `success` | boolean | 请求是否成功 |
| `api_version` | number | API 版本。目前只有 `1`。 |

## 列出评论

地址：`/v1/list`

### 提交参数

为 JSON 格式，具体信息如下：

| 参数名 | 类型 | 必需 | 说明 |
| - | - | - | - |
| `url` | string | 是 | 评论串所对应的页面地址 |

### 返回参数

为 JSON 格式，具体信息如下：

| 参数名 | 类型 | 说明 |
| - | - | - |
| `success` | boolean | 请求是否成功 |
| `name` | string | 评论串所对应的页面地址 |
| `locked` | boolean | 评论是否被锁定 |
| `content` | array | 评论串内容 |

`content` 各项的具体信息如下：

| 每项参数名 | 类型 | 说明 |
| - | - | - |
| `id` | number | 评论在数据库中的 ID |
| `name` | string 或 null | 评论者的昵称。如果昵称为 `null`，则该用户进行了匿名发言，同时 `website` 与 `email_hashed` 将始终是 `null`。 |
| `website` | string 或 null | 评论者留下的个人主页地址 |
| `email_hashed` | string 或 null | 评论者留下的电子邮箱地址的 MD5 散列。该值用于在评论列表中展示评论者的 [Gravatar](https://gravatar.com/) 头像 |
| `parent` | number | 该评论回复的已有的其它评论的 ID。如果没有回复已有的其它评论，则为 `-1` |
| `birth` | string | 评论发布的日期。以 [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) 格式表示 |
| `content` | string 或 null | 评论内容 |
| `by_admin` | boolean | 是否为管理员发布 |

#### 示例

```bash
curl \
    -H "Content-Type: application/json" \
    -X POST \
    -d '{url: "https://www.tcdw.net/post/first-theme-release/"}' \
    https://www.example.com/v1/list
```

```json
{
    "success": true,
    "name": "https://www.tcdw.net/post/first-theme-release/",
    "locked": false,
    "content": [
        {
            "id": 1,
            "name": "qwe7002",
            "website": "https://qwe7002.com",
            "parent": -1,
            "birth": "2018-06-02T10:45:52.906Z",
            "content": "好耶！不过要加入silverblog的主题列表么（",
            "by_admin": false,
            "email_hashed": "829e35ddb6a7ea0f8f172284efab090f"
        },
        {
            "id": 2,
            "name": "tcdw",
            "website": null,
            "parent": 1,
            "birth": "2018-06-02T11:02:22.031Z",
            "content": "其实这玩意最早就是做的 SilverBlog 版。。\n只是仓库什么的太难看了，我还在整理，大概一两天就会面世了（",
            "by_admin": true,
            "email_hashed": "70ae2023afad30dae905344325cece8f"
        }
    ]
}
```