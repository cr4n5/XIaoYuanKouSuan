# XIaoYuanKouSuan

- 方案一： 小猿口算 - MIMT, 采用抓包方式获取题目和答案, 通过 adb 模拟滑动操作，比机器视觉识别更快更准确！一键启动</br>
- 方案一支持各种比大小，其他比赛很快就能支持
- 方案二： 修改所有答案为“1”（推荐使用方案二）[方案二链接](Change_Answer/README.md) （画饼中：可以融入方案一）

![Language](https://img.shields.io/badge/language-python-blue?logo=python)
![Stars](https://img.shields.io/github/stars/cr4n5/XiaoYuanKouSuan.svg)
![Forks](https://img.shields.io/github/forks/cr4n5/XiaoYuanKouSuan.svg)
![Issues](https://img.shields.io/github/issues/cr4n5/XiaoYuanKouSuan.svg)
![Platform](https://img.shields.io/badge/platform-Android-green?logo=android)

- [安卓模拟器使用教程](README_EMULATOR.md)

## 目录

- [XIaoYuanKouSuan](#xiaoyuankousuan)
  - [目录](#目录)
  - [演示视频](#演示视频)
  - [碎碎念 :thought\_balloon:](#碎碎念-thought_balloon)
  - [环境配置 :hammer\_and\_wrench:](#环境配置-hammer_and_wrench)
  - [代码修改 :pencil2:](#代码修改-pencil2)
  - [使用 :hammer\_and\_wrench:](#使用-hammer_and_wrench)

## 演示视频（过时了）

https://github.com/user-attachments/assets/e9ccfa25-4bdd-4b43-855c-af4a045dcb00

## 效果图（最新版）

![img.png](img.png)

## 碎碎念 :thought_balloon:

代码有点屎山哈哈哈哈，抛砖引玉, 有问题欢迎提 issue :bug:

## 环境配置 :hammer_and_wrench:

1. 能开启adb的设备 建议mumu模拟器 :iphone:
2. python3 :snake:
3. adb :electric_plug:

## 代码修改 :pencil2:

```python
def str_to_xy(str):
    match str:
        case "1":
            return [[1480, 1050], [1440, 1470]]
        case "2":
            return [[1255, 1100], [1700, 1100], [1255, 1470], [1700, 1470]]
        case "3":
            return [[1344, 1040], [1600, 1200], [1270, 1323], [1635, 1379], [1249, 1588]]
        case "4":
            return [[1716, 1274],[1245,1296],[1450,1030],[1450,1466]]
        case "5":
            return [[1558,1020],[1290,1211],[160,1348],[1300.1472]]
        case "6":
            return [[1533,1027],[1265,1428],[1663,1439]]
        case ">":
            return [[[1350, 1080], [1545, 1172], [1295, 1297]]]
        case "<":
            return [[[1578,1058],[1308,1231],[1560,1292]]]
        case "=":
            return [[[1284, 1122], [1700, 1122]],[[1280, 1300], [1700, 1300]]]
```

> [!TIP]
> 根据设备分辨率修改坐标（同元组内坐标连续滑动），坐标已自适应不需要手动修改


```python
adb_ip = "127.0.0.1"
adb_port = 16384
```

> [!TIP]
> 请前往`mitmCode/adb`修改连接adb的ip和地址

```bash
# 查看当前分辨率
adb shell wm size
#还原默认分辨率
adb shell wm size reset
# 更改分辨率为 1800x2880
adb shell wm size 1800x2880
```

```python
for idx, question in enumerate(questions):
    answer = question.get("answer", None)
    swipe_screen(answer)
    logger.info(f"完成题目{idx + 1}|答案：{answer}")
    time.sleep(0.2)
```

根据所需更改每个题目间隔时间

## 使用 :hammer_and_wrench:

1. 使用虚拟环境安装依赖 PowerShell

```shell
python -m venv your_venv_name
.\your_venv_name\Scripts\Activate.ps1
pip install -r requirements.txt
```

3. 配置 adb

- 打开开发者选项中的 usb 调试，推荐使用[mumu模拟器](https://mumu.163.com/help/20230214/35047_1073151.html)

4. 配置安卓代理

- WIFI 设置代理为电脑 ip 和端口(8080) [教程](https://mumu.163.com/help/20230214/35047_1073151.html)

5. 运行

```shell
cd mitmCode
mitmweb -s __init__.py --quiet
```

