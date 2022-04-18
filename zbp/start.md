# 启动你的第一个zbp机器人！

启动一个zbp机器人，你需要……

- 一个qq号
- 一个github账号
- 一台手机/电脑 （**萌新推荐使用电脑** 容易操作）
- 一份可以耐心配置机器人的心情

## 获取zbp的可运行文件

> 推荐直接阅读项目原`README.md`。

### 一般通用方法

1. 进入[zbp项目页面](https://github.com/FloatTech/ZeroBot-Plugin)
2. fork到你的仓库中（手机需要让浏览器请求**桌面版网站**）
3. 新建（create new file）名为`config.json`的文件
4. 修改`config.json`内容如下并提交保存：

```json
{
  "zero": {
    "nickname": [
      "你的机器人昵称", // 可添加多个昵称 仅需添加像左侧一样的一行
      "姬气人昵称2"
    ],
    "command_prefix": "/", // 指令前缀 可不改
    "super_users": ["12345678","87654321"] // 此处填写机器人管理员qq 可多个
  },
  "ws": [ // 此部分内容可不作修改 与onebot侧所填端口相同即可
      {
          "Url": "ws://127.0.0.1:6700",
	  "Access Token": ""
      }
  ]
}
```

5. 修改`main.go`：通过在`_ "github.com/FloatTech/ZeroBot-Plugin/plugin/xxxx"`前添加`// `来关闭插件

?> 此处的关闭插件指的是*使机器人不具有此功能*，即 /启用 和 /禁用 都无法干涉的强制关闭。

6. 提交修改后，编译。
  - 选择前往仓库的Github Actions页面下载自动编译好的文件
    1. 点击右上角 Fork 本项目，并转跳到自己 Fork 的仓库
    2. 点击仓库上方的 Actions 按钮，确认使用 Actions
    3. 编辑 main.go 文件，内容按需修改
    4. 前往 Release 页面发布一个 Release，tag形如v1.2.3，以触发稳定版编译流程
    5. 点击 Actions 按钮，等待编译完成，回到 Release 页面下载编译好的文件
    6. ~~我们才不会在最后一条写啾咪~~
  - 选择`git clone`这个仓库到装好[GoLang环境](https://studygolang.com/dl)的本地进行编译
    1. 下载安装最新[Go](https://studygolang.com/dl)环境
    2. `git clone`并进入本项目，下载所需包
```
git clone --depth=1 https://github.com/FloatTech/ZeroBot-Plugin.git
cd ZeroBot-Plugin
go version
go env -w GOPROXY=https://goproxy.cn,direct
go env -w GO111MODULE=auto
go mod tidy
```
    3. 编辑 main.go 文件，内容按需修改
    4. 按照平台输入命令编译，下面举了一些例子
```
# 本机平台
go build -ldflags "-s -w" -o zerobot -trimpath
# x64 Linux 平台 如各种云服务器
GOOS=linux GOARCH=amd64 go build -ldflags "-s -w" -o zerobot -trimpath
# x64 Windows 平台 如大多数家用电脑
GOOS=windows GOARCH=amd64 go build -ldflags "-s -w" -o zerobot.exe -trimpath
# armv6 Linux 平台 如树莓派 zero W
GOOS=linux GOARCH=arm GOARM=6 CGO_ENABLED=0 go build -ldflags "-s -w" -o zerobot -trimpath
```
7. 运行OneBot框架，同时运行本插件的可执行文件

### 懒人包程度的方法

在这里，FloatTech提供了[gocqzbp](https://github.com/FloatTech/gocqzbp)~~贴贴~~整合包，~~只用运行一个可执行文件的好时代来临啦~~

你还可以使用该项目的[docker版](https://github.com/FloatTech/gocqzbp/pkgs/container/gocqzbp)。

## 真不错！

现在你已经成功拥有了一只自己的姬气人！如果只是日常使用的话，明白这些已经足够了！左转退出吧~~

接下来的内容、就让我们一起对姬气人进行更高程度的自定义吧！
