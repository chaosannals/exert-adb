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
