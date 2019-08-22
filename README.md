[![Build Status](https://travis-ci.org/ab77/netflix-proxy.svg?branch=master)](https://travis-ci.org/ab77/netflix-proxy) [![Docker Pulls](https://img.shields.io/docker/pulls/ab77/sniproxy.svg?maxAge=2592000)](https://hub.docker.com/r/ab77/sniproxy/) [![Docker Stars](https://img.shields.io/docker/stars/ab77/bind.svg?maxAge=2592000)](https://hub.docker.com/r/ab77/bind/)

# about
` netflix proxy`是一个智能DNS代理，用于'netflix'、'hulu`[[n2]]（footnotes）、'hbo now'等流媒体和其他区域外的代理。它使用Docker容器部署，并使用'dnsmasq`[[n18]]（footnotes）和'sniproxy`[[n1]]（footnotes）提供smartdns服务。它适用于一些被屏蔽的网站，如[Pornhub]（http://www.pornhub.com/）和[YouTube]（https://en.wikipedia.org/wiki/blocking-youtube-videos-u在德国）。[订阅]（http://eepurl.com/cb4ruv）邮件列表，并收到新功能、更新等的通知。

需要注意的是，由于容器不能够在ovz平台上安装（除了ovz7），所以建议使用kvm架构的vps安装此dns解锁服务，此服务建议使用debian系统。


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
