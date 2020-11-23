# testmake  
该 Demo是vscode 配置 make 编译 调试/运行 C++程序的 测试  
1、创建 tasks.json  
在vscode的主菜单栏单击 Terminal --> Configure Tasks --> Create tasks.json file from template --> Others ,生成的tasks.json 如下所示：  
{  
    // See https://go.microsoft.com/fwlink/?LinkId=733558  
    // for the documentation about the tasks.json format  
    "version": "2.0.0",  
    "tasks": [  
        {  
            "label": "echo",  
            "type": "shell",  
            "command": "echo Hello"  
        }  
    ]  
}  
  
将其修改成如下：  
  
{  
    // See https://go.microsoft.com/fwlink/?LinkId=733558  
    // for the documentation about the tasks.json format  
    "version": "2.0.0",  
    "tasks": [  
        {  
            "label": "build-debug",  
            "command": "make",  
            "args": [],  
            "type": "shell"  
        }  
    ]  
}  
  
其中， "label" 的值 对应 launch.json文件中 "preLaunchTask"  
  
2、创建 launch.json , 在vscode主菜单点击 Run --> Open Configurations --> C++ (GDB/LLDB), 生成的launch.json文件如下：  
  
其中 "program" 是 make后生成的可执行文件的路径， "preLaunchTask" 对应tasks.json文件中一个task。  
  
{  
    // Use IntelliSense to learn about possible attributes.  
    // Hover to view descriptions of existing attributes.  
    // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387  
    "version": "0.2.0",  
    "configurations": [  
        {  
            "name": "(gdb) Launch",                 //启动配置的下拉菜单中显示的名称  
            "type": "cppdbg",  
            "request": "launch",  
            "program": "${workspaceFolder}/build",  // 将要进行调试的程序的路径  
            "args": [],  
            "stopAtEntry": false,                   // 设为true时程序将暂停在程序入口处  
            "cwd": "${workspaceFolder}",  
            "environment": [],  
            "externalConsole": false,               // 调试时是否显示控制台窗口  
            "MIMode": "gdb",  
            "setupCommands": [  
                {  
                    "description": "Enable pretty-printing for gdb",  
                    "text": "-enable-pretty-printing",  
                    "ignoreFailures": true  
                }  
            ],  
            "preLaunchTask": "build-debug"           // 调试会话开始前执行的任务，一般为编译程序  
        }  
    ]  
}  
  
3、在程序中设置断点， 按F5 开始调试。  
  









