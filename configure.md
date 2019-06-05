# 配置

Pomment 的配置文件存放在数据文件夹下的 `config.json`。你可以通过两种方法修改配置：

1. 通过 Pomment 的 [TUI](https://en.wikipedia.org/wiki/Text-based_user_interface) 调整配置（需要系统安装有 whiptail 或 dialog）。在第一次安装时，**如果使用的是交互式 shell**，将会弹出该界面以便进行首次配置；在日后，也可以通过 `pomment-config 你的目录名称` 启动配置界面。
2. 直接使用文本编辑器修改 `config.json`。

## 配置项介绍

### 站点信息 (Site Information)

| 变量名 | 介绍 | 数据类型 | 默认值 |
| - | - | - | - |
| `apiHost` | 服务端使用的域名 | string | `127.0.0.1` |
| `apiPort` | 服务端使用的 IP 地址 | number | `5005` |
| `underProxy` | 服务端是否在反代服务器下运行。设置正确的目的是为了在日志中显示正确的评论者 IP 地址 | boolean | `false` |

### 管理员信息 (Admin)

| 变量名 | 介绍 | 数据类型 | 默认值 |
| - | - | - | - |
| `siteAdmin/name` | 管理员的昵称 | string | 略 |
| `siteAdmin/email` | 管理员的电子邮件地址 | string | 略 |

### 访客提醒设置 (Guest Notifiation)

| 变量名 | 介绍 | 数据类型 | 默认值 |
| - | - | - | - |
| `guestNotify/mode` | 评论模式。<br>`0`：不发送任何提醒<br>`1`：向访客发送电子邮件（通过 SMTP 方式）<br>`2`：执行 Webhook | string | `0` |
| `guestNotify/smtpSender` | SMTP 发信人 | string | `"Alice" <foo@example.com>` |
| `guestNotify/smtpHost` | SMTP 服务器域名 | string | 略 |
| `guestNotify/smtpPort` | SMTP 服务器端口 | number | 略 |
| `guestNotify/smtpUsername` | SMTP 服务器用户名 | string | 略 |
| `guestNotify/smtpPassword` | SMTP 服务器密码 | string | 略 |
| `guestNotify/smtpSecure` | 通过 TLS/SSL 方式安全连接 SMTP 服务器 | boolean | `false` |
| `guestNotify/title` | 邮件标题。模板书写规则请见 邮件模板。 | string | `[YOUR_SITENAME] {{name}}, you got a new reply!` |

本栏目中，所有除 `guestNotify/mode` 以外的值，只会在 `guestNotify/mode` 为 1 时生效。这意味着如果使用其它 webhook 接收服务端来处理访客提醒，以上的配置信息不会被传输给 webhook 接收服务端，你需要对其进行单独配置。

### 安全设置

| 变量名 | 介绍 | 数据类型 | 默认值 |
| - | - | - | - |
| `reCAPTCHA/enabled` | 是否启用 reCAPTCHA v3 验证 | boolean | `false` |
| `reCAPTCHA/siteKey` | reCAPTCHA v3 siteKey | string | 略 |
| `reCAPTCHA/secretKey` | reCAPTCHA v3 secretKey | string | 略 |
| `reCAPTCHA/minimumScore` | 通过验证所需的最低 reCAPTCHA 分数 | number | `0.1` |