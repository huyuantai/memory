# Centos 切换root用户
su -x


# VMware Centos 连接上网
- 1.选择桥接模式
![](/assets/qiaojie.png)

- 2.编辑-虚拟网络编辑器
![](/assets/xuni.png)

- 3.更改配置
![](/assets/genggai.png)

- 4.设置桥接 Realtek ... Controller
![](/assets/sehiji.png)

- 5.centos 更改配置
su -x 切换成root 用户
sudo gedit /etc/sysconfig/network-scripts/ifcfg-ens33

把这一项改为YES（ONBOOT=yes）




