**常用命令**

| 命令               | 描述                                |
| ------------------ | ----------------------------------- |
| .databases         | 查看数据库                          |
| .tables            | 查看表                              |
| .show              | 查看设置                            |
| .exit              | 退出命令行                          |
| .quit              | 退出命令行                          |
| .schema TABLE      | 查看表的结构                        |
| .dump TABLE        | 导出表                              |
| .import FILE TABLE | 导入文件到指定表中                  |
| .backup DB FILE    | 备份某个数据库                      |
| .read FILENAME     | 执行指定文件中的sql                 |
| .timeout MS        | 尝试打开锁定的表MS毫秒              |
| .echo ON\|OFF      | 开启或关闭echo命令                  |
| .header(s) ON\|OFF | 开启或关闭头部显示                  |
| .stat ON\|OFF      | 开启或关闭统计                      |
| .timer ON\|OFF     | 开启或关闭CPU定时器                 |
| .seperator STRING  | 改变输出模式和.import所使用的分隔符 |
| .nullvalue STRING  | 在NULL的地方输出STRING字符串        |
| .help              | 查看帮助                            |



#  数据库

## 创建数据库

```bash
sqlite3 runoob.db 
```

## 附加数据库

**语法**

```bash
ATTACH DATABASE file_name AS database_name
```

**实例**

```bash
ATTACH DATABASE 'runoob.db' AS 'runoob'
```

## 分离数据库

**语法**

```bash
DETACH DATABASE 'Alias-Name'
```

**实例**

```bash
DETACH DATABASE 'runoob'
```



[sqlite-jdbc](https://bitbucket.org/xerial/sqlite-jdbc/downloads/)



[runoob](https://www.runoob.com/sqlite/sqlite-tutorial.html)