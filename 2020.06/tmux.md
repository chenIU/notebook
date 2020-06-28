**tmux的作用是将窗口和会话分离**

| 命令                                    | 描述                     |
| --------------------------------------- | ------------------------ |
| tmux                                    | 进入tmux窗口             |
| tmux list-keys                          | 列出所有的快捷键         |
| tmux info                               | 列出当前tmux会话信息     |
| exit/ctrl+d                             | 退出tmux                 |
| tmux new -s <session-name>              | 新建会话                 |
| tmux detach                             | 分离会话                 |
| tmux ls                                 | 列出所有的tmux会话       |
| tmux attach -t -0(session_name)         | 接入会话                 |
| tmux kill-session -t -0(session_name)   | 终止会话                 |
| tmux switch -t 0(session_name)          | 切换会话                 |
| tmux rename-session -t -0(session_name) | 重命名会话               |
| tmux split-window                       | 水平分割                 |
| tmux split-window -h                    | 竖直分割                 |
| ctrl+b q                                | 显示窗格编号             |
| ctrl+b x                                | 关闭当前窗格             |
| ctrl+b z                                | 当前窗格全屏显示         |
| ctrl+b !                                | 将当前窗格拆分为独立窗格 |
| ctrl+b ctrl+<arrow key>                 | 按箭头方向调整窗格大小   |
| ctrl+b %                                | 划分左右两个窗格         |
| ctrl+b "                                | 划分上下两个窗格         |
| ctrl+b :                                | 光标切换到上一个窗格     |
| ctrl+b o                                | 光标切换到下一个窗格     |

