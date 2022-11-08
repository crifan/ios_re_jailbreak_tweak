# 搭建Theos环境

TODO：

* 【已解决】XCode编译iOSOpenDev的Logo Tweak项目报错： Command PhaseScriptExecution failed with a nonzero exit code Failed to locate Logos Processor

---

## 前提

* `Mac`
  * `Homebrew`
  * `XCode`
    * XCode是必须的，因为`Command Line Tools`是不够用的。而`Xcode`包含了所有Apple平台的所有工具（链）
  * 必要的工具
    * `ldid`
    * `xz`
        ```bash
        brew install ldid xz
        ```

## 设置theos的环境变量

先确认自己的shell是啥：

```bash
➜  iOS_Tweak echo $SHELL
/bin/zsh
```

此处是：`zsh`，所以去编辑`zsh`的启动脚本：

```bash
vi ~/.zshrc
```

加上：

```bash
export THEOS=/opt/theos
export PATH=$THEOS/bin:$PATH
```

说明：

* 安装位置的选择
  * 为了后续兼容其他相关开发工具，比如iOSOpenDev
  * 最好安装到默认的=大家常用的位置
    * `/opt/theos`
  * 最好不要放在其他位置
    * 比如我之前就放在自己的某个目录
      * `/Users/crifan/dev/DevSrc/iOS_Tweak/theos`
    * 否则容易导致各种错误
* 如果后续需要，可以把IP的环境变量也加上
  ```bash
  export THEOS_DEVICE_IP=192.168.31.43
  ```
    * 注：其中的`192.168.31.43`是你的调试的目标设备iPhone的WiFi的IP地址

## 下载theos代码

```bash
cd /opt/theos
git clone --recursive https://github.com/theos/theos.git $THEOS
```

### 常见问题

#### xcrun error invalid active developer path

macOS升级后

```bash
git clone
```

出错：`xcrun: error: invalid active developer path`

解决办法：

```bash
xcode-select --install
```

会弹框，点击安装，开始安装`xcode-select`。等安装完毕，即可。

## 下载私有框架=下载sdk

注：`XCode 7.3`之后，就不再提供，后续开发tweak时（可能）需要链接使用的私有框架private Framework了

所以要单独下载：

```bash
curl -LO https://github.com/theos/sdks/archive/master.zip
TMP=$(mktemp -d)
unzip master.zip -d $TMP
mv $TMP/sdks-master/*.sdk $THEOS/sdks
rm -r master.zip $TMP
```

## 编译运行调试

最后是，编译运行调试：

```bash
make do
```

注：

* 最新的 `make do` == 之前的：`make package install`
  * 新官网（https://theos.dev/）中也有显示
    * ![theos_make_do](../../assets/img/theos_make_do.png)

说明：

* 新版theos已内置`CydiaSubstrate`（`CydiaSubstrate.framework`），无需运行`bootstrap.sh`或从`iPhone`中拷贝了
* 新版theos也无需：`dpkg-deb`、`brew install dpkg` 了
