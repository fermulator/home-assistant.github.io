---
layout: page
title: "Troubleshooting installation problems"
description: "Common installation problems and their solutions."
date: 2015-01-20 22:36
sidebar: true
comments: false
sharing: true
footer: true
redirect_from: /getting-started/troubleshooting/
---

It can happen that you run into trouble while installing Home Assistant. This page is here to help you solve the most common problems.


#### {% linkable_title pip3: command not found %}
This utility should have been installed as part of the Python 3.4 installation. Check if Python 3.4 is installed by running `python3 --version`. If it is not installed, [download it here](https://www.python.org/getit/).

If you are able to successfully run `python3 --version` but not `pip3`, install Home Assistant by running the following command instead:

```bash
$ python3 -m pip install homeassistant
```

On a Debian system, you can also install python3 by `sudo apt-get install python3`, and pip3 by `sudo apt-get install python3-pip`.

#### {% linkable_title No module named pip %}
[Pip](https://pip.pypa.io/en/stable/) should come bundled with the latest Python 3 but is omitted by some distributions. If you are unable to run `python3 -m pip --version` you can install `pip` by [downloading the installer](https://bootstrap.pypa.io/get-pip.py) and running it with Python 3:

```bash
$ python3 get-pip.py
```

#### {% linkable_title libyaml is not found or a compiler error %}

On a Debian system, install the Python 3 YAML library by `sudo apt-get install python3-yaml`.

#### {% linkable_title distutils.errors.DistutilsOptionError: must supply either home or prefix/exec-prefix -- not both %}
This is a known issue if you're on a Mac using Homebrew to install Python. Please follow [these instructions](https://github.com/Homebrew/brew/blob/master/docs/Homebrew-and-Python.md#note-on-pip-install---user) to resolve it.

#### {% linkable_title No access to the frontend %}
In newer Linux distributions (at least Fedora > 22/CentOS 7) the access to a host is very limited. This means that you can't access the Home Assistant frontend that is running on a host outside of the host machine. Windows and macOS machines may also have issues with this.

To fix this you will need to open your machine's firewall for TCP traffic to port 8123. The method for doing this will vary depending on your operating system and the firewall you have installed. Below are some suggestions to try. Google is your friend here.

- [Windows instructions](http://windows.microsoft.com/en-us/windows/open-port-windows-firewall#1TC=windows-7)
- [macOS instructions](https://support.apple.com/en-us/HT201642)

For systems with **firewalld** (Fedora, CentOS/RHEL, etc.):

```bash
$ sudo firewall-cmd --permanent --add-port=8123/tcp
$ sudo firewall-cmd --reload
```

For UFW systems (Ubuntu, Debian, Raspbian, etc.):

```bash
$ sudo ufw allow 8123/tcp
```

For `iptables` systems (was the default for older distributions):

```bash
$ iptables -I INPUT -p tcp --dport 8123 -j ACCEPT
$ iptables-save > /etc/network/iptables.rules  # your rules may be saved elsewhere
```

#### {% linkable_title After upgrading, your browser login gets stuck at the "loading data" step %}
After upgrading to a new version, you may notice your browser gets stuck at the "loading data" login screen. Close the window/tab and go into your browser settings and delete all the cookies for your URL. You can then log back in and it should work. 

Android Chrome 
chrome -> settings -> site settings -> storage -> search for your URL for Home Assistant-> "clear & reset"

