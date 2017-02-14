---
layout: post
title:  "Install local yum repository on centos 7"
date:   2017-02-13 22:18:00
categories: linux
comments: true
---

￿## Installing local yum repository on centos 7

```bash
yum install vsftpd # => very secure ftpd.

systemctl enable vsftpd # => enable sftpd service.
systemctl start vsftpd # => start sftpd service.

yum install createrepo # => for creation of local repository.

mkdir /var/ftp/pub/localrepo # => this is where our local repo is.

cp -ar /mnt/Packages/*.* /var/ftp/pub/localrepo/ # => copy an existing repo to your localrepo.

vi /etc/yum.repos.d/localrepo.repo # => point to the local repo.


```