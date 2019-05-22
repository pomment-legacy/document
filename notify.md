# 消息提醒设置

你可以使用多种途径提醒访客。

## 0: 不启用

不启用任何评论提醒服务；程序不会试图向访客发送任何提醒。

## 1：发送电子邮件（SMTP）

### 模板语法

`{{函数名}}`：在渲染邮件内容时，会自动替换为**经过转义**的变量值。

### 可用变量

* `title`：评论串所在页面的标题
* `url`：评论串所在页面的 URL
* `parent:name`：原评论中评论者填写的昵称
* `parent:website`：原评论中评论者填写的个人主页
* `parent:content`：原评论中评论者填写的内容。本变量的所有换行符会被转义成 HTML 的 `<br>` 标签
* `name`：回复者填写的昵称
* `website`：回复者填写的个人主页
* `content`：回复者填写的内容。本变量的所有换行符会被转义成 HTML 的 `<br>` 标签
* `unsubscriber`：退订链接（`/unsubscribe/:thread/:id/:editKey`）。你需要自行在邮件模板中添加实际 API 服务端地址，如：  
`<a href="https://example.com/{{unsubscriber}}" target="_blank">Unsubscribe</a>`
