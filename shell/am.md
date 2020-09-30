# Activity 管理器（am）

```bash
# 拨打电话
am start -a android.intent.action.CALL -d tel:12345678910

# 显示信息，和系统的默认处理有关。
am start -a android.intent.action.VIEW

# 杀指定后台进程
am kill <package>

# 杀所有后台进程
am kill-all

# 强杀进程
am force-stop

# 重启
am restart
```
