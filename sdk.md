# SDK

对于不想使用官方前端的用户，Pomment 提供了一套 SDK，可以让您开发属于您自己的前端。

## 安装

```bash
npm install pomment-sdk
```

## 使用

```javascript
import Pomment from 'pomment-sdk';
```

## 方法

### `new Pomment({ server, defaultURL, defaultTitle })`

| 值名 | 类型 | 必须项 | 简介 |
| - | - | - | - |
| `server` | `String` | 是 | Pomment 服务器地址，不以斜杠结尾 |
| `defaultURL` | `String` | 否 | 本页 URL。如果不指定，则依次尝试读取 [Canonical link element](https://en.wikipedia.org/wiki/Canonical_link_element) 值和该页面实际 URL |
| `defaultTitle` | `String` | 否 | 本页标题。如果不指定，则默认使用在 `<title>` 标签中指定的标题 |

