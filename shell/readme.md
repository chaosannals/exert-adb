# shell

## 输入（input）

详细键值信息，自行网上查找。

```bash
# 设备返回建
input keyevent 4

# 锁定
input keyevent 26

# 解锁屏幕
input keyevent 82

# 点击屏幕 50 250 位置。
input tap 50 250

# 滑动屏幕 (50,250) 到 (500, 250) 滑动 600ms
input swipe 50 250 500 250 600

# 字符输入 abc 是字符底层事件会被输入法捕获。
# 中文输入查看下面中文输入说明。
input text abc
```

### 中文输入

```bash
# 查看有哪些输入法
ime list -a
```

输入中文需要安装[ADBKeyBoard](https://github.com/senzhk/ADBKeyBoard)。

1. 安装后需要在 语言与输入设置 里面启用这个输入法。
2. 把他设置成 默认的输入法 或者 确保在输入时使用该输入法。
3. 通过 broadcast 发送信息。

```bash
# GitHub 项目文件里有 apk 文件可安装。
adb install ADBKeyboard.apk

# 发送中文输入。
adb shell am broadcast -a ADB_INPUT_TEXT --es msg "你好"
```
