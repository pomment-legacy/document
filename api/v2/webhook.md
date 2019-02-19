# Webhook

Pomment 服务端提供 Webhook 支持，可以用于触发一些基于 Webhook 回调的事件。

## 基本内容

为 JSON 格式，具体信息如下：

| 参数名 | 类型 | 说明 |
| - | - | - |
| `event` | `string` | 事件名称 |
| `url` | `string` | 评论串所对应的页面地址 |
| `title` | `string` | 评论串所对应的页面名称 |
| `content` | `any` | 视 `event` 的内容而定 |

## 事件：`new_comment`

| 参数名 | 类型 | 说明 |
| - | - | - |
| `id` | `integer` | 评论在数据库中的 ID |
| `name` | `string` 或 `null` | 评论者的昵称。如果昵称为 `null`，则该用户进行了匿名发言，同时 `website` 与 `email_hashed` 将始终是 `null` |
| `email` | `string` | 评论作者的电子邮箱地址，用来展示 Gravatar 头像与接收提醒邮件（如果 `receiveEmail` 为 `true`） |
| `website` | `string` 或 `null` | 评论者留下的个人主页地址 |
| `parent` | `number` | 该评论回复的已有的其它评论的 ID。如果没有回复已有的其它评论，则为 `-1` |
| `content` | `string` | 评论内容 |
| `hidden` | `boolean` | 评论是否已经被隐藏（软删除） |
| `byAdmin` | `boolean` | 是否为管理员发布 |
| `receiveEmail` | `boolean` | 评论发布者是否愿意在评论得到回复时接收电子邮件提醒 |
| `editKey` |  `string` | 用于编辑或删除该评论的密钥 |
| `createdAt` | `integer` | 评论发布的日期。以 Java 时间戳表示 |
| `updatedAt` | `integer` | 评论最后编辑的日期，如果没有被编辑过则与 `createdAt` 相等。以 Java 时间戳表示 |
| `reCAPTCHAScore` | `float` 或 `null` | reCAPTCHA v3 的评分，范围从 0 到 1 |
| `parentContent` | `object` 或 `null` | 其所回复的评论的信息，结构与上一层相同，除了没有 `parentContent` 值 |
