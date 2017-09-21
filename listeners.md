Listeners
===
Listeners 是 Cobalt Strike's 对于payloads handler的抽象，Listeners 是连接到 payload 配置信息的名称(例如:协议、主机、端口等等)，在某些情况下，还承诺建立一个服务器来接收来自所描述的有效负载的连接。
## Listener API
Aggressor Script 会聚合您当前连接到的所有团队服务器的Listeners 信息，这使得很容易将会话传递给另一个团队服务器。 要获取所有侦听器名称的列表，请使用＆listeners函数。 如果您只想使用本地监听器，请使用 **&listeners_local** 。 **&listener_info** 函数将侦听器名称解析为其配置信息。 此示例将所有侦听器及其配置输出到Aggressor Script控制台：
```
command listeners {
	local('$name $key $value');
	foreach $name (listeners()) {
		println("== $name == ");
		foreach $key => $value (listener_info($name)) {
			println("$[20]key : $value");
		}
	}
}
```
## 创建 Listens
使用 **&listener_create**v 创建一个监听器并启动一个与之关联的负载处理程序。
## 选择 Listens
使用＆openPayloadHelper打开一个列出所有可用侦听器的对话框。用户选择侦听器后，此对话框将关闭，Cobalt Strike将运行回调函数。以下是Beacon spawn 菜单的源代码：
```
item "&Spawn" {
	openPayloadHelper(lambda({
		binput($bids, "spawn $1");
		bspawn($bids, $1);
	}, $bids => $1));
}
```
## Shellcode
使用 **&shellcode**为指定的Listens生成shellcode。

## 可执行文件和DLLs
使用 **&artifact** 为指定的Listens生成可执行文件或DLL。
## PowerShell
使用 **&powershell** 生成一个用于加载Listens的powershell一行程序。
## Stageless Artifacts
使用 **&artifact_stageless** 为本地Listens生成无Stage可执行文件，DLL，PowerShell脚本或 raw position-independent blob。
