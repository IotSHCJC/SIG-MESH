# Mesh 概述规范 1.0.1
[SIG Mesh官方链接](https://www.bluetooth.com/specifications/mesh-specifications/)
## 1.缩略语
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
	
## 2.1分层结构
Mesh概述规范V1.0.1一共定义了七层网络结构，包括:<br>
* Model Layer(网络模型层)
* Foundation Model Layer(基础模型层)
* Acces Layer(接入层)
* Upper transport Layer(上层传输层)
* Lower transport Layer(下层传输层)
* Network Layer(网络层)
* Bearer Layer(承载层)

#### 2.1.1 Model Layer(网络模型层)
用于标准化典型用户场景的操作，比如照明和传感器模型
#### 2.1.2 Foundation Model Layer(基础模型层)
配置和管理Mesh网络的状态，消息和模型
#### 2.1.3 Acces Layer(接入层)
接入层定义更高层应用程序如何调用上层传输层，定义了应用层数据的格式，定义和控制应用程序数据在上层传输层中的加解密。并检查从上下文接收到应用程序数据的密匙是否正确，如果正确，则将应用程序数据转发到更高层
#### 2.1.4 Upper transport Layer(上层传输层)
对应用层数据进行加密，解密和身份验证，旨在提供访问消息的安全性。还定义了如何使用传输控制消息来管理节点之前的上层传输层，包括何时由朋友功能使用
#### 2.1.5 Lower transport Layer(下层传输层)
定义了如何将上层传输层消息分段并重组为多个下层传输PDU，以将大型上层传输层消息传递给其他节点。 还定义了一个控制消息来管理分段和重组。
#### 2.1.6 Network Layer(网络层)
定义了如何针对一个或多个元素寻址传输消息。 它定义了允许承载层传输传输PDU的网络消息格式。
网络层决定是中继/转发消息，接受消息以进行进一步处理还是拒绝消息。 它还定义了如何加密和认证网络消息。
#### 2.1.7 Bearer Layer(承载层)
定义了数据是如何在节点之间传输，有两个承载定义，广播承载和GATT承载，或许还会添加更多承载在将来。

## 2.2 网格操作概述

### 2.2.1 网络和子网
本规范定义的Mesh网络操作旨在：<br>
* 使消息能够从一个元素发送到一个或多个元素； •允许通过其他节点中继消息以扩展通信范围；
* 保护消息免受已知的安全攻击，包括窃听攻击，中间人攻击，重播攻击，垃圾桶攻击，蛮力密钥攻击以及可能的其他攻击.这里未记录的安全攻击；
* 在当今市场上的现有设备上工作；
* 及时传递消息；
* 一台或多台设备移动或停止运行时继续工作；
* 具有内置的前向兼容性以支持将来版本的Mesh Profile规范。<br>

该规范定义了一个基于受管理洪水的Mesh网络，该网络使用广播通道传输消息，以便其他节点可以接收消息并中继这些消息；从而扩展了原始消息的范围。只要有足够密度的设备正在侦听和中继消息，托管洪水网状网络中的任何设备都可以随时发送消息。可以考虑添加路由功能并定义基于路由的网状网络的增强功能以便将来对该规范进行修订。本规范使用多种方法来限制在洪水泛滥的网状网络中消息的无限中继。使用的两种主要方法是网络消息缓存方法和生存时间方法。网络消息缓存旨在通过将所有消息添加到缓存列表中来防止设备中继先前收到的消息。收到消息后，将对照列表进行检查，如果已存在，则将其忽略。如果尚未收到，则将其添加到缓存中，以便将来可以忽略。为了防止此列表过长，缓存的消息数受实现方式的限制。每封邮件都包含一个生存时间（TTL）值，该值限制了消息可以中继的次数。每次接收到一条消息，然后由设备进行中继（最多126次），则TTL值将减少1。

### 2.2.2 设备和节点
 一个不是Mesh网络成员的设备被称为没有配置过设备。一个是Mesh网络成员的设备被称为节点。配置者被用于管理未配置设备和节点之间的转换。<br>
一个未配置的设备不能发送和接受Mesh网络的数据。但是，它可以广播它的存在给配置者。未配置设备被验证完之后，配置者将邀请它进入Mesh网络，并将它转换为节点。<br>
一个节点可以发送，接受数据同时也被一个客户端设置者管理。一个节点或许也当作类似于管理者一样的设备，通过Mesh网络去设置这个节点是如何跟其他节点交流的。一个客户端设置者可以将节点移除Mesh网络，将其还原到未配置设备。<br>
在已经被配置到Mesh网络的设备之后，通过将其自身提供给另外一个Mesh网络来支持一个节点的多个实例。Mesh网络的每个实例是
由地址和设备在配置期间获得的设备密钥确定。

### 2.2.3 添加设备到Mesh网络当中
   为了协助配置多个设备，设备具有可由供应商设置的关注计时器。当设置为非零值时，设备将使用可能的任何方式进行自我识别。对于
例如，设备可能会闪烁，发出声音或振动。注意计时器到期后，设备将停止标识自己。这允许预配器将单个消息发送到设备，以使其进行标识，并且设备在给定时间后自动停止标识其自身。<br>
在这两个载体上运行的协议是该协议v4.2的安全管理器协议的派生产品。
蓝牙核心规范，引入了对具有非常有限的用户界面的设备（例如电灯或开关）进行身份验证的能力。安全管理器协议需要可靠的载体，而广告供应载体无法保证这一点；因此，本规范中使用的协议旨在独立于承载而可靠地传递消息。与安全管理器协议的相似性使得能够在实现了这种功能的设备上大量重用现有代码。

### 2.2.4 交流支持
在没有更新的情况下，很多当前的设备不能广播和解析Mesh网络的数据。在Mesh网络中，无需操作系统更新或者硬/软件更新的情况下，为了让这些设备能够和节点通信，该规范允许所有现有设备使用GATT连接。

### 2.2.5 低功耗支持
本规范中的功能使网状网络中的许多设备能够由电池供电或使用诸如能量收集之类的技术。 此类设备可能受限于它们如何充当网状网络的一部分（例如，仅在与之交互时才发送数据的设备）。 本规范不要求设备协调传输，建立连接或在每个连接上重新启动安全性。 从而有利于低功耗操作。 需要低功耗支持的设备可以使用称为“友谊”的概念将自己与始终在线的设备关联，该设备可以代表他们存储和中继消息（请参阅第3.6.6节）。 但是，中继消息的设备将在大多数时间接收消息以及转发消息，并且可能会使用比典型的小型电池或电容器所提供的功率大得多的功率。

## 2.3 建筑概念
这个Mesh网络建筑使用多个不同概念： states, messages, bindings, elements, addressing, models, publish-subscribe, mesh keys, and associations.（状态，消息，绑定，元素，地址，模型，发送-订阅，Mesh密匙，还有协会）
### 2.3.1 States
状态是表示元素条件的值。暴露状态的元素称为服务器。例如，最简单的服务器是通用OnOff服务端，表示它是打开还是关闭。<br>
接收状态的元素被称为客户端。举个例子，最普通的客户端是通用OnOff客户端（二进制开关），它可以通过通用OnOff模型的消息去控制通用OnOff服务端。<br>
由两个或者多个值组成的状态被称为合成状态。举个例子，一个颜色渐变灯可以控制色彩，通过分别控制色彩饱和度和亮度的方式。
### 2.3.2 Bound states
当一个状态被另外一个状态绑定的时候，一个状态的更改会导致另一个状态的更改。绑定状态可能来自于一个或者多个元素的不同模型。一个公共的绑定类型是在一个水平状态和OnOff状态。将这个水平值改成0会将Bound OnOff状态变成关闭，还有将这个水平值变成非0值会将Bound OnOff状态变成开启。
### 2.3.3 Messages	
在Mesh网络内的交流都是通过发送消息完成的。消息操作状态。对于每个状态，服务端支持一组定义的消息和客户端可能使用请求状态值或者改变状态。
一个客户端或许也可以传输不请自来的，携带状态或者改变状态信息的消息。<br>
被定义的消息有一个*操作码*,*相关参数*,和*行为*。一个操作码可以是一个普通的八位位组(对于特殊的消息，可能会要求更大的参数承载)，2个八位位组(标准消息),3个八位位组(供应特殊信息)。
一个总的消息类型，包括操作码，取决于下层传输层，它或许使用了分段和重组(SAR)机制。
### 2.3.4 Elements

### 2.3.5 Addresses

### 2.3.6 Models

### 2.3.7 Example device

### 2.3.8 Publish-subscribe and message exchange



