# Mesh 概述规范 1.0.1

## 缩略语
   |ACK| Acknowledgment|确认|
	|AD | Advertising Data|广播数据|
	|AES| Advanced Encryption Standard|先进的加密标准|
	|AID| Application Key Identifier|应用程序密钥标识符|
	|AKF| Application Key Flag|应用程序密钥标志|
	|ASCII| American Standard Code for Information Interchange|美国标准信息交换码|
	|Mesh| Profile / Specification|概述/规范|
	|ATT| Attribute/ Protocol|属性/协议|
	|ATT_MTU| Attribute Protocol Maximum Transmission Unit|属性协议最大交换单元|
	|BR/EDR| Basic Rate / Enhanced Data Rate|基本速率/增强数据速率|
	|CCM| Counter with CBC-MAC|与CBC-MAC对抗|
	|CID| Company Identifier|公司识别码|
	|CMAC| Cipher-based Message Authentication Code|基于密码的消息验证码|
	|CTL| Network control message indication|网络控制消息指示|
	|DST| Destination|目标地址|
	|ECB| Electronic CodeBook|电子密码本|
	|ECDH Elliptic Curve Diffie-Hellman|椭圆曲线Diffie-Hellman|
	|FCS Frame Check Sequence|帧检查序列|
	|FIPS| Federal Information Processing Standards|联邦信息处理标准|
	|FSN| Friend Sequence Number|朋友序列号|
	|GAP| Generic Access Profile|通用访问配置文件|
	|GATT| Generic Attribute Profile|通用属性配置文件|
	|ID| Identifier|识别码|
	|IEEE| Institute of Electrical and Electronics Engineers|电气电子工程师学会|
	|IKM| Input Key Material|输入键材料|
	|IVI| Initialization Vector Index|初始化向量索引|
	|LSO| Least Significant Octet|最低有效八位位组|
	|MAC| Message Authentication Code|消息验证码|
	|MIC| Message Integrity Check|消息完整性检查|
	|MSO| Most Significant Octet|最重要的八位位组|
	|MTU| Maximum Transmission Unit|最大传输单元|
	|NID| Network Identifier|网络识别码|
	|OBO| On Behalf Of (another element)|代表（另一个要素）|
	|OKM| Output Key Material|输出键材料|
	|OOB| Out of Band|带外|
	|PDU| Protocol Data Unit|协议数据单元|
	|PID| Product Identifier|产品标识|
	|RFU| Reserved for Future Use|保留以备将来使用|
	|RPL| Replay Protection List|重播保护列表|
	|RSSI| Received Signal Strength Indicator|接收信号强度指示器|
	|SAR| Segmentation And Reassembly|细分和重组|
	|SEG| Segmentation indication bit|分段指示位|
	|SEQ| Sequence Number|序列号|
	|SRC| Source|源地址|
	|SZMIC| Size of Message Integrity Check|信息完整性检查的大小|
	|TTL| Time To Live|生存时间|
	|URI| Uniform Resource Indicator|统一资源指标|
	|UUID| Universally Unique Identifier|通用唯一标识符|
	|VID| Version Identifier|版本标识符|
	|WG| Working Group|工作组|
	
## 分层结构
Mesh概述规范V1.0.1一共定义了七层网络结构，包括:<br>
* Model Layer(网络模型层)
* Foundation Model Layer(基础模型层)
* Acces Layer(接入层)
* Upper transport Layer(上层传输层)
* Upper transport Layer(下层传输层)
* Network Layer(网络层)
* Bearer Layer(承载层)

### Model Layer(网络模型层)
用于标准化典型用户场景的操作，比如照明和传感器模型
### Foundation Model Layer(基础模型层)
配置和管理Mesh网络的状态，消息和模型
### Acces Layer(接入层)
接入层定义更高层应用程序如何调用上层传输层，定义了应用层数据的格式，定义和控制应用程序数据在上层传输层中的加解密。并检查从上下文接收到应用程序数据的密匙是否正确，如果正确，则将应用程序数据转发到更高层
### Upper transport Layer(上层传输层)
对应用层数据进行加密，解密和身份验证，旨在提供访问消息的安全性。还定义了如何使用传输控制消息来管理节点之前的上层传输层，包括何时由朋友功能使用
### Upper transport Layer(下层传输层)
定义了如何将上层传输层消息分段并重组为多个下层传输PDU，以将大型上层传输层消息传递给其他节点。 还定义了一个控制消息来管理分段和重组。
### Network Layer(网络层)
定义了如何针对一个或多个元素寻址传输消息。 它定义了允许承载层传输传输PDU的网络消息格式。
网络层决定是中继/转发消息，接受消息以进行进一步处理还是拒绝消息。 它还定义了如何加密和认证网络消息。
### Bearer Layer(承载层)
定义了数据是如何在节点之间传输，有两个承载定义，广播承载和GATT承载，或许还会添加更多承载在将来。



