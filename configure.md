# 配置

Pomment 的配置文件存放在数据文件夹下的 `config.json`。你可以通过两种方法修改配置：

1. 通过 Pomment 的 [TUI](https://en.wikipedia.org/wiki/Text-based_user_interface) 调整配置（需要系统安装有 whiptail 或 dialog）。在第一次安装时，**如果使用的是交互式 shell**，将会弹出该界面以便进行首次配置；在日后，也可以通过 `pomment-config 你的目录名称` 启动配置界面。
2. 直接使用文本编辑器修改 `config.json`。

## 配置项介绍

### 站点信息 (Site Information)

| 变量名 | 介绍 | 默认值 |
| - | - | - |
| `apiHost` | 服务端使用的域名 | `127.0.0.1` |
| `apiPort` | 服务端使用的 IP 地址 | `5005` |
| `underProxy` | 服务端是否在反代服务器下运行。设置正确的目的是为了在日志中显示正确的评论者 IP 地址 | `false` |

### 管理员信息 (Admin)

| 变量名 | 介绍 | 默认值 |
| - | - | - |
| `siteAdmin/name` | 管理员的昵称 | 略 |
| `siteAdmin/email` | 管理员的电子邮件地址 | 略 |

### 访客提醒设置 (Guest Notifiation)
| 变量名 | 介绍 | 默认值 |
| - | - | - |
| `mode` | 评论模式。<br>`0`：不发送任何提醒<br>`1`：向访客发送电子邮件（通过 SMTP 方式）<br>`2`：执行 Webhook | `0` |
| `smtpSender` | SMTP 发信人 | `"Alice" <foo@example.com>` |
| `smtpHost` | SMTP 服务器域名 | 略 |
| `smtpPort` | SMTP 服务器端口 | 略 |
| `smtpUsername` | SMTP 服务器用户名 | 略 |
| `smtpPassword` | SMTP 服务器密码 | 略 |
| `smtpSecure` | 通过 TLS/SSL 方式安全连接 SMTP 服务器 | `false` |
| `title` | 邮件标题。模板书写规则请见 邮件模板。 | `[YOUR_SITENAME] {{name}}, you got a new reply!` |

| 变量名 | 介绍 | 默认值 |
| - | - | - |
| `` |  | `` |