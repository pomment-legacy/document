# 访客 API

* 除非特别说明，所有 HTTP 请求均使用 POST。
* 如果 `success` 为 `false`，则其它参数不会被返回。

## 列出评论

地址：`/v2/list`

### 提交参数

为 JSON 格式，具体信息如下：

| 参数名 | 类型 | 必需 | 说明 |
| - | - | - | - |
| `url` | `string` | 是 | 评论串所对应的页面地址 |

### 返回参数

为 JSON 格式，具体信息如下：

| 参数名 | 类型 | 说明 |
| - | - | - |
| `success` | `boolean` | 请求是否成功 |
| `url` | `string` | 评论串所对应的页面地址 |
| `locked` | `boolean` | 评论是否被锁定 |
| `content` | `array` | 评论串内容 |
| `content[]/id` | `integer` | 评论在数据库中的 ID |
| `content[]/name` | `string` 或 `null` | 评论者的昵称。如果昵称为 `null`，则该用户进行了匿名发言，同时 `website` 与 `email_hashed` 将始终是 `null`。 |
| `content[]/website` | `string` 或 `null` | 评论者留下的个人主页地址 |
| `content[]/emailHashed` | `string` 或 `null` | 评论者留下的电子邮箱地址的 MD5 散列。该值用于在评论列表中展示评论者的 [Gravatar](https://gravatar.com/) 头像 |
| `content[]/parent` | `number` | 该评论回复的已有的其它评论的 ID。如果没有回复已有的其它评论，则为 `-1` |
| `content[]/createdAt` | `string` | 评论发布的日期。以 [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) 格式表示 |
| `content[]/content` | `string` | 评论内容 |
| `content[]/byAdmin` | `boolean` | 是否为管理员发布 |

如果数据库中没有所对应的评论串，则返回 `content` 为空，`name` 为用户提交的 `url` 的值，`locked` 为 `false` 的返回值。

## 提交评论

地址：`/v2/submit`

为 JSON 格式，具体信息如下：

| 参数名 | 类型 | 必需 | 说明 | 最大 UTF-8 字节数 |
| - | - | - | - | - |
| `title` | `string` | 是 | 要评论的文章的标题 | |
| `url` | `string` | 是 | 要评论的文章的 URL | |
| `parent` | `string` | 否 | 要回复的已有的评论 ID。如果是发布一篇新评论则不应当提交该参数 | |
| `name` | `string` | 否 | 评论作者的昵称。如果不指定，则会被认为是匿名评论 | 32 |
| `email` | `string` | 是 | 评论作者的电子邮箱地址，用来展示 Gravatar 头像与接收提醒邮件（如果 `receiveEmail` 为 `true`）。<br>匿名评论也需要提交该参数，但其电子邮箱地址的 MD5 值将不会被公开输出。 | 255 |
| `website` | `string` | 否 | 评论作者的个人主页。<br>匿名评论可以提交该参数，但个人主页地址将不会被公开输出。 | 64 |
| `content` | `string` | 是 | 评论内容。 | 2048 |
| `receiveEmail` | `boolean` | 是 | 是否在评论得到回复时接收电子邮件提醒。 | |
| `responseKey` | `string` | 是 / 不允许 | reCAPTCHA v3 的验证结果密钥。<br>如果 API 服务端指定开启 reCAPTCHA v3 验证，则必须提交有效值；反之，不允许提交该参数。 | |

### 返回参数

为 JSON 格式，具体信息如下：

| 参数名 | 类型 | 说明 |
| - | - | - |
| `success` |  `boolean` | 请求是否成功 |
| `coolDownTimeout` |  `integer` | 发布该评论后需要等待的冷却时间，长度为秒。<br>如果 API 服务端指定不需要冷却，值则为 0 及以下。 |
| `content` |  `object` | 刚才提交的评论详情 |
| `content/id` |  `integer` | 评论在数据库中的 ID |
| `content/parent` |  `integer` | 该评论回复的已有的其它评论的 ID。如果没有回复已有的其它评论，则为 `-1` |
| `content/createdAt` |  `string` | 评论发布的日期。以 [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) 格式表示 |
| `content/editToken` |  `string` | 用于编辑或删除该评论的密钥 |
| `content/editTimeout` |  `integer` | 用于编辑或删除该评论的密钥的过期时间，长度为秒。<br>如果 API 服务端指定密钥不会过期，值则为 0 及以下。 |
| `content/name` |  `string` 或 `null` | 评论者的昵称。如果昵称为 `null`，则该用户进行了匿名发言 |
| `content/email` |  `string` | 评论者留下的电子邮箱地址 |
| `content/website` |  `string` 或 `null` | 评论者留下的个人主页地址 |
| `content/content` |  `string` | 评论内容 |

## 编辑评论

地址：`/v2/edit`

为 JSON 格式，具体信息如下：

| 参数名 | 类型 | 必需 | 说明 | 最大 UTF-8 字节数 |
| - | - | - | - | - |
| `url` | `string` | 是 | 要修改的评论所在的文章的 URL | |
| `id` | `integer` | 是 | 要修改的评论的 ID | |
| `token` | `string` | 是 | 评论的修改 / 删除密钥 | |
| `content` | `string` | 是 | 评论内容 | 2048 |

### 返回参数

为 JSON 格式，具体信息如下：

| 参数名 | 类型 | 说明 |
| - | - | - |
| `success` |  `boolean` | 请求是否成功 |

## 删除评论

地址：`/v2/delete`

为 JSON 格式，具体信息如下：

| 参数名 | 类型 | 必需 | 说明 |
| - | - | - | - | - |
| `url` | `string` | 是 | 要删除的评论所在的文章的 URL |
| `id` | `integer` | 是 | 要删除的评论的 ID |
| `token` | `string` | 是 | 评论的修改 / 删除密钥 |

### 返回参数

为 JSON 格式，具体信息如下：

| 参数名 | 类型 | 说明 |
| - | - | - |
| `success` |  `boolean` | 请求是否成功 |
