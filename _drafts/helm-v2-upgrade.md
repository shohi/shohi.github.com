---
layout: post
title: helm v2之upgrade
category: tech
guid: 368CAFF4-6B93-4428-A447-22A3BDD07C78
tags: [tech, k8s, helm]

---
{% include JB/setup %}

`helm`中用于升级部署的应用的子命令是`upgrade`, 该命令可以说是日常运营中最经常使用的. 但是升级同时也暗含着一个问题-即如何降级. 当升级出错时, helm应该能将应用回滚到升级前的状态并保留升级过程中的日志信息, 以便排查. 本文将简要介绍`helm upgrade`以及其对应的回滚子命令`helm rollback`的一些常用的用法.

## 1. 查看Release的历史版本

```
$> helm history [release-name]

REVISION	UPDATED                 	STATUS    	...
1       	Fri Mar  6 11:13:19 2020	SUPERSEDED
2       	Fri Mar  6 11:18:47 2020	DEPLOYED
```
