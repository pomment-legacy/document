# 配置

Pomment 的配置文件存放在数据文件夹下的 `config.yaml`。

## 示例配置文件

```yaml
# HTTP 服务监听的 IP 地址
apiHost: 127.0.0.1
# HTTP 服务监听的端口号
apiPort: 8080
# HTTP 服务被实际访问的网址，不要以 / 结尾
apiURL: 'https://example.com'

# 管理员信息
siteAdmin:
  # 管理员的昵称
  name: alice
  # 管理员的 Email
  email: alice@example.com
  # 管理员的密码，以 sha512 的形式存储
  password: blahblah

# reCPATCHA v3 设置
reCAPTCHA:
  # 是否启用 reCAPTCHA v3 验证
  enabled: false
  # reCAPTCHA v3 的 Secret Key
  secretKey: blahblahblahblahblahblah
  # 通过验证所需的最低分数
  minimumScore: 0.1

# 访客提醒设置
guestNotify:
  # 当访客收到评论回复，且明确同意接收电子邮件时，就会向其发送提醒邮件。目前支持以下方式：
  # - none: 不启用提醒访客功能
  # - smtp: 通过 SMTP 发送提醒邮件
  # - mailgun: 通过 Mailgun API 发送提醒邮件

  mode: smtp
  # 电子邮件标题
  title: ''
  # 电子邮件的发送者
  smtpSender: '"世界上最好的博客" <noreply@example.com>'

  # ========== 以下只有使用 smtp 模式才需要配置 ==========
  # SMTP 服务器地址
  smtpHost: smtp.example.com
  # SMTP 服务器端口
  smtpPort: 587
  # SMTP 用户名
  smtpUsername: postmaster
  # SMTP 密码
  smtpPassword: 12345678
  # 通过加密方式连接到 SMTP 服务器
  smtpSecure: false

  # ========== 以下只有使用 mailgun 模式才需要配置 ==========
  # Mailgun API 密钥
  mailgunAPIKey: ''
  # Mailgun 域名
  mailgunDomain: ''

# webhook 设置
webhook:
  # 启用 webhook
  enabled: false
  # webhook 地址列表
  targets: []
```