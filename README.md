# 【刷 WARP IP】 - 为 WARP 解锁流媒体而生
Born to make stream media unlock by WARP 

* * *

# 目录

- [更新信息](README.md#更新信息)
- [脚本特点(附 5 种模式对比)](README.md#脚本特点)
- [VPS 运行脚本(附 TG bot 创建方法)](README.md#VPS-运行脚本)
- [Docker 自动解锁方案](README.md#Docker-自动解锁方案)
- [鸣谢](README.md#鸣谢下列作者的文章和项目)

* * *

## 更新信息
2023.7.4 1.13 Wireguard-go-reserved supports changing IP; Wireguard-go-reserved 支持更换 IP

2023.6.28 1.12 Wireproxy dual-stack supports changing IP; Wireproxy 模式双栈支持更换 IP

2023.6.26 1.11 1. Warp-go uses the official api to register and cancel accounts; 2. Client proxy mode dual-stack supports changing IP; 3. Client warp mode dual-stack supports changing IP 1. warp-go 使用官方 api 注册和注销账户; 2. Client proxy 模式双栈支持更换 IP; 3. Client warp 模式双栈支持更换 IP

<details>
    <summary>历史更新 history（点击即可展开或收起）</summary>
<br>

>2023.3.26 1.10 Upgrade the Netflix unlocking section; 升级解锁奈飞的部分
>
>2022.9.16  1.09 Support change IP for warp-go mode; 支持 warp-go 模式下更换 IP
>
>2022.4.9  1.08 Support change IP for Client WARP mode; 支持 Client WRAP 模式下更换 IP
>
>2022.4.2  1.07 1. Support change IP for WireProxy; 2. Add Misaka one-key warp. 1. 支持 WireProxy 更换 IP; 2. 新增 Misaka WARP 一键脚本
>
>2022.2.23 1.06 1. Add two modes to unlock: systemd service and pm2 daemon; 1. 增加两个解锁模式: systemd 服务和 pm2 进程守护
>
>2022.2.20 AC 交叉编译（cross-compilation）上传镜像，支持 AMD64、 ARM64 和 s390x
>
>2022.2.15 Happy Lantern Festival. Bring you a new experience of docker unlock, another way to unlock Netflix. Project based on alpine. Content wgcf and unblocking Netflix scripts. Change unlock warp ip automatically. Provide a socks5 proxy for the host. Thanks Oreo ,Coia Prant and Brother Big B   
>元宵节快乐。为大家带来个 docker 解锁的全新体验，换个姿势解锁 Netflix。项目以 alpine 为基础系统，内含 wgcf 和解锁 Netflix 脚本，自动切换解锁 WARP IP，为宿主机提供 socks5 代理，感谢 "猫佬"、"Coia Prant"和"大B哥"
>
>2022.2.2 1.05 1. Support switch unlock modes and stream media freely; 2. Remove ASN information. Add icon in TG push; 3. Limit the log to 1000 lines; 1. 轻松地切换解锁模式和流媒体平台; 2. 去掉日志里的线路供应商信息，在 TG push 里加入icon; 3. 限制日志在1000行
>
>2022.1.31 1.04 1. Support push the logs to Telegram. 1. 日志结果输出到 Telegram.
>
>2022.1.30 1.03 1. Suppport pass parameter. You can run like this:```bash <(curl -sSL https://gitlab.com/fscarmen/warp_unlock/-/raw/main/unlock.sh) -E -A us -4 -N nd -M 2```; 2. Improve log details     
>1. 支持传参，你可以这样运行脚本:  ```bash <(curl -sSL https://gitlab.com/fscarmen/warp_unlock/-/raw/main/unlock.sh) -E -A us -4 -N nd -M 2```; 2. 日志显示更详细
</details>

2022.1.29 1.02 1. Support Disney+ 1. 支持 Disney+

2022.1.28 1.01 1. Add two ways to unlock; 2. Add running logs file 1. 增加两种解锁方式; 2. 加入运行日志
```
2022-01-31 21:27:35.    IP: 8.37.43.216         Country: Japan        Script runs.
2022-01-31 21:27:35.    IP: 8.37.43.216         Country: Japan        Netflix: No.
2022-01-31 21:27:56.    IP: 8.37.43.188         Country: Japan        Netflix: No.
2022-01-31 21:28:15.    IP: 8.37.43.192         Country: Japan        Netflix: No.
2022-01-31 21:28:38.    IP: 8.37.43.229         Country: Japan        Netflix: Yes.
2022-01-31 22:28:40.    IP: 8.37.43.229         Country: Japan        Script runs.
2022-01-31 22:28:42.    IP: 8.37.43.229         Country: Japan        Netflix: Yes.
```

beta 2022.1.26 Media unlock daemon. Check it every 5 minutes. If unlocked, the scheduled task exits immediately. If it is not unlocked, it will be swiped successfully in the background. Advantages: Minimized use of system resources. ~Disadvantage: Can't see the results as intuitively as screen~

## 脚本特点
* 支持多种主流串流影视检测，可以单选或多选
* 支持 warp socks5 / interface 检测和更换 IP 
* 日志输出
* 多种方式解锁: 1.crontab 每 5 分钟检测一次状态; 2. screen 后台运行; 3. nohup & 后台运行; 4. systemd service 进程守护; 5. pm2 daemon 进程守护

  | Mode<br>模式 | Dependencies<br>依赖 | Resident Process<br>常驻进程 | Maximum detection interval time<br>最大检测间隔时长 | recommendation<br>推荐度 |
  | ------- | ------- | ------- | ------- | ------- |
  | 1 crontab |❌| ❌| 5 min | ⭐⭐⭐⭐⭐ |
  | 2 systemd |❌| ✅ | 60 min | ⭐⭐⭐⭐ |
  | 3 nohup |❌| ✅ | 60 min | ⭐⭐⭐⭐ |
  | 4 screen | screen | ✅ | 60 min | ⭐⭐⭐ |
  | 5 pm2| node npm pm2 | ✅ | 60 min | ⭐⭐ |
  
<img src="https://user-images.githubusercontent.com/62703343/155870006-ce235b59-fee7-4f45-a9b7-9af3ede8420f.png" width="70%" />

<img src="https://user-images.githubusercontent.com/62703343/155870126-97aaea72-d714-4d1d-80c6-f9864d0246a6.png" width="60%" />

## VPS 运行脚本

### 1.菜单方式 (menu)
```
bash <(curl -sSL https://gitlab.com/fscarmen/warp_unlock/-/raw/main/unlock.sh)
```
### 2.带参数 (pass parameter)
  | paremeter 参数 | value 值 | describe 具体动作说明 |
  | ----------|------- | --------------- |
  | -E |   | English 英文 |
  | -C |   | Chinese 中文 |
  | -U |   | Uninstall 卸载  |
  | -M | 1 | Mode 1: detect every 5   minute 每5分钟检测 |
  | -M | 2 | Mode 2: run by systemd   以 systemd 方式运行 |
  | -M | 3 | Mode 3: run by nohup &   以 hup & 方式运行 |
  | -M | 4 | Mode 4: run by screen   以 screen 方式运行 |
  | -M | 5 | Mode 5: run by pm2 daemon  以 pm2 进程守护方式运行 |  
  | -A | ** | region abbreviation,such as us. 地区简码,如 us |
  | -N | n | Unlock Neflix 解锁奈飞 |
  | -N | d | Unlock Disney+ 解锁迪士尼 |
  | -N | ud | Unlock Neflix and Disney+ 解锁奈飞和迪士尼 |
  | -T | Token@ID@Name | Receive messages Bot 接收信息的 TG bot 信息 |

For example 1: Language is Chinese. Unlock area is Singapore. Brush WARP IPv4. Unlock Netflix and detect every 5 minute when successed. Receive message to
举例1: 用中文，解锁新加坡奈飞，当成功的时候每5分钟检测一次，
```
bash <(curl -sSL https://gitlab.com/fscarmen/warp_unlock/-/raw/main/unlock.sh) -C -A sg -4 -N n -M 1 -T 1730133Uu5:AAF33T7sWPB8cGu31-QoaUkjdkjzeRo1_m8@1254502669@unlock
```
For example 2: Display and uninstall in English
举例2: 用英文卸载
```
bash <(curl -sSL https://gitlab.com/fscarmen/warp_unlock/-/raw/main/unlock.sh) -E -U
```

### TG bot 创建方法
转自 北纬37度的大飛 [如何申请Telegram机器人 | 推送通知](https://w37fhy.cn/2364.html)

## Docker 自动解锁方案

* 支持 AMD64 和 ARM64 机器
* Docker 以 alpine 为底包，内置 WGCF
* 每 5 分钟检测一次状态，TG 通知输出
* 容器内 gost 为宿主机提供 socks5 或者 http 服务，端口为 40000，可以在xray/v2ray 配置文件里作相应设置

```
bash <(curl -sSL https://gitlab.com/fscarmen/warp_unlock/-/raw/main/docker.sh)
```

先安装 Docker, 其 IP 为 172.17.0.2 ，获取```docker exec -it wgcf ip route get  172.17.0.1 | grep -oP 'src \K\S+'```
并安装 [mack-a 八合一脚本](https://github.com/mack-a/v2ray-agent)。编辑  ```/etc/v2ray-agent/xray/conf/10_ipv4_outbounds.json```

```
{
    "outbounds": [
        {
            "protocol": "freedom"
        },
        {
            "tag": "media-unlock",
            "protocol": "socks",
            "settings": {
                "servers": [
                    {
                        "address": "172.17.0.2",
                        "port": 40000,
                        "users": []
                    }
                ]
            }
        }
    ],
    "routing": {
        "domainStrategy": "AsIs",
        "rules": [
            {
                "type": "field",
                "domain": [
                    "geosite:netflix"
                ],
                "outboundTag": "media-unlock"
            }
        ]
    }
}
```


## 鸣谢下列作者的文章和项目

互联网永远不会忘记，但人们会。

技术文章和相关项目（排名不分先后）:
* luoxue-bot 解锁 Netflix: https://github.com/luoxue-bot/warp_auto_change_ip
* lmc999 查各大流媒体解锁情况: https://github.com/lmc999/RegionRestrictionCheck
* ginuerzh 的 socks+http 代理: https://github.com/ginuerzh/gost/
* 跨平台构建 Docker 镜像新姿势，x86、arm 一把梭: https://cloud.tencent.com/developer/article/1543689
* Run-On-Arch GitHub Action: https://github.com/marketplace/actions/run-on-architecture#supported-platforms
* Linux 利用systemd开机自启shell脚本: https://blog.csdn.net/qq_41539778/article/details/109361023
* 让你的傻妞稳稳地和机器人GG拍拖！: https://mp.weixin.qq.com/s/77rGQUKg_n5Kz2MqlAUmzw
* 如何高速安装pm2来守护您的进程？: https://www.kejiwanjia.com/jiaocheng/51930.html

服务提供（排名不分先后）:
* CloudFlare Warp(+): https://1.1.1.1/
* WGCF 项目原作者: https://github.com/ViRb3/wgcf/
* 获取公网 IP 及归属地查询: https://ifconfig.co  
https://ip.gs/  
https://ip.sb
* 统计PV网:https://hits.seeyoufarm.com/