# Pomment

Pomment 是一种『刚好够用』的静态博客评论框解决方案。

## 初衷

静态博客越来越流行，但市面上一直 [缺少一种『刚好够用』的静态博客评论框解决方案](https://www.tcdw.net/post/pomment-brainhole/)：不是访客评论麻烦，就是功能过于简单或臃肿。

## 特性

### 简单粗暴

对于访客来说，Pomment 几乎没有学习门槛，访客不需要了解为什么他们的评论会出现在『奇怪』的 GitHub 仓库的 issues 栏目里，也不需要任何认证过程，直接输入自己的个人信息即可开始评论。

### 支持 Gravatar 头像

Pomment 提供原生的 [Gravatar](https://en.gravatar.com/) 支持，访客只需输入正确的邮箱地址，即可显示出自己的头像。

网站管理者亦可使用 [Libravatar](https://www.libravatar.org/) 等其它头像托管服务，只要其兼容 Gravatar 的 URL 格式。

### 支持留下自己的个人主页地址

如果访客填写自己的个人主页地址，则点击其昵称，即可链接到相对应的站点或页面。

### 邮件通知

只要访客勾选『接收邮件提醒』，当有其它人回复评论时，系统会通过 SMTP 或 Mailgun API 发送邮件提醒；如果不希望接收邮件提醒，也可以通过邮件内的退订链接取消接收。

### reCAPTCHA v3 支持

Pomment 拥有内置 [reCAPTCHA v3](https://developers.google.com/recaptcha/docs/v3) 支持。该功能可自主选择开启或关闭，只需填入申请好的 reCAPTCHA Key，即可正常工作。

### 方便的数据导入 / 导出

Pomment 数据存储使用的是标准的 JSON，可以轻松的实现数据的导入、导出及转换。

### 自行部署

Pomment 可以被自行部署在独立服务器、VPS、应用平台等环境，站长拥有充分的控制权。

## 缺点

### 需要后端

正是由于需要自行部署后端服务，站长需要自行解决 Pomment 的托管方案（选择合适的 VPS、应用平台等）。这对于已经不再自行部署后端的静态博客来说，可能是一个问题。