<div align="center">
  <br/>
  <a href="http://pm2.keymetrics.io" title="PM2 Keymetrics link">
    <img width=710px src="https://raw.githubusercontent.com/Unitech/pm2/master/pres/pm2-v4.png" alt="pm2 logo">
  </a>
  <br/>
<br/>
<b>P</b>(rocess) <b>M</b>(anager) <b>2</b>
<br/><br/>

 <a href="https://www.bithound.io/github/Unitech/pm2" title="Bithound PM2 score">
 <img src="https://www.bithound.io/github/Unitech/pm2/badges/score.svg" alt="bitHound Score">
</a>

<a href="https://www.npmjs.com/package/pm2" title="PM2 on NPM">
  <img alt="NPM Downloads" src="https://img.shields.io/npm/dm/pm2.svg?style=flat-square"/>
</a>

<a href="https://travis-ci.org/Unitech/pm2" title="PM2 Tests">
  <img src="https://travis-ci.org/Unitech/pm2.svg?branch=master" alt="Build Status"/>
</a>


<br/>
<br/>
<br/>
</div>

PM2 是具有内置负载平衡器的 Node.js 应用程序的生产进程管理器。它使您可以永久保持应用程序的活动状态，无需停机即可重新加载应用程序，并且可以使常见的系统管理任务更容易

在生产模式下启动应用程序非常简单：

```bash
$ pm2 start app.js
```

PM2 经过了[超过 1400 次测试](https://travis-ci.org/Unitech/pm2)。

官方网站： [http://pm2.keymetrics.io/](http://pm2.keymetrics.io/)

适用于 Linux（stable）＆ macOS（stable）＆ Windows（stable）。
从 Node.js 0.12 开始，所有 Node.js 版本都支持。

[![NPM](https://nodei.co/npm/pm2.png?downloads=true&downloadRank=true)](https://nodei.co/npm/pm2/)

## 安装 PM2

```bash
$ npm install pm2 -g
```

*当您安装 Node.js 时，npm 是一个内置的 CLI - [使用 NVM 安装 Node.js](https://keymetrics.io/2015/02/03/installing-node-js-and-io-js-with-nvm/)*

## 启动应用程序

```bash
$ pm2 start app.js
```

现在，您的应用程序已被守护，被监控并保持永久激活。

[更多关于进程管理](http://pm2.keymetrics.io/docs/usage/process-management/)

## 官方的 Docker 图像

Docker Hub PM2 image:

[PM2 Official Docker Image](https://hub.docker.com/r/keymetrics/pm2/)

使用 pm2-docker 命令行接口:

```
FROM keymetrics/pm2:latest
[...]
CMD [ "pm2-docker", "start", "ecosystem.config.js" ]
```

 更多 Docker/PM2 集成：
[pm2 Docker 支持](http://pm2.keymetrics.io/docs/usage/docker-pm2-nodejs/)

## 监控器 PM2 和 应用程序

要监控你的应用程序，只需键入:

```bash
$ pm2 register
```

[更多关于 PM2 监控](http://docs.keymetrics.io/)

## 更新 PM2

```bash
# 安装 PM2 的最新版本
$ npm install pm2@latest -g
# 保存进程列表，退出旧的 PM2 并恢复所有进程
$ pm2 update
```

*PM2 无缝更新*

## 主要特性

### 命令概述

```bash
# 常规
$ npm install pm2 -g            # 安装 PM2
$ pm2 start app.js              # 启动，后台运行并自动重启应用程序 (Node)
$ pm2 start app.py              # 启动，后台运行并自动重启应用程序 (Python)
$ pm2 start npm -- start        # 启动，后台运行并自动重启 Node 应用程序

# 集群模式 (仅限 Node.js )
$ pm2 start app.js -i 4         # 在集群模式下启动 4 个应用程序实例，它将为每个应用程序加载平衡网络查询（负载均衡）
$ pm2 reload all                # 0 秒停机重新加载
$ pm2 scale [app-name] 10       # 集群应用程序规模为 10 个集成

# 过程监控
$ pm2 list                      # 列出所有使用 PM2 启动的进程
$ pm2 monit                     # 显示每个应用程序的内存和 cpu 使用情况
$ pm2 show [app-name]           # 显示关于应用程序的所有信息

# 日志管理
$ pm2 logs                      # 显示所有应用程序的日志
$ pm2 logs [app-name]           # 显示指定应用程序的日志
$ pm2 logs --json               # JSON格式的日志
$ pm2 flush
$ pm2 reloadLogs

# 进程状态管理
$ pm2 start app.js --name="api" # 启动应用程序并命名为 “api”
$ pm2 start app.js -- -a 34     # 启动应用程序并传递选项 "-a 34" 作为参数
$ pm2 start app.js --watch      # 文件更改时，重启应用程序
$ pm2 start script.sh           # 启动 bash 脚本
$ pm2 start app.json            # 启动在 app.json 中声明的所有应用程序
$ pm2 reset [app-name]          # 重置所有计数器
$ pm2 stop all                  # 停止所有的应用程序
$ pm2 stop 0                    # 使用 id 0 停止所有 进程
$ pm2 restart all               # 重启所有应用程序
$ pm2 gracefulReload all        # 在集群模式下优雅地重新加载所有应用程序
$ pm2 delete all                # 杀死和删除所有应用程序
$ pm2 delete 0                  # 使用 id 0 删除所有应用程序

# Startup/Boot 管理
$ pm2 startup                   # 检测初始化系统，在启动时生成和配置pm2 boot
$ pm2 save                      # 保存当前进程列表
$ pm2 resurrect                 # 恢复以前保存的进程
$ pm2 unstartup                 # 禁用和移除启动系统

$ pm2 update                    # 保存进程，杀死 PM2 进程并恢复进程
$ pm2 generate                  # 生成一个样本 json 配置文件

# 部署
$ pm2 deploy app.json prod setup    # 设置 "prod" 远程服务器
$ pm2 deploy app.json prod          # 更新 "prod" 远程服务器
$ pm2 deploy app.json prod revert 2 # 使用 2 恢复 "prod" 远程服务器

# 模块系统
$ pm2 module:generate [name]    # 生成带有名称 [name] 的样例模块
$ pm2 install pm2-logrotate     # 安装模块 (这里是一个 log 循环系统)
$ pm2 uninstall pm2-logrotate   # 卸载模块
$ pm2 publish                   # 增加版本, git push 和 npm publish
```

### 进程管理

一旦应用程序启动，您就可以轻松地列出和管理它们:

![Process listing](https://github.com/unitech/pm2/raw/master/pres/pm2-list.png)

列出所有正在运行的进程：

```bash
$ pm2 list
```

管理进程是很简洁明了的：

```bash
$ pm2 stop     <app_name|id|'all'|json_conf>
$ pm2 restart  <app_name|id|'all'|json_conf>
$ pm2 delete   <app_name|id|'all'|json_conf>
```

为了确保它对 `json_conf` 中声明的环境变量进行重新计算，可以将其作为参数传递，并且可以从 `json_conf` 中选择自定义的 `env` 名称：

```bash
$ pm2 restart <json_conf> [--env <env_name>]
```

获得关于指定进程的更多细节:

```bash
$ pm2 describe <id|app_name>
```

[更多关于进程管理](http://pm2.keymetrics.io/docs/usage/process-management/)

### 负载平衡 & 0 秒停机重新加载

当应用程序使用 `-i <instance_number> ` 选项启动时，**集群模式** 是被启用的。

集群模式启动了您的应用程序的 `<instance_number>` 实例，并在每个实例之间自动负载平衡 HTTP/TCP/UDP。这允许根据可用 CPU 的数量来增加总体性能。

所有主要节点的无缝支持。js框架和任何节点。js应用程序不需要任何代码更改:

所有主流的  Node.js 框架和任何  Node.js 应用程序都无缝支持，不需要更改任何代码

![Framework supported](https://raw.githubusercontent.com/Unitech/PM2/development/pres/cluster-support.png)

主要命令:

```bash
$ pm2 start app.js -i max  # 启用负载平衡器并启动 'max' 实例(cpu nb)

$ pm2 reload all           # 0 秒停机重新加载

$ pm2 scale <app_name> <instance_number> # 增加/减少 进程数量
```

[更多关于 PM2 如何使集群变得容易的信息](https://keymetrics.io/2015/03/26/pm2-clustering-made-easy/)

### CPU / Memory 监控

![Monit](https://github.com/Unitech/pm2/raw/master/pres/pm2-monit.png)

监控所有进程启动:

```bash
$ pm2 monit
```

### 日志设施

![Monit](https://github.com/unitech/pm2/raw/master/pres/pm2-logs.png)

实时显示指定进程或所有进程的日志。标准的、原始的、JSON 和格式化的输出都可用。

```bash
$ pm2 logs ['all'|app_name|app_id] [--json] [--format] [--raw]
```

示例:

```bash
$ pm2 logs APP-NAME       # 显示 APP-NAME 日志
$ pm2 logs --json         # JSON 输出
$ pm2 logs --format       # 格式化输出

$ pm2 flush               # 冲洗所有日志
$ pm2 reloadLogs          # 重新加载所有日志
```

[更多关于日志管理](http://pm2.keymetrics.io/docs/usage/log-management/)

### 启动脚本生成

在每次服务器重启时，PM2 都会生成并配置一个启动脚本，以保持  PM2 和 进程活跃。

支持初始系统，如： **systemd** (Ubuntu 16, CentOS, Arch), **upstart** (Ubuntu 14/12), **launchd** (MacOSx, Darwin), **rc.d** (FreeBSD).

```bash
# 自动检测初始系统 + 在服务器启动时生成和设置 PM2 boot
$ pm2 startup

# 手动指定启动系统
# 可以是: systemd, upstart, launchd, rcd
$ pm2 startup [platform]

# 在服务器启动时禁用和移除 PM2
$ pm2 unstartup
```

在重新启动（reboot）时保存/冻结（save/freeze ）一个进程列表:

```bash
$ pm2 save
```

[更多关于启动脚本](http://pm2.keymetrics.io/docs/usage/startup/)

## 模块系统

PM2 嵌入了一种简单而强大的模块系统。安装模块很简单:

```bash
$ pm2 install <module_name>
```

下面是一些与 PM2 兼容的模块(由 PM2 管理的独立的 Node.js 应用程序):

[**pm2-logrotate**](https://github.com/pm2-hive/pm2-logrotate) auto rotate logs of PM2 and applications managed<br/>
[**pm2-webshell**](https://github.com/pm2-hive/pm2-webshell) expose a fully capable terminal in browsers<br/>
[**pm2-server-monit**](https://github.com/pm2-hive/pm2-server-monit) monitor your server health<br/>

[编写自己的模块](http://pm2.keymetrics.io/docs/advanced/pm2-module-system/)

## Keymetrics 监控

[![Keymetrics Dashboard](https://keymetrics.io/assets/images/application-demo.png)](https://app.keymetrics.io/#/register)

如果你用 PM2 来管理你的 NodeJS 应用，那么 Keymetrics 可以使监控和管理服务器上的应用变得简单。
试一试:

[PM2发现  PM2 的监测指示板](https://app.keymetrics.io/#/register)

谢谢您的帮助，我们希望您喜欢我们的 PM2 。

## 更多关于 PM2

- [通过 JS 文件的应用程序声明](http://pm2.keymetrics.io/docs/usage/application-declaration/)
- [Watch & Restart](http://pm2.keymetrics.io/docs/usage/watch-and-restart/)
- [PM2 API](http://pm2.keymetrics.io/docs/usage/pm2-api/)
- [部署工作流程](http://pm2.keymetrics.io/docs/usage/deployment/)
- [PM2 on Heroku/Azure/App Engine](http://pm2.keymetrics.io/docs/usage/use-pm2-with-cloud-providers/)
- [PM2 自动完成](http://pm2.keymetrics.io/docs/usage/auto-completion/)
- [在 ElasticBeanStalk 中使用 PM2 ](http://pm2.keymetrics.io/docs/tutorials/use-pm2-with-aws-elastic-beanstalk/)
- [PM2 教程系列](https://futurestud.io/tutorials/pm2-utility-overview-installation)

## 更新日志

[CHANGELOG](https://github.com/Unitech/PM2/blob/master/CHANGELOG.md)

## 贡献者

[Contributors](http://pm2.keymetrics.io/hall-of-fame/)

## License

PM2 is made available under the terms of the GNU Affero General Public License 3.0 (AGPL 3.0).
We can deliver other licenses, for more informations [contact sales](mailto:sales@keymetrics.io).

[![GA](https://ga-beacon.appspot.com/UA-51734350-7/pm2/readme?pixel&useReferer)](https://github.com/igrigorik/ga-beacon)
