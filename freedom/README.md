# Vultr 搭建 SS(ShadowSocks)教程-超详细（转）
发布于 2018-02-01  1.41k 次阅读

## 国外服务器的购买
这里我选择的是 Vultr，对比了很多国外的服务器，这个蛮靠谱的，且搭建成功后看 youtube1080p 完全无压力。
这里是链接：Vultr The Infrastructure Cloud™
当然，已经有服务器的小伙伴，直接从==快速搭建 ShadowSocks==开始看
Vultr 服务器价格
Vultr 服务器按小时计费,最低 0.004 美元/h,算起来 2.5 美元/月，且 destory 掉服务器是不收费的，所以不用担心如果暂时没有使用还一直扣费的问题，如下图所示：

最低价格的服务器是 512M 的内存，500G 的带宽，只能说 99%的情况下完全够用了！
注册 Vultr
首先打开Vultr 链接，点击 Create Account，如下图

因为 Vultr 的网站是全英文的，对注册还是有要求的，密码的规范如下图所示：

充值 Vultr
注册完成之后就是充值，Vultr 提供 4 种充值方式，如下图：

这里我选择支付宝，因为方便快捷，但是最低消费 10 美元，也不多，60 多人民币，如下图：

付款之后，就可以看到账户的钱多了
选择 VPS 的位置
首先，位置很重要！我们如何选择呢，当然有科学的办法，ping 它！
Vultr 的服务器有很多位置，下面我测试的东京节点和新加坡节点的数据如下：


这么看来还是东京的节点速度比较好，当然这个因人而异，在中国不同的地理位置访问国外不同位置的服务器速度也不一样。（下面提供了下载地址,下载下来双击运行即可）。
根据测速的结果，我选择东京位置的 VPS
创建 VPS
左侧菜单栏 Servers，点击+，如下图：

选择 VPS 的位置，如下图：

选择操作系统和价格，如下图：

点击最下面的 Deploy Now，如下图：

创建成功

VPS 的信息
安装成功之后，点击 Manage

可以看到你购买的 VPS 的信息，如下图所示：

ping 一下 ip 地址，100ms 多一点，这个速度相当可以了，如下图：

## VPS 的使用
下载 Shell
当然是选择先连接它了，我们选择的工具是 XShell
下载地址：Xshell 下载
下载完成之后安装，下一步即可

接着选择免费为家庭/学校

语言选择中文：

安装成功后打开
连接 VPS
打开 Xshell，选择文件->新建，输入 VPS 的 IP，IP 地址就在 Vultr 的管理页面上，如下图所示：

点击确定，输入用户名，默认应该为 root，如下图：

接着输入密码：

连接成功：

### 快速搭建 ShadowSocks(二选一)
一键安装
使用方法
在 Xshell 中依次运行以下命令
wget --no-check-certificate -O shadowsocks.sh https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocks.sh
 
chmod +x shadowsocks.sh
 
./shadowsocks.sh 2>&1 | tee shadowsocks.log
接着按照提醒输入你的密码，端口和加密方式，如下图：


然后可以去听首歌~，成功安装之后有你配置的信息显示，记住这些信息，然后跳过下面的手动安装部分，直接去看客户端连接部分即可，如下图：

以上脚本来源于秋水逸冰
### 手动安装
安装依赖包
在 XShell 的控制台输入：
curl "https://bootstrap.pypa.io/get-pip.py" -o "get-pip.py"
python get-pip.py
一个个的来，如下图：

安装 ShadowSocks
pip install --upgrade pip
pip install shadowsocks
如下图：
创建 ShadowSocks 配置文件
## 单端口
vi /etc/shadowsocks.json
输入以下内容，然后点 ESC 后输入:wq 保存退出
{
  "server": "0.0.0.0",
  "server_port": 2018,
  "password": "12345678",
  "method": "aes-256-cfb"
}
## 多端口
（可选，配置了单端口就不要配置这个）多端口的配置文件如下：
{
  "server": "0.0.0.0",
  "port_password": {
      "8381": "password1",
      "8382": "password2",
      "8383": "password3",
      "8384": "password4"
  },
  "timeout": 300,
  "method": "aes-256-cfb"
}
我采取的是单端口配置，如下图所示：


## 配置防火墙
systemctl stop firewalld.service

## 启动 ShadowSocks 服务
ssserver -c /etc/shadowsocks.json -d start
如图所示：

下面的是关闭，启动成功之后不要执行
关闭 ShadowSocks 服务
ssserver -c /etc/shadowsocks.json -d stop
连接 ShadowSocks，体会科学上网的魅力
Windows 客户端
下载地址：Shadowsocks-4.0.7.zip
下载完成之后解压打开，如下图所示：


