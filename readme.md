# exert-adb

## adb 命令

```bash
# 查看文档
adb help

# 列举设备
adb devices -l

# 安装软件
# -s 指定设备
adb -s emulator-5554 install /path/to/app.apk

# 进入 shell
# -s 指定设备
# 进入后 exit 可退出
adb -s emulator-5554 shell
# 后接命令可直接执行并打印结果
adb -s emulator-5554 shell ls

# 下载文件
adb pull /remote/path /local/path

# 上传文件
adb push /local/path /remote/path
```

## 截屏和录像

```bash
# 截屏
adb shell screencap /sdcard/screen.png

# 录像
adb shell screenrecord /sdcard/demo.mp4 --time-limit 10
```

## 关闭签名验证

修改 /system/build.prop 文件，去掉签名验证。

```bash
# 查看
adb shell getprop ro.install.3rd_cert

# 设置为不验证
adb shell setprop ro.install.3rd_cert false

# 重启
adb shell reboot

# 确保文件权限为 644 ，默认是 644，不是时需手动修改。
# 如果权限不够，进入 shell 处理。
adb shell chmod 644 /system/build.prop
```


## 设置

```bash
# 设置经纬度
adb -s emulator-5554 emu geo fix 116.770473 23.463044
```

## 前向/反向代理

```bash
# 列举前向代理
adb forward --list

# 设置前向代理
# adb forward tcp:<host_port> tcp:<avd_port>
adb -s emulator-5554 forward tcp:8080 tcp:8081

# 删除
# adb forward --remove tcp:<host_port>
adb forward --remove tcp:8080
```

```bash
# 这种方式只能 模拟器到本地主机，如果要内网，加多个反向代理
# adb reverse tcp:<avd_port> tcp:<host_port>
adb -s emulator-5554 reverse tcp:8081 tcp:8080

# 列举反向代理
# adb reverse --list
adb reverse --list
adb -s emulator-5554 reverse --list

# 删除反向代理，tcp:<avd_port>
# adb reverse --remove tcp:<avd_port>
# 删除所有反向代理
# adb reverse --remove-all
adb reverse --remove tcp:8081
```

## 使用 telnet 链接 模拟器管理器

```bash
# 指定 host 和 port 链接
telnet localhost 5554

# 进入连接会话后需要认证
# 会有提示你在某个路径下打开文件找到token 
# auth <token>
auth token123456

# 列出重定向列表
redir list

# 设置重定向
# redir add protocol:host-port:guest-port
# protocol 只能是 tcp 或 udp
# host-port 宿主这边
# guest-port 虚拟机
redir add tcp:host-port:guest-port

# 删除
redir del protocol:host-port
```