[![Build Status](https://travis-ci.org/ab77/netflix-proxy.svg?branch=master)](https://travis-ci.org/ab77/netflix-proxy) [![Docker Pulls](https://img.shields.io/docker/pulls/ab77/sniproxy.svg?maxAge=2592000)](https://hub.docker.com/r/ab77/sniproxy/) [![Docker Stars](https://img.shields.io/docker/stars/ab77/bind.svg?maxAge=2592000)](https://hub.docker.com/r/ab77/bind/)
服务由ab77大神编写，这里稍作整理，需要注意的是，此服务用的是旧版服务，因为新版对python3.6安装存在问题。

# 关于
` netflix proxy`是一个智能DNS代理，用于'netflix'、'hulu`[[n2]]（footnotes）、'hbo now'等流媒体的解锁。它使用Docker容器部署，并使用'dnsmasq`[[n18]]（footnotes）和'sniproxy`[[n1]]（footnotes）提供smartdns服务，它适用于一些被屏蔽的网站，如Pornhub和YouTube。

需要注意的是，由于容器不能够在ovz平台上安装（除了ovz7），所以建议使用kvm架构的vps安装此dns解锁服务，此服务建议使用debian系统。

该项目用到了DNS劫持 和 SNI代理。将Netflix的查询请求劫持到中转服务器的IP上，之后通过中转服务器监听443端口的 SNI代理 ，将你的观看请求通过中转服务器处理后发送给Netflix服务器。中转服务器使用SNI代理 ，因此也不会被判断成使用Proxy。

# 脚本安装
> `TL;DR`

find a Debian or Ubuntu box with root on a clean public IP and run:

    apt-get update\
	  && apt-get -y install vim dnsutils curl sudo\
	  && curl -fsSL https://get.docker.com/ | sh || apt-get -y install docker.io\
	  && mkdir -p ~/netflix-proxy\
	  && cd ~/netflix-proxy\
	  && curl -fsSL https://github.com/skytotwo/netflix-proxy/archive/latest.tar.gz | gunzip - | tar x --strip-components=1\
	  && ./build.sh

See the [**Wiki**](https://github.com/skytotwo/netflix-proxy/wiki) page(s) for some common troubleshooting ideas.

... or subscribe to [Unzoner](http://unzoner.com) VPN service to un-block:

<a href="https://dashboard.unzoner.com/sub"><img align="left" src="https://api.unzoner.com/api/v1.0/countries/available/flags.png"></a><br><br>

输入之后回车，等待docker的部署，部署完成之后出现下图所示文字：
![QQ20190404-2138362x-.png](http://picture.totoro.site/images/2019/08/22/QQ20190404-2138362x-.png)

可以看到生成了一个登陆网址和用户名密码，用记事本保存。接着登录网页：
![QQ20190412-1502162x-.png](http://picture.totoro.site/images/2019/08/22/QQ20190412-1502162x-.png)

登陆之后点击「Add IP」，添加需要中转的机器的ip（ipv4/6均可），这样我们就完成了中转的配置。

剩下的就是需要中转机器修改dns指向这个安装dns中转服务的机器的ip即可。

# supported services
The following are supported out of the box, however adding additional services is trivial and is done by updating `dnsmasq.conf` file and running `docker restart dnsmasq`:
* Netflix
* Hulu[[n2]](#footnotes)
* HBO Now
* Amazon Instant Video
* Crackle
* Pandora
* Vudu
* blinkbox
* BBC iPlayer[[n5]](#footnotes)
* NBC Sports and potentially many [more](https://github.com/skytotwo/netflix-proxy/blob/master/proxy-domains.txt)
