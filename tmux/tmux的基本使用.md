# tmux的基本原理及使用:
### tmux是什么
 [tmux](https://zh.wikipedia.org/wiki/Tmux)全称为`terminal multiplexer`，用户可以通过 tmux 在一个终端内管理多个分离的会话，窗口及面板（重点：不受断网影响，避免丢失重要工作进度，所以tmux与[SSH](https://so.csdn.net/so/search?q=SSH&spm=1001.2101.3001.7020)非常搭）
### SSH时发生了什么？
SSH断掉时，server会杀掉你在SSH里运行的程序吗？答案是会！
比如Alice（client）想要SSH到Bob的电脑（server）上跑一个程序，例如java xxx，那么如果这个程序耗时较长，或者Alice需要密切观察程序的输出，在Alice的SSH因为网络或者Bob电脑的设置等原因突然断线的情况下，一切都变成了浮云，这个java程序会被Bob的电脑杀掉。我们可以把SSH程序当成一个同步模型。Alice也可以考虑在java运行时写log，但是今天我们讨论一种更简单的方法，那就是tmux！
### tmux运行原理
tmux 采用client/server架构，当Alice ssh到Bob的电脑上并键入命令tmux时，她就默认启动了tmux服务器，并且创建了一个名字为0的session。我们可以把session当成一个bash环境：ssh启动了一个bash环境，这个session也启动了一个bash环境，不过session的环境独立于SSH，由在Bob电脑上运行的tmux服务器管理。所以ssh断掉完全不影响tmux session的正常运行。我们可以把tmux服务当做异步模型。相比ssh，孰优孰劣一目了然。
### tmux会话(session)的基本操作
1. 创建新会话
` tmux new -s Rin ` 
2. 查看当前的会话列表
`tmux ls`
3. 进入会话
`tmux a -t Rin`
4. 连接上一个会话
`tmux a`
5. 重命名会话s1为s2
`tmux rename -t s1 s2`
6. 关闭会话s1
`tmux kill-session -t s1`
7. 关闭除s1外的所有会话
`tmux kill-session -a -t s1`
8. 关闭所有会话
`tmux kill-server`
9. 会话中的默认前缀键(prefix)
 `ctrl+B`
### tmux窗口(window)中的基本操作
`prefix s　　`列出会话，可进行切换  
`prefix $　　`重命名会话  
`prefix d　　`分离当前会话  
`prefix D　　`分离指定会话  
`prefix c　　`创建一个新窗口  
`prefix ,　　`重命名当前窗口  
`prefix w　　`列出所有窗口，可进行切换  
`prefix n　　`进入下一个窗口  
`prefix p　　`进入上一个窗口  
`prefix l　　`进入之前操作的窗口  
`prefix 0~9`　　选择编号0~9对应的窗口  
`prefix .　　`修改当前窗口索引编号  
`prefix '　　`切换至指定编号（可大于9）的窗口  
`prefix f　　`根据显示的内容搜索窗格  
`prefix &　　`关闭当前窗口  
### tmux窗格管理(pane)中的基本操作
`prefix %　　`水平方向创建窗格  
`prefix "　　`垂直方向创建窗格  
`prefix Up|Down|Left|Right`　　根据箭头方向切换窗格  
`prefix q　　`显示窗格编号  
`prefix o　　`顺时针切换窗格  
`prefix }　　`与下一个窗格交换位置  
`prefix {　　`与上一个窗格交换位置  
`prefix x　　`关闭当前窗格  
`prefix space`(空格键)　　重新排列当前窗口下的所有窗格  
`prefix !　　`将当前窗格置于新窗口  
`prefix Ctrl+o　`　逆时针旋转当前窗口的窗格  
`prefix t　　`在当前窗格显示时间  
`prefix z　　`放大当前窗格(再次按下将还原)  
`prefix i　　`显示当前窗格信息  
