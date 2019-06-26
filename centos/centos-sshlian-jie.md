# 安装openssh-server
yum install -y openssl openssh-server

# 修改配置文件
用vim打开配置文件/etc/ssh/sshd_config
- port 
- PermitRootLogin
- RSAAuthentication，
- PubkeyAuthentication

