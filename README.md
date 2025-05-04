# smart210_SDK

记录一下

## 环境配置

### 板子IP配置

```shell
setenv gatewayip 192.168.0.1
setenv ipaddr 192.168.0.111
setenv netmask 255.255.255.0
setenv serverip 192.168.0.100
sa

```

### 编译时工具链配置

```shell
cat /etc/environment
PATH="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/usr/local/arm/4.3.2/bin"

source /etc/environment

```


# uboot

## 编译

```shell
make clean
make distclean
make smart210_config
make
```


## 下载

```shell
tftp 20000000 smart210-uboot.bin
nand erase 0x0 0x40000
nand write 0x20000000 0 40000
```

### 注意事项

#### 当前uboot固件不能大于256KB

因为env环境变量存放在0x40000开头的16KB，如果uboot固件大于256KB，那么会覆盖掉env。导致uboot运行时检查出来env的crc不对（被uboot覆盖），从而会重新写入default env这样会覆盖掉uboot代码。

目前临时做法是保证uboot固件小于256kb
