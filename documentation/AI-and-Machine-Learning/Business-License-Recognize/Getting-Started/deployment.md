# 一键部署
  
超级账本网络由隶属不同组织的身份互认Peer和Orderer服务节点组成，通过BaaS平台可实现超级账本网络的一键部署。超级账本“一键部署”页面设置网络部署参数，点击“部署”按钮即可实现部署超级账本网络。

通过“区块链.超级账本”菜单->“超级账本”界面->“一键部署”按钮进入“一键部署”页面，网络部署示例配置如网络部署属性配置示例图所示，参数说明参见网络部署配置属性说明表：
![图片](../../../../image/JD-Blockchain-Open-Platform/Getting-Started/Pic/image001.png)
图-网络部署属性配置示例图


<table class="tg">
  <tr>
    <th class="tg-0pky"><br>&nbsp;&nbsp;参数名<br>&nbsp;&nbsp;</th>
    <th class="tg-0lax"><br>&nbsp;&nbsp;参数值<br>&nbsp;&nbsp;</th>
    <th class="tg-0pky"><br>&nbsp;&nbsp;参数说明<br>&nbsp;&nbsp;</th>
  </tr>
  <tr>
    <td class="tg-0pky"><br>&nbsp;&nbsp;基础信息<br>&nbsp;&nbsp;</td>
    <td class="tg-0lax" colspan="2"><br>&nbsp;&nbsp;Fabric网络中包含的背书（Peer）组织。<br>&nbsp;&nbsp;</td>
  </tr>
  <tr>
    <td class="tg-0pky"><br>&nbsp;&nbsp;区块链名<br>&nbsp;&nbsp;</td>
    <td class="tg-0lax"><br>&nbsp;&nbsp;myfabric<br>&nbsp;&nbsp;</td>
    <td class="tg-0pky"><br>&nbsp;&nbsp;Fabric网络标识名。<br>&nbsp;&nbsp;</td>
  </tr>
  <tr>
    <td class="tg-0pky"><br>&nbsp;&nbsp;版本号<br>&nbsp;&nbsp;</td>
    <td class="tg-0lax"><br>&nbsp;&nbsp;1.0.0<br>&nbsp;&nbsp;</td>
    <td class="tg-0pky"><br>&nbsp;&nbsp;Fabric网络使用的Fabric软件版本号。<br>&nbsp;&nbsp;</td>
  </tr>
  <tr>
    <td class="tg-0pky"><br>&nbsp;&nbsp;域名<br>&nbsp;&nbsp;</td>
    <td class="tg-0lax"><br>&nbsp;&nbsp;baas.jd.com<br>&nbsp;&nbsp;</td>
    <td class="tg-0pky"><br>&nbsp;&nbsp;Fabric网络对外访问域名。<br>&nbsp;&nbsp;</td>
  </tr>
  <tr>
    <td class="tg-0pky"><br>&nbsp;&nbsp;持久化存储<br>&nbsp;&nbsp;</td>
    <td class="tg-0lax"><br>&nbsp;&nbsp;gluster-heketi-2w7jw<br>&nbsp;&nbsp;</td>
    <td class="tg-0pky"><br>&nbsp;&nbsp;Fabric网络中使用的Kubernetes持久化存储类型。<br>&nbsp;&nbsp;</td>
  </tr>
  <tr>
    <td class="tg-0pky"><br>&nbsp;&nbsp;组织列表<br>&nbsp;&nbsp;</td>
    <td class="tg-0lax" colspan="2"><br>&nbsp;&nbsp;Fabric网络中包含的Peer组织。<br>&nbsp;&nbsp;</td>
  </tr>
  <tr>
    <td class="tg-0lax"><br>&nbsp;&nbsp;组织名<br>&nbsp;&nbsp;</td>
    <td class="tg-0lax"><br>&nbsp;&nbsp;org0<br>&nbsp;&nbsp;</td>
    <td class="tg-0lax"><br>&nbsp;&nbsp;Peer组织在Fabric网络中的唯一标志名。Peer组织只能是小写英文字母和数字构成，并且首字符是英文字母。<br>&nbsp;&nbsp;</td>
  </tr>
  <tr>
    <td class="tg-0lax"><br>&nbsp;&nbsp;节点数量<br>&nbsp;&nbsp;</td>
    <td class="tg-0lax"><br>&nbsp;&nbsp;1<br>&nbsp;&nbsp;</td>
    <td class="tg-0lax"><br>&nbsp;&nbsp;组织拥有的Peer节点数量。<br>&nbsp;&nbsp;</td>
  </tr>
  <tr>
    <td class="tg-0lax"><br>&nbsp;&nbsp;用户数量<br>&nbsp;&nbsp;</td>
    <td class="tg-0lax"><br>&nbsp;&nbsp;1<br>&nbsp;&nbsp;</td>
    <td class="tg-0lax"><br>&nbsp;&nbsp;组织中参与的用户数量。<br>&nbsp;&nbsp;</td>
  </tr>
  <tr>
    <td class="tg-0lax" colspan="3"><br>&nbsp;&nbsp;附加组件<br>&nbsp;&nbsp;</td>
  </tr>
  <tr>
    <td class="tg-0lax"><br>&nbsp;&nbsp;区块链浏览器<br>&nbsp;&nbsp;</td>
    <td class="tg-0lax"><br>&nbsp;&nbsp;是<br>&nbsp;&nbsp;</td>
    <td class="tg-0lax"><br>&nbsp;&nbsp;Fabric区块链浏览器。<br>&nbsp;&nbsp;</td>
  </tr>
  <tr>
    <td class="tg-0lax"><br>&nbsp;&nbsp;示例程序<br>&nbsp;&nbsp;</td>
    <td class="tg-0lax"><br>&nbsp;&nbsp;否<br>&nbsp;&nbsp;</td>
    <td class="tg-0lax"><br>&nbsp;&nbsp;marble示例程序。<br>&nbsp;&nbsp;</td>
  </tr>
</table>

表-网络部署配置属性说明表

