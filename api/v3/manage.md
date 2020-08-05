# 管理 API

## 验证

密码在后端以 sha512 密文形式存储。

### 认证

本页列出的所有 API 都需要附带一个名为 `auth` 的对象，内容为：

```javascript
{
    "time": 当前时间,
    "token": hmacSha512({ message: 当前时间, sign: sha512(明文密码) })
}
```

其中：

* 『当前时间』格式以 Java 时间戳表示（即 Unix 时间戳乘以 1000）。
* 误差不超过 60 秒。
* 程序内部设置一个队列存放已经用过的时间戳（如果用过则不能再使用）。超过容忍误差的时间戳将被清理。

## 列出评论串列表

地址：`/v3/manage/threads`

### 提交参数

为 JSON 格式，具体信息如下：

| 参数名 | 类型 | 必需 | 说明 |
| - | - | - | - |
| `auth` | `Auth` | 是 | 详见 [认证](#认证) 一节 |

### 返回参数

返回一个列表，列表中每项中的参数如下：

| 参数名 | 类型 | 说明 |
| - | - | - |
| `title` | `string` | 评论串的标题 |
| `url` | `string` | 评论串的 URL |
| `amount` | `number` | 评论数量 |
| `latestPostAt` | `number` | 最后更新时间。以 Java 时间戳表示 |

## 列出评论（管理员版）

地址：`/v3/manage/post`

### 提交参数

为 JSON 格式，具体信息如下：

| 参数名 | 类型 | 必需 | 说明 |
| - | - | - | - |
| `auth` | `Auth` | 是 | 详见 [认证](#认证) 一节 |
| `url` | `string` | 是 | 评论串所对应的页面地址 |

### 返回参数

为 JSON 格式，具体信息如下：

| 参数名 | 类型 | 说明 |
| - | - | - |
| `url` | `string` | 评论串所对应的页面地址 |
| `locked` | `boolean` | 评论是否被锁定 |
| `attr/title` | `string` | 评论对应页面的标题 |
| `attr/latestPostAt` | `number` | 最后更新时间。以 Java 时间戳表示 |
| `attr/amount` | `number` | 评论数量 |
| `content[]/id` | `integer` | 评论在数据库中的 ID |
| `content[]/name` | `string` 或 `null` | 评论者的昵称。如果昵称为 `null`，则该用户进行了匿名发言。 |
| `content[]/email` | `string` 或 `null` | 评论者留下的电子邮箱地址 |
| `content[]/website` | `string` 或 `null` | 评论者留下的个人主页地址 |
| `content[]/parent` | `number` | 该评论回复的已有的其它评论的 ID。如果没有回复已有的其它评论，则为 `-1` |
| `content[]/content` | `string` | 评论内容 |
| `content[]/hidden` | `boolean` | 是否被隐藏 |
| `content[]/byAdmin` | `boolean` | 是否为管理员发布 |
| `content[]/receiveEmail` | `boolean` | 是否接收邮件提醒 |
| `content[]/editKey` | `string` | 访客使用的评论修改 / 删除密钥 | |
| `content[]/createdAt` | `integer` | 评论发布的日期。以 Java 时间戳表示 |
| `content[]/createdAt` | `integer` | 评论最后修改的日期。以 Java 时间戳表示 |
| `content[]/origContent` | `string` | 最初版本的评论内容 |
| `content[]/avatar` | `string` 或 `null` | 访客的头像 URL 地址。如果值不为 null，则在访客一端优先展示该值指定的头像。<br>这是一个**不允许**访客自行指定的值，该字段存在的目的是为了更好的处理**从其它评论系统导入的评论**所**附带**的访客头像。 |
| `content[]/rating` | `number` 或 `null` | 评论的 reCAPTCHA 评分。如果没有开启 reCAPTCHA 或通过管理员通道发表，则为 `null` |

## 回复评论

## 设置评论隐藏状态
