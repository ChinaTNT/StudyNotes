# window10 ubuntu配置

+ 配置图形界面

  安装xorg（包括显卡驱动、图形环境库等等一系列软件包）

  sudo apt-get install xorg

  安装xfce4（运行在类Unix操作系统上，提供轻量级桌面环境）

  sudo apt-get install xfce4

  安装xrdp（一种开源的远程桌面协议（RDP）服务器）

  sudo apt-get install xrdp

  配置xrdp（配置端口）

  sudo sed -i 's/port=3389/port=3390/g' /etc/xrdp/xrdp.ini

  向.xsession中写入xfce4-session

  sudo echo xfce4-session >~/.xsession

  重启xrdp服务

  sudo service xrdp restart

  远程桌面连接