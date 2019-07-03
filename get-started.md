# 部署

如果需要使用 Pomment 评论系统，首先需要部署服务端。我们以 Ubuntu 18.04 LTS 为例，讲解部署过程。

## 过程

### 为服务端建立单独的新用户（推荐）

```bash
adduser pomment
su pomment
cd ~
```

### 安装 Node.js

我们推荐使用 [n](https://github.com/tj/n) 管理你的 Node.js 版本，并通过 [n-install](https://github.com/mklement0/n-install) 安装：

```bash
curl -L https://git.io/n-install | bash
```

然后安装最新的 Node.js LTS 版本：

``` bash
n lts
```

n 与通过 n 安装的 Node.js 均属于用户态应用，因此你不需要担心污染系统全局环境。

### 安装 Pomment 服务端

```bash
npm install -g pomment-backend
```

如果安装成功，你应该会看到类似这样的输出：

```
/usr/local/bin/pomment-init -> /home/pomment/n/lib/node_modules/pomment-backend/bin/pomment-init
/usr/local/bin/pomment-config -> /home/pomment/n/lib/node_modules/pomment-backend/bin/pomment-config
/usr/local/bin/pomment-server -> /home/pomment/n/lib/node_modules/pomment-backend/bin/pomment-server
+ pomment-backend@2.2.7
added 160 packages from 151 contributors in 23.45s
```

### 配置 Pomment

现在你可以输入命令 `pomment-init 你的目录名称`，开始初始化 Pomment 的数据文件夹了。

假如你在你的 `$HOME` 下，执行 `pomment-init data`，将会在 `/home/pomment/data` 下创建数据文件夹结构。

初始化完成以后，**如果使用的是交互式 shell**，程序会自动切换到基于 whiptail 或 dialog（视系统安装了哪一种而定）的设置界面，你可以在该菜单中调整你需要修改的参数（非交互式 shell 则将只生成配置文件）。如果以后需要重新调整配置，直接执行 `pomment-config 你的目录名称` 即可。

### 启动 Pomment

部署完成以后，你可以启动你的 Pomment 服务端了：

```bash
pomment-server 你的目录名称
```

此时的 Pomment 是在前台运行的。如果需要在后台持续运行，我们建议你通过 pm2、supervisor 等工具使其持续运行。

### 设置反代服务

Pomment 使用 Node.js 的 http 模块来提供 web 服务。如果需要在实际生产环境中使用，则需要反向代理。

以 nginx 为例：

```nginx
server {
    listen 80;
    server_name comment.example.com;
    location / {
        # 你的 Pomment 服务端的 host 和 port
        proxy_pass          http://127.0.0.1:4600;
        proxy_redirect      off;
        proxy_set_header    Host            $host;
        proxy_set_header    X-Real-IP       $remote_addr;
        proxy_set_header    X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header    Range           $http_range;
        proxy_set_header    If-Range        $http_if_range;

        # 如果你的 Pomment 服务端站点和主站点不在一个域名上，请务必设置 Access-Control-Allow-Origin 值为主站点地址，否则 AJAX 将不会工作！
        add_header          'Access-Control-Allow-Origin' 'https://example.com';
        add_header          'Access-Control-Allow-Credentials' "true";
        add_header          'Access-Control-Allow-Methods' 'GET, POST, OPTIONS, DELETE';
        add_header          'Access-Control-Allow-Headers' 'reqid, nid, host, x-real-ip, x-forwarded-ip, event-type, event-id, accept, content-type';
    }
}
```