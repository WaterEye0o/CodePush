# CodePush
本文章仅翻译
[原文地址](https://microsoft.github.io/code-push/docs/cli.html)
#安装
安装 node.js
安装 CodePush CLI:
```
npm install -g code-push-cli 
```
#开始使用
1. 创建一个CodePush账号来使用CodePush CLI
* 将你的app注册进Codepush当中，并且可以将它分享给你团队的其他人
* 将Codepush（cordova或者react native）的依赖配置进你的app当中
* 发布或者更新一个你的app
* 祝愿它长期有用，并且越来越好

#创建账号
在你开始发布和更新一个app时你需要先创建一个CodePush账号。你可以跑下面的这行代码来注册你的app（在用之前确保你安装了code-push-cli）
```
code-push register
```
这将会弹出一个页面让你使用GitHub或者微软账号授权。当你授权完成以后，它将会创建一个CodePush账号与你的Github/MSA身份的“连接”，并且生成一个access key ，你可以复制/粘贴在你的CLI中来登录。

>*注意:注册完成以后，你将在CLI之中自动登录一直到你自己退出，意味着你不需要重复登录在同一台机器上*

如果你已经存在了一个账号，你可能需要使用另一个身份来连接你的账号，可以跑下面的命令：
```
code-push link
```
在跑这个命令行的时候需要主要你的邮箱地址必须与你的已经存在的账号匹配上。

#授权
大部分的CodePush CLI命令都是需要授权，因此在你开始管理你的账号之前，你需要使用GitHub或者微软账号登录。你可以使用下面的命令来登录：
``` 
code-push login 
```
这将会弹出一个页面，要求你使用GitHub或者微软账号进行授权。这将会生成一个access key，你需要将它复制/粘贴到CLI终端上(它将会让你提供给他）。你现在就成功的授权了并且可以安全的退出浏览器。
在一般情况下，登录的命令会支持代理并且会根据你的环境变量（HTTPS_PROXY 或者HTTP_PROXY for HTTPS 或者 HTTP traffic respectively）去与这个代理建立一个连接。
CodePush 具体的代理也是可以使用 --proxy参数来设置的:
```
code-push login --proxy proxyUrl
```
另外，很幸运的是代理是能够被失效的（系统环境变量被抑制并且CodePush忽略代理的设置）通过 --noproxy参数来设置的：
```
code-push login --noproxy
```
在任何时候你想要确认你是否已经登录了，你能通过跑下面的命令来展示邮箱的地址以及你当前的授权会话（你所提供验证身份的账号例如：GitHub)
还有以前你对代理的所有设置：
```
code-push whoami
```
当你登录CLI的时候你的access key是一直在你的硬盘中存在的在在你使用会话的期间，所以你不需要每次都去通过你的账号去登录。换句话如果你终止了你的会话并且删除这个access key，只要简单的运行下面这个命令：
```
code-push logout
```
如果你忘记从机器中退出登录，你不愿意退出一个正在运行中的会话（例如：你朋友的笔记本），你可以使用下面的命令来展示和移除正在“live“的access keys。这个access keys的列表将展示哪台机器创建了这个key，并且是在什么时候登录的。这将使他很简单的展示keys的状态，你不想继续的话。
```
code-push access-key ls
code-push access-key rm <accessKey>
```
如果你不想通过给出GitHub或者微软凭证来使用的额外keys来使用CodePush服务的话可以运行下面的命令来产生一个持久的账号（需要有一个对他的描述）：
```
code-push access-key add "VSTS Integration"
```
在创建一个新的key之后，你能够指定他的值通过--accessKey参数在你登录的命令当中（允许你执行“headless”授权，不想要弹出一个页面）。
```
code-push login --accessKey <accessKey>
```
当你通过这个方法登录的时候，access key将不会自动的销毁在你退出登录的时候，并且可以一直在未来的对话当中使用直到他在CodePush服务当中消失。但是他会一直推荐你退出登录当你会话关闭的时候，换句话说将他从你的硬盘当中删除掉。
