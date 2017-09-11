说明：购买机器时，服务器厂商说只有esxi5.5 和6.0版本

因此安装了6.0，其 vsphere client无法设置虚拟机模板和克隆虚拟机；因此没有特别需要，建议不要用esxi6.0，用5.5即可；



操作依赖软件：
vSphere client：通过在浏览器器上登录安装好的机器，访问80端口，如esxi ip时1.1.1.，用浏览器访问1.1.1.1，即可看到client下载链接
Vmware vCenter converter Standalone ：用于拷贝克隆虚机
VMware WorkStation Pro：安装自己主机客户端使用


操作过程：

1、通过浏览器访问 http://esxi-ip ，下载vspherer client 客户端并安装，注意client版本与服务器版本保持一致， client 必须等于高于服务器版本，向下兼容

2、如操作1，下载vcenter converter Standalone，并安装到本地

3、安装VMware WorkStation Pro ，（非必须），因为我的vsphere client 安装ubuntu时，图形操作界面显示不全，安装通过tab执行不下去，因此采用此工具安装系统；

4、通过vsphere client创建虚机， 通过ubuntu ios文件执行安装，配置网络为dhcp，安装好后，关闭电源，作为虚机模板使用

5、通过VMware workstation在本地安装centos7、win10 ，安装好后，关闭电源，作为虚机模板使用


此时已经有了ubuntu虚机模板（esxi主机上），centos&&win10模板（我自己电脑）


6、通过模板生成虚机
生成ubuntu || windows10 ：打开 Vmware vCenter converter Standalone  的功能 convert machine 本地的vmware workstation的ubuntu 虚拟机 （源服务器），选定虚拟机模板，convert到远程 任意一台esxi（目的服务器），等待拷贝完成，启动，进行后续虚机配置调整，即可使用

生成centos虚机：同上，只不过使用Vmware vCenter converter Standalone 拷贝时，虚机模板从 esxi -> esxi ，这两台esxi可以是一台服务器也可以不是一台

注意：通过Vmware vCenter converter Standalone ，支持 vmware workstation 格式的虚机转化为 esxi格式，也支持从esxi转化为workstation格式
，这个是比之前vsphere clinet5.5要强一点的（只支持从workstation到 esxi单向），此为优点
但是凭空多一个Vmware vCenter converter Standalone 中间工具，安装操作都更麻烦，此为缺点

7、下载 vsphere web client：https://my.vmware.com/group/vmware/details?downloadGroup=WEBCLIENTSDK60U2&productId=491
参看官网文档：http://pubs.vmware.com/vsphere-60/index.jsp#com.vmware.vcli.getstart.doc/cli_install.4.7.html#991936

8、安装vcenter（windows server 2008企业版，不要安装标准版）时，提示要安装 windows 2008 sp2 ，下载标准的64位，请不要关闭防火墙等，其他都保持默认配置；通过百度google等搜索，在顶部的搜索结果中一般是官网下载地址，包括操作系统镜像，sp2安装包，vcenter官网只要6.5版本免费下载，可以去百度云盘下载
  另外，windows2008 安装vcenter是iso格式，需要安装daemon-tools，这个通过官网或百度下载的无法安装，可以先安装腾讯软件关键，从里边搜索daemon，找一个安装即可（360的软件管家下载的daemon也不可安装，windows2008好坑），安装deamon 过程中可能要求安装.net framework3或者4的版本，安装即可

vcenter安装：安装好esxi主机后，从浏览器输入 esxi主机IP，网页上会显示出下载vcenter的链接，点击链接进行下载即可获取vcenter  
我安装版本为：VMware-VIM-all-6.5.0-4944578

因此，总结如下，如果么有特别要使用的功能，建议安装esxi5.5或者5.6，操作更方便实用；

标注：win10家庭版不支持远程，又一个坑！！！

9、esxi 6.0.0 license  
0U0QJ-FR1EP-KZQN9-J1C74-23P5R  

10、vcenter注册机  
vcenter注册机：VMware VC6 Serial Generator，见本仓库同名exe程序，经本人验证好用
