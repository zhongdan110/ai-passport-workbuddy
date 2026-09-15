# 第三方与参考

## 设备固件

* **这是非官方固件。** 基于 FoloToy 公开的 AI Passport Buddy 参考分支
  （`demo/claude-buddy-port`）改写，**不是** FoloToy 官方发布的固件。
  仅供学习交流，刷机风险自负，请先自行备份。
* 界面上的 WorkBuddy 图标取自 WorkBuddy 桌面端自带的官方资源。
* 设备屏幕上的中文字体是**子集**（约 300 字），由思源黑体 SourceHanSansSC
  （SIL Open Font License 1.1）经 `lv_font_conv` 生成。

## 电脑端

协议与思路参考了这些公开项目 —— 是**参考**，不是代码依赖：

| 项目 | 许可 | 参考了什么 |
| --- | --- | --- |
| `anthropics/claude-desktop-buddy` | — | Hardware Buddy 线协议 |
| `mac20777/vibecoding-voice` | MIT | 虚拟声卡 + 微信输入法这条路线的最早实践 |
| `xiabill/ai-passport` | MIT | IMA ADPCM 编解码 |
| FoloToy `ai-passport` 的 `demo/claude-buddy-port` 分支 | — | 设备端基础 |

运行时依赖（由安装脚本自动装进包内独立环境）：

| 库 | 许可 | 用途 |
| --- | --- | --- |
| [bleak](https://github.com/hbldh/bleak) | MIT | 蓝牙通信（Windows 上走 WinRT） |
| [sounddevice](https://github.com/spatialaudio/python-sounddevice) | MIT | 把解码后的音频写进虚拟声卡 |
| [pyserial](https://github.com/pyserial/pyserial) | BSD-3-Clause | 串口（烧录、抓屏、救援） |
| [esptool](https://github.com/espressif/esptool) | GPL-2.0 | 烧录设备固件（由用户自行安装，不随包分发） |

## 本仓库不包含什么

只发布**成品**（电脑端程序与设备固件包），不包含上游项目的源码。
如果你要找上游，请到上表列出的仓库。
