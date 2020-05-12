# 第1章 介绍

API Box Plus是一款由北京智博万维科技有限公司（以下简称“智博万维”）开发的产品，专为提供API线下服务而设计。通过联动智博万维的API SaaS服务产品API STORE，API Box Plus可以帮助您轻松构建本地API服务应用。

智博万维开发的API Box Plus，具有以下优点：

```
· 使用简单，易于上手；

· 占用资源少；

· 提供丰富多样的API。
```

通过本文档，用户可以快速了解API Box Plus的安装及使用。

若有疑问，欢迎联系我们：support@geek-block.com。  



# 第2章 安装

### 2.1 下载OS镜像

您可以从官方网站(https://www.geek-block.com/#/home/apiBox)下载该OS镜像压缩包，下文以发布的api-box-plus.zip为例。



### 2.2 部署API Box Plus虚拟机

您可以使用压缩软件解压镜像压缩包，并将解压后获得的 apibox-plus.ova 镜像文件导入到vmware workstations平台。

【推荐使用vmware workstation 15.5版本】

以下是vmware workstations导入部署虚拟机方法示例

1、打开vmware workstations软件，在首页中点击“打开虚拟机”，选择解压后的apibox-plus.ova 镜像文件，点击“打开”。

![Image](https://github.com/geek-block/Images/blob/master/API_STORE_and_API_BOX/openware.png)

![Image](https://github.com/geek-block/Images/blob/master/API_STORE_and_API_BOX/openimage.png)

2、可根据实际需要，修改选择虚拟机的存放位置，点击“导入”，等待一段时间后完成API Box Plus虚拟机导入部署。

![Image](https://github.com/geek-block/Images/blob/master/API_STORE_and_API_BOX/importvh.png)



### 2.3 检查和配置网络环境

#### 2.3.1 检查NAT网络和DHCP配置

1、检查“NAT模式”虚拟网络设配器的DHCP设置。

在vmware workstations界面左上角点击“编辑”-》“虚拟网络编辑器”，选中“NAT模式”的虚拟网络设配器。检查确认“使用本地DHCP 服务将IP地址分配给虚拟机”的功能已勾上。

![Image](https://github.com/geek-block/Images/blob/master/API_STORE_and_API_BOX/confignetwork.png)

点击“DHCP设置”，检查DHCP设置中起始地址和结束地址已配置，以满足可分配IP地址给导入的API Box Plus虚拟机。

![Image](https://github.com/geek-block/Images/blob/master/API_STORE_and_API_BOX/DHCP.png)

![Image](https://github.com/geek-block/Images/blob/master/API_STORE_and_API_BOX/DHCP2.png)

2、“NAT模式”设配器启用和配置DHCP 

【注意】如果以上检查发现NAT模式的网络设配器没有启用勾选DHCP服务，或者DHCP设置没有配置合适的IP地址池，才请进行以下操作：

点击右下角的“更改设置”按钮，

![Image](https://github.com/geek-block/Images/blob/master/API_STORE_and_API_BOX/DHCP3.png)

选择NAT模式设配器，勾选“使用本地DHCP 服务将IP地址分配给虚拟机”

![Image](https://github.com/geek-block/Images/blob/master/API_STORE_and_API_BOX/DHCP4.png)

点击“DHCP设置”，配置与子网IP地址相同网段的合适的起始IP地址和结束IP地址后，点击“确定”。

![Image](https://github.com/geek-block/Images/blob/master/API_STORE_and_API_BOX/DHCP5.png)

![Image](https://github.com/geek-block/Images/blob/master/API_STORE_and_API_BOX/DHCP6.png)

完成启用DHCP和DHCP设置之后，点击“应用”再点击“确定”使配置应用生效。  

![Image](https://github.com/geek-block/Images/blob/master/API_STORE_and_API_BOX/DHCP7.png)

#### 2.3.2 配置API Box Plus网卡

1、配置API Box Plus虚拟机网卡为NAT模式

在导入的API Box Plus虚拟机页面中，点击“编辑虚拟机设置”

![Image](https://github.com/geek-block/Images/blob/master/API_STORE_and_API_BOX/configvh.png)

检查和配置“网络设配器”为“NAT模式”，确认“启动时连接”框已勾选。并点击“确定”进行保存。

![Image](https://github.com/geek-block/Images/blob/master/API_STORE_and_API_BOX/setnat.png)



### 2.4 开始使用API Box Plus

在完成以上所有配置之后，点击“开启此虚拟机”开始运行API Box Plus虚拟机。

![Image](https://github.com/geek-block/Images/blob/master/API_STORE_and_API_BOX/runvh.png)

API Box Plus虚拟机启动完成后，机器已默认启动了API Box Plus服务。

您可以通过浏览器访问API Box Plus url地址(http://<IP-address>:18008 )开始使用API Box Plus。

【上述API Box Plus url具体地址请根据实际用户环境，在虚拟机用户登录界面查看获取】

![Image](https://github.com/geek-block/Images/blob/master/API_STORE_and_API_BOX/userpage.png)

【备注】如启动虚拟机时提示如下错误，则需要重启你的电脑进入BIOS配置启用CPU VT-x虚拟化支持  

![Image](https://github.com/geek-block/Images/blob/master/API_STORE_and_API_BOX/CPUVTx.png)

重启电脑并进入BIOS设置页面，找到虚拟化功能选项后，修改为Enable。  

![Image](https://github.com/geek-block/Images/blob/master/API_STORE_and_API_BOX/bios.png)

![Image](https://github.com/geek-block/Images/blob/master/API_STORE_and_API_BOX/bios2.png))

完成启用虚拟化功能配置后按F10并根据提示保存退出BIOS。  

![Image](https://github.com/geek-block/Images/blob/master/API_STORE_and_API_BOX/bios3.png)

设置启用CPU虚拟化技术后开机，再重新运行API Box Plus虚拟机。  



## 第3章 授权

首次使用API BOX需要进行授权。授权码绑定机器唯一信息，如更换机器需要重新申请。

### 3.1 获取授权申请文件

点击获取申请码，得到授权申请文件“request.license”  。

![Image](https://github.com/geek-block/Images/blob/master/API_STORE_and_API_BOX/request.png)

进入**智博万维**官网(https://www.geek-block.com/#/user/info)的个人中心页面，将授权申请文件上传给我们。

![Image](https://github.com/geek-block/Images/blob/master/API_STORE_and_API_BOX/gb1.png)

上传成功后请耐心等待审核结果，预计审核将在1-3个工作日内完成。

![Image](https://github.com/geek-block/Images/blob/master/API_STORE_and_API_BOX/gb2.png)

### 3.2 上传授权文件

授权通过后，点击下载按钮得到授权文件“response.license“

![Image](https://github.com/geek-block/Images/blob/master/API_STORE_and_API_BOX/download.png)

进入API BOX授权页面，将授权文件上传到API BOX，上传成功后将会显示授权信息。

![Image](https://github.com/geek-block/Images/blob/master/API_STORE_and_API_BOX/put.png)



**详细功能使用，请查看用户手册**

