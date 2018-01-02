# node-supervisor

适用于 nodejs 的一个管理器脚本。它运行你的程序，并监视代码的变化，
所以你可以有热代码重新加载行为，而不用担心内存泄漏，
并确保清理所有的模块间引用，并没有一个全新的 `require` 系统。

## node-supervisor -?

  Node Supervisor 在程序崩溃时被用来重新启动程序。
  它还可以用于在一个 *.js 文件更改时重新启动程序。

### 用法:

  ```
  supervisor [options] <program>
  supervisor [options] -- <program> [args ...]
  ```

  `<program>` 是必须的，它是用来运行的程序。

### 选项：

            选项  |       描述         |      默认值
-----------------|--------------------|------------
`-w|--watch <watchItems>`  | 要观察的文件或文件夹列表，以逗号分隔。当文件发生改变时，重新加载程序  |  `.`
`-i|--ignore <ignoreItems>`  | 要忽略改变的文件夹列表，以逗号分隔  |  -
`--ignore-symlinks`  |  忽略符号链接 :)|  -
`-s|--timestamp`  | 每次运行后记录时间戳。这可以很容易地告诉任务上次运行的时间。  |  -
`-p|--poll-interval <milliseconds>`  | 轮询观察文件更改的频率。  |  Node 的默认值
`-e|--extensions <extensions>`  | 要观测的文件扩展列表，以逗号分隔。  |  `node,js`(或者 CoffeeScript 时 'node,js,coffee,litcoffee')
`-x|--exec <executable>`  | 运行指定程序的可执行文件 |  `'node'`
`-pid|--save-pid <path>`  | 将管理的进程 id 保存到给定路径的文件中。  |  -
`--debug[=port]`  | 使用 --debug 标志启动 node  |  -
`--debug-brk[=port]`  | 使用 --debug-brk 标志启动 node  |  -
`--harmony`  |  使用 --harmony 标志启动 |  -
`--inspect[=port]`  |  使用 --inspect 标志启动 |
`-n|--no-restart-on error|exit|success`  | 如果管理程序结束，不要自动重启它。管理器将等待源文件的更改。如果为 `error`，0 退出码将会重启；如果为 `exit`，无论退出代码如何，都不会重新启动；如果为 `success`，只有当退出代码为 0 时才会重新启动。|  -
`-t|--non-interactive`  | 禁用交互模式。使用此选项将不会监听标准输入  |  -
`--force-watch`  | 使用 `fs.watch` 代替 `fs.watchFile`。如果您在 windows 机器上看到高 cpu 负载，这可能很有用。| -
`-k|--instant-kill`  | 立即杀死服务器进程，而不是正常关闭服务器。当 node 应用程序将事件附加到 SIGTERM 或 SIGINT 中以便在进程退出之前进行正常关闭时，这会非常有用。  |
`-RV|--restart-verbose`  | 记录导致管理器重新启动的文件  |
`-h|--help|-?`  | 显示这些使用说明。  |
`-q|--quiet`  |  抑制 DEBUG 消息 |
``  |   |
``  |   |
``  |   |
``  |   |

启动后的可用选项：

* `rs ` - 重启进程。即使没有文件更改，也要重新启动程序，这很有用。

## 示例

```
supervisor myapp.js
supervisor myapp.coffee
supervisor -w scripts -e myext -x myrunner myapp
supervisor -w lib,server.js,config.js server.js
supervisor -- server.js -h host -p port
```

为了不监视文件的变化，使用 "-i ."。


## 简单安装

运行

```
$  npm install supervisor -g
```

## 花式安装

获取这些代码，然后这样做:

```
$ npm link
```
