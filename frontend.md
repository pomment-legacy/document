# 官方前端

对于不打算自行开发访客前端的用户，Pomment 也提供了官方访客前端（客户端）。服务端部署完成以后，你可以直接将它插入到你的网站上。

同时，该组件基于 [ef.js](https://ef.js.org) 实现，可单独使用或用于已有的 ef.js 项目中。

## 安装

### 直接引用到已有页面中

1. 获取编译好的 Pomment 前端文件。
    * 我们建议直接从 [jsDelivr](https://www.jsdelivr.com/package/npm/pomment-frontend?path=dist) 等服务引用它们，这样如果你的网站和其它网站同时引用了这个版本，访客访问两个站点时的加载速度将得到改善。
    * 你也可以自行编译一份：
        ```bash
        git clone https://github.com/pomment/frontend pfbuild
        cd pfbuild
        npm install
        npm run build
        ```
        编译好的 CSS 与 JS 将出现在 `dist` 目录下。
2. 在页面引用相应的 CSS 与 JS。
3. 在**相应引用的后面**添加以下代码：
    ```html
    <script>
    var plugin = new PommentWidget({
        // plugin 的设置。具体请见下面『配置项』一节。
    });
    plugin.$mount({
        target: document.getElementById("main"), // 要将挂件插入到哪个元素中？
    });
    plugin.load();
    </script>
    ```

### 引用到其它 ef.js 项目中

```bash
npm install pomment-frontend
```

```javascript
import PommentWidget from 'pomment-frontend';

const plugin = new PommentWidget({
    // ...
});
someElement.comment = plugin;
```

## 配置项

```javascript
const plugin = new PommentWidget(props);
```

`props` 是一个 object，可用键值如下：

| 值名 | 类型 | 介绍 | 必须项 |
| - | - | - | - |
| `server` | string | Pomment 服务器地址 | 是 |
| `url` | string | 本页 URL。如果不指定，则依次尝试读取 [Canonical link element](https://en.wikipedia.org/wiki/Canonical_link_element) 值和该页面实际 URL | 否 |
| `title` | string | 本页标题。如果不指定，则默认使用在 `<title>` 标签中指定的标题 | 否 |
| `adminName` | string | 管理员昵称（用于统一拥有 `byAdmin` 属性的评论的评论者信息） | 否 |
| `adminAvatar` | string | 管理员头像 URL（用于统一拥有 `byAdmin` 属性的评论的评论者信息） | 否 |
| `fixedHeight` | number | 页面已有的固定导航栏高度（单位为像素） | 否 |
| `avatarPrefix` | string | Gravatar 服务器地址，以 `/` 结尾。如 `https://secure.gravatar.com/avatar/` | 否 |
| `reCAPTCHA` | string | reCAPTCHA v3 网站密钥。如果留空，则不启用 reCAPTCHA 模式 | 否 |
| `showReceiveEmail` | boolean | 展示『发送邮件提醒』选项。如果设置隐藏，则访客提交的评论均默认为不展示 | 否 |

## 编译

```bash
npm run build
```

编译得到的 css 与 js 将出现在 dist 目录下。
