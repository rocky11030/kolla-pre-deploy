安装注意事项和步骤
================
脚本暂时只支持ubuntu系统

主要是pre_install.yml前期准备和网络配置两部分组成

pre_install.yml前期准备主要是hosts.yml更新hostname文件拷贝hosts文件、base安装源和更新ntp、optimize更新内核安装biosdevname优化sysctl.conf和limits.conf、raid.yml主要是除了系统盘外的全部做单盘raid0(需要修改磁盘的数量)、配置ntp配置并重启系统(主要是内核更新和biosdev影响网卡名称，所以重启)

网络配置分为bond和nobond，主要是配置网卡信息，配置管理网、业务网络、存储网络和外网，bond主要用于生产环境，nobond主要用于实施或者测试环境

第一步: 前期准备
-----------------

* inventory: 先修改pre_hosts主机变量,包括hostnane名称变量
* 修改源: 修改local.list本地源的地址
* 修改raid的磁盘数量,查看现在的raid磁盘是否被使用，需要删除子磁盘的数量，autoraid.sh脚本和format disk修改磁盘数量
* 执行命令: ansible-playbook -i pre_hosts pre_install.yml


第二步: net配置
----------------
* inventory: 先修改bond_hosts/nobond_hosts主机变量
* 根据需求修改templates下面的网卡模板
* 执行命令: ansible-playbook -i bond_hosts/nobond_hosts bond_net.yml/nobond_net.yml

