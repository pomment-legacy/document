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
