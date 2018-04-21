# C-Lua

## 示例1
### 项目配置
去年尝试过一次，过了一年流程全忘了，为免重蹈覆辙，于此记录一下关键步骤。

__目录结构__

> 
Lib\			// 这个目录用于放库文件  
	lua-5.1.5\	// 包含改版本 lua 的所有源文件，其中的 readme 介绍了如何对其进行build  
Source\		// 用于存放 C++ 源文件  
	main.cpp 	// 该文件创建了一个lua状态机并演示了简单的栈操作。  
VSProj\		// VS 解决方案的存放目录  
	Lua5.1.5\	// 单独的项目用于生成静态库文件  
	Release\ 	// 最后生成的库文件和可执行文件都放在里面  
	VSProj\ 	// 这个创建的时候名字没起好，用于生成仅包含 main.cpp 的主项目。（后文中把这个目录叫做 LuaStateTestMain 方便区分）  

上面的结构可以看出 VS的项目目录和源文件库文件不需要在同一个目录中。  
Lua5.1.5 和LuaStateTestMain 两个项目在创建的时候，都是通过 Win32 控制台应用程序 进入，会出来一个项目创建的向导，一个选择静态库的空项目，一个选择 控制台应用程序的空项目即可。  
主要需要进行配置的项目是 LuaStateTestMain 。在 解决方案资源管理器中，右键 LuaStateTestMain 项目，先设置成启动项目，再  
1.选择`属性`- `配置属性`-`C/C++`-`常规`-`附加包含目录` 添加lua 头文件的包含目录。如果不包含的话，写在 main.cpp 文件中的头文件引用在编译的时候会找不到。  
2.选择`属性`- `配置属性`-`链接器`-`常规`-`附加库目录` 添加生成的 Lua5.1.5.lib 的包含目录。  
3.选择`属性`- `配置属性`-`链接器`-`输入`-`附加依赖项` 添加 Lua5.1.5.lib 作为依赖。  
4.选择`生成依赖项`- `项目依赖项`，勾选 Lua5.1.5 。表示在编译多个项目的过程中，要等编译完 Lua5.1.5 之后才能编译 LuaStateTestMain 。  



