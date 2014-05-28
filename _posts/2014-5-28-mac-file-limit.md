---
layout: post
title: git使用goagent代理
description: "git代理"
date: 2014-05-28
modified: 2014-05-28
category: mobile
tags: [ios]
image:
  feature: texture-feature-01.jpg
  credit: Texture Lovers
  creditlink: http://texturelovers.com
comments: true
share: true
---

goagent 设置代理
git config --local --add http.proxy 127.0.0.1:8087
git config --local --unset http.proxy

关闭SSL验证
git config –global http.sslVerify false


