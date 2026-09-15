# WorkBuddy × AI Passport

把 **FoloToy AI Passport** 接进 **WorkBuddy** 工作流 —— 设备屏幕实时显示助手在干什么，
按下设备下键还能对着它说话，说的话直接变成电脑输入框里的文字。

```
WorkBuddy ──转录文件──▶ 桥接程序 ──蓝牙──▶ AI Passport 屏幕
                          ▲                    │
                          └── 按键 / 语音 ──────┘
```

## 下载

到 [Releases](../../releases/latest) 页下载两个包：

| 包 | 装在哪 | 版本 |
| --- | --- | --- |
| `WorkBuddy-Bridge-2.2.zip` | 你的电脑 | 2.2.0 |
| `workbuddy-passport-firmware-0.2.6-workbuddy-20260915.zip` | AI Passport 硬件 | 0.2.6 |

> **重刷过固件的，先把电脑端升到 2.2.0**：整片刷写会覆盖设备 NVS，
> 设备侧的配对密钥随之丢失，而 Windows 仍记着旧密钥，会出现「连上就断、语音用不了」。
> 2.2.0 会自己识别并清除，不用再去设置里手动删设备。

## 安装

**先刷固件（设备），再装桥（电脑）。**

### 1. 固件 → 设备

设备用 USB 数据线连到电脑，关掉任何串口监视工具（桥不用关，它走蓝牙），然后在解压出来的目录里：

```bash
python tools/flash.py --list      # 看串口
python tools/flash.py --check     # 只读检查
python tools/flash.py --full      # 首次安装
```

需要 Python 3.9+ 与 `pip install esptool`。刷之前会自动备份设备原有固件，刷完逐字节回读验证；
工具**不提供整片擦除**，出厂身份区与分区表都在保护范围内。

### 2. 桥 → 电脑

解压 `WorkBuddy-Bridge-2.2.zip`，双击 `install.cmd`，跟着提示走（**不需要管理员权限**）。
装完**完全退出 WorkBuddy 再打开**一次（配置在启动时缓存）。

### 3. 验证

```bash
python -m wbb status
```

看到 `BLE=已连 设备=WorkBuddy-xxxxxx` 就成了。

## 需要什么

| 项 | 要求 |
| --- | --- |
| 系统 | Windows 10 / 11 |
| Python | 3.11+（电脑端）／3.9+（烧录） |
| WorkBuddy | 桌面版（桥靠它取状态） |
| 设备 | FoloToy AI Passport |

## 校验值

```
9f8feaf119a7e63cebf6c0b97267bed6b09623841f165042f4b87d4414f39788  WorkBuddy-Bridge-2.2.zip
59a900d642b99cb5b31493885e36e86dc09ed196186fb47efaae92153674b079  workbuddy-passport-firmware-0.2.6-workbuddy-20260915.zip
```

固件包内另有 `SHA256SUMS.txt` 与 `firmware/manifest.json`（含每个镜像的哈希与**构建指纹**）。
判断"设备上跑的是不是这一份"要看构建指纹 —— 版本号与编译时间在重新链接时不会更新。

## 许可与声明

* 本项目代码以 [MIT](LICENSE) 发布。
* **设备固件为非官方固件**，基于 FoloToy 公开的 Buddy 参考分支改写，仅供学习交流；
  刷机有风险，请自行判断并备份。详见 [THIRD-PARTY.md](THIRD-PARTY.md)。
* 不往任何服务器发数据：只有你电脑与设备之间的蓝牙，以及（可选）本机虚拟声卡。
