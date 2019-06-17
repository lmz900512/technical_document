# SSL/TLS

## SSL/TLS是什么？

**SSL：（Secure Socket Layer，安全套接字层）**，位于可靠的面向连接的网络层协议和应用层协议之间的一种协议层。SSL通过互相认证、使用数字签名确保完整性、使用加密确保私密性，以实现客户端和服务器之间的安全通讯。该协议由两层组成：SSL记录协议和SSL握手协议。

**TLS：（Transport Layer Security，传输层安全协议）**，用于两个应用程序之间提供保密性和数据完整性。该协议由两层组成：TLS记录协议和TLS握手协议

![image-20190617090343230](http://ww4.sinaimg.cn/large/006tNc79ly1g43vlimmsvj31240kgh3d.jpg)

**区别和联系**

1994年，NetScape公司设计了SSL协议（Secure Sockets Layer）的1.0版，但是未发布。

1995年，NetScape公司发布SSL 2.0版。

在1996年，由Netscape和Paul Kocher共同设计的版本SSL 3.0协议发布。SSL 3.0协议获得互联网广泛认可和支持，因特网工程任务组（IETF）接手负责该协议，并将其重命名为传输层安全（TLS）协议。

TLS协议的第一个版本（RFC 2246）于1999年1月发布，实质上就是SSL 3.0协议的适度改进版。虽然TLS协议和SSL协议是同一个协议的迭代升级，但是其重命名后在名称上造成的混淆一直延续到今天，业内通常将二者统称为SSL/TLS协议。

2006年4月，IETF发布TLS 1.1版本（RFC4346），包含一些小的安全改进。

2008年8月，TLS 1.2版本（RFC5246）发布，移除了老旧加密套件，增强了协议的安全性，TLS 1.2协议是目前主流的TLS协议版本。

2018年3月，TLS 1.3协议正式批准问世，成为下一代TLS协议版本。TLS 1.3版本历经长达4年28次草案修改，是迄今为止改动最大的一次，既能提高互联网用户的访问速度，又能增强安全性，大大提升HTTPS连接的速度性能，是非常值得期待的一代TLS版本。

**TLS协议和SSL协议是同一个协议的迭代升级，是同一个协议的不同阶段。TLS 1.0通常被标示为SSL 3.1，TLS 1.1为SSL 3.2，TLS 1.2为SSL 3.3。**



TLS协议的优势是与高层的应用层协议（如[HTTP](https://baike.baidu.com/item/HTTP)、[FTP](https://baike.baidu.com/item/FTP)、[Telnet](https://baike.baidu.com/item/Telnet)等）无耦合对接。应用层协议能透明地运行在TLS协议之上，由TLS协议进行创建加密通道需要的协商和认证。应用层协议传送的数据在通过TLS协议时都会被加密，从而保证通信的私密性。

**SSL/TLS最典型的应用是HTTPS (HTTP over SSL)**



## 为什么使用SSL/TLS，有什么好处？

###**网络通信加密的发展过程**



在开始之前，我们来虚构两个人物， 一个是位于中国的张大胖， 还有一个是位于米国的Bill。

这俩哥们隔着千山万水，通过网络联系上了， 两个人臭味相投，聊得火热。

两个人越聊越投机，天南地北，海阔天空，还夹杂着不少隐私的话题。

**总是有一种被偷看的感觉**

有一天， Bill 突然意识到： 坏了， 我们的通信是明文的， 这简直就是网络上裸奔啊， 任何一个不怀好意的家伙都可以监听我们通信，打开我们发送的数据包，窥探我们的隐私啊。

####**对称加密**

Bill  提议： “要不我们做个数据的加密？ 每次传输之前， 你把消息用一个加密算法加密， 然后发到我这里以后我再解密， 这样别人就无法偷窥了，像这样： ”

![image-20190615171140246](http://ww3.sinaimg.cn/large/006tNc79ly1g41ygi02fvj30zm0jctfm.jpg)



 他说： “Bill 老兄，你生成一个密钥， 然后把密钥发给我， 咱们这就开启加密消息， 让那些偷窥狂人们哭去吧！”

一炷香功夫过去了， Bill 还是没有回音， 张大胖忍不住地催促： “快发啊？！！！”

Bill 终于回复了： “ 我感觉有一双眼睛正在虎视眈眈地盯着我们的通话， 如果我把密钥发给你， 也被他截取了， 那加密岂不白费工夫？”

张大胖沉默了， 是啊， 网络是不安全的， 这密钥怎么安全地发过来啊 ？　

“奥，对了，我下周要去米国旅游，到时候我们见一面，把密码确定下来，写到纸上，谁也偷不走， 这不就结了？”　

“哈哈， 这倒是终极解决之道 ”  Bill 笑了， “不过，我不仅仅和你聊天， 我还要和易卜拉欣，阿卜杜拉， 弗拉基米尔，克里斯托夫，玛格丽特， 桥本龙太郎， 李贤俊， 许木木，郭芙蓉，吕秀才等人通信， 我总不能打着飞的，满世界的和人交换密码吧？ ”

张大胖心里暗自佩服Bill同学的好友竟然遍布全球，看来他对加密通信的要求更加强烈啊！

可是这个加密解密算法需要的密钥双方必须得知道啊， 但是密钥又无法通过网络发送， 这该死的偷窥者！

####**非对称加密**

Bill 和 张大胖的通信无法加密，说话谨慎了不少， 直到有一天， 他们听说了一个叫做RSA的**非对称加密算法**，一下子来了灵感。

这个RSA算法非常有意思，它不是像之前的算法， 双方必须协商一个保密的密钥， 而是有一对儿钥匙， 一个是保密的，称为**私钥**，另外一个是公开的，称为**公钥**。

更有意思的是，**用私钥加密的数据，只有对应的公钥才能解密，用公钥加密的数据， 只有对应的私钥才能解密**。

![image-20190615171924027](http://ww4.sinaimg.cn/large/006tNc79ly1g41yoiufe0j30p80j678m.jpg)



有了这两个漂亮的特性， 当张大胖给Bill发消息的时候， 就可以先用Bill的公钥去加密（反正Bill的公钥是公开的，地球人都知道）， 等到消息被Bill 收到后， 他就可以用自己的私钥去解密（只有Bill才能解开，私钥是保密的 ）

![image-20190615172007110](http://ww4.sinaimg.cn/large/006tNc79ly1g41ypank9oj30zk0u0n7g.jpg)

反过来也是如此， 当Bill 想给张大胖发消息的时候，就用张大胖的公钥加密， 张大胖收到后，就用自己的私钥解密。这样以来，通信安全固若金汤， 没有任何人能窥探他们的小秘密了。

####**中间人攻击**

张大胖把和Bill 聊天的情况给老婆汇报了一次。

老婆告诫他说： “你要小心啊， 你确定网络那边坐着的确实是Bill ?”

![image-20190615172305998](http://ww3.sinaimg.cn/large/006tNc79ly1g41ysffin8j30o213i7i3.jpg)

**看来问题出现在公钥的分发上**！  虽然这个东西是公开的， 但是在别有用心的人看来，截取以后还可以干坏事 ！

 **你到底是谁？**

但是怎么安全地分发公钥呢？ 似乎又回到了最初的问题： 怎么安全的保护密钥？

可是似乎和最初的问题还不一样，这一次的公钥不用保密，但是一定得有个办法声明这个公钥确实是Bill的， 而不是别人的。

怎么声明呢？

张大胖突然想到： 现实中有公证处，它提供的公证材料大家都信任，那在网络世界也可以建立一个这样的具备公信力的**认证中心**， 这个中心给大家颁发一个**证书**， **用于证明一个人的身份**。

这个证书里除了包含一个人的基本信息之外，还有包括最关键的一环：这个人的公钥！

这样以来我拿到证书就可以安全地取到公钥了 ！ 完美！

可是Bill 马上泼了一盆冷水：**证书怎么安全传输？ 要是证书传递的过程中被篡改了怎么办？**

天无绝人之路， 张大胖很快就找到了突破口： **数字签名**。

**为了解决非对称加密中公匙来源的不安全性。我们可以使用数字证书和数字签名来解决。**

简单来讲是这样的， Bill可以把他的公钥和个人信息用一个Hash算法生成一个消息摘要， 这个Hash算法有个极好的特性，**只要输入数据有一点点变化，那生成的消息摘要就会有巨变**，这样就可以防止别人修改原始内容。

![image-20190615173227380](http://ww1.sinaimg.cn/large/006tNc79ly1g41z23dofzj30ou08c41c.jpg)

可是作为攻击者的中间人笑了： “虽然我没办法改公钥，但是我可以把整个原始信息都替换了， 生成一个新的消息摘要， 你不还是辨别不出来？”

####**公证处——认证中心（**简称CA**）**

张大胖说你别得意的太早 ， 我们会让有公信力的认证中心（**简称CA**）用它的私钥对消息摘要加密，形成签名：

![image-20190615173415335](http://ww4.sinaimg.cn/large/006tNc79ly1g41z3z43alj310y088wip.jpg)

这还不算， 还把原始信息和数据签名合并， 形成一个全新的东西，叫做“**数字证书**”

数字证书是用来认证公钥持有者身份合法性的电子文档，以防止第三方冒充行为。数字证书由 **CA（Certifacate Authority）** 负责签发，关键内容包括 **颁发者**、**证书有效期**、**使用者组织**、**使用者公钥** 等信息。数字证书涉及到一个名为 **PKI（Public Key Infrastructure）** 的规范体系，包含了数字证书格式定义、密钥生命周期管理、数字签名及验证等多项技术说明，不在这篇笔记中详细展开。

![image-20190615173444296](http://ww2.sinaimg.cn/large/006tNc79ly1g41z4ixo95j31040qoguw.jpg)

张大胖接着说：当Bill把他的证书发给我的时候， 我就用同样的Hash 算法， 再次生成消息摘要，然后用CA的公钥对数字签名解密， 得到CA创建的消息摘要， 两者一比，就知道有没有人篡改了！

![image-20190615173535228](http://ww3.sinaimg.cn/large/006tNc79ly1g41z5dvgbxj311o0g2tf7.jpg)

中间人恶狠狠地说： “算你小子狠！ 等着吧，我还有别的招。 对了，我且问你， 你这个CA的公钥怎么拿到？　难道不怕我在你传输ＣＡ公钥的时候发起中间人攻击吗？　如果我成功的伪装成了ＣＡ，你这一套体系彻底玩完。”

####**CA与证书链**

CA 数字签名包括两个过程：**签发证书（Signing）** 和 **验证证书（Verification）** 

![image-20190616175519198](http://ww1.sinaimg.cn/large/006tNc79ly1g435c89hz6j30y00u0gtm.jpg)

**证书链**

以访问百度为例

![image-20190615180504965](http://ww2.sinaimg.cn/large/006tNc79ly1g42003v6awj30qw1c0ndj.jpg)

在图片的顶部，我们看到这样一个层次关系：

GlobalSign Root CA -> GlobalSign Organization Validation CA -> baidu.com

这个层次可以抽象为三个级别：

1.  end-user：即 baidu.com，该证书包含百度的公钥，访问者就是使用该公钥将数据加密后再传输给百度，即在 HTTPS 中使用的证书

2.  intermediates：即上文提到的 **签发人 Issuer**，用来认证公钥持有者身份的证书，负责确认 HTTPS 使用的 end-user 证书确实是来源于百度。这类 intermediates 证书可以有很多级，也就是说 **签发人 Issuer 可能会有有很多级** 

3.  root：可以理解为 **最高级别的签发人 Issuer**，负责认证 intermediates 身份的合法性

    这其实代表了一个信任链条，**最终的目的就是为了保证 end-user 证书是可信的，该证书的公钥也就是可信的。**

    ![image-20190615180834333](http://ww2.sinaimg.cn/large/006tNc79ly1g4203p9e4jj315e0ke119.jpg)

    结合实际的使用场景对证书链进行一个归纳：

    1.  为了获取 end-user 的公钥，需要获取 end-user 的证书，因为公钥就保存在该证书中
    2.  为了证明获取到的 end-user 证书是可信的，就要看该证书是否被 intermediate 权威机构认证，等价于是否有权威机构的数字签名
    3.  有了权威机构的数字签名，而权威机构就是可信的吗？需要继续往上验证，即查看是否存在上一级权威认证机构的数字签名
    4.  信任链条的最终是Root CA，他采用自签名，对他的签名只能无条件的信任

    ![image-20190615181124522](http://ww4.sinaimg.cn/large/006tNc79ly1g4206mtr46j314y0p0q8m.jpg)

Root 根证书从何而来呢？除了自行下载安装之外，**浏览器、操作系统等都会内置一些 Root 根证书，称之为 Trusted Root Certificates**。比如 Apple MacOS 官网就记录了操作系统中内置的可信任根证书列表。[macOS High Sierra 中可用的受信任根证书列表](https://support.apple.com/zh-cn/HT208127)

（数字证书是一种普遍使用的身份认证方式，而另外一种认证方式，基于身份标识，也就是和PKI竞争的IBC（Identity-Based Cryptography）体系正在兴起）



#### **SSL/TLS **

不使用SSL/TLS的通信，就是不加密的通信。所有信息明文传播，带来了三大风险。

>   （1） **窃听风险**（eavesdropping）：第三方可以获知通信内容。
>
>   （2） **篡改风险**（tampering）：第三方可以修改通信内容。
>
>   （3） **冒充风险**（pretending）：第三方可以冒充他人身份参与通信。

SSL/TLS协议是为了解决这三大风险而设计的，希望达到：

>   （1） 所有信息都是**加密传播**，第三方无法窃听。
>
>   （2） 具有**校验机制**，一旦被篡改，通信双方会立刻发现。
>
>   （3） 配备**身份证书**，防止身份被冒充。
>
>   互联网是开放环境，通信双方都是未知身份，这为协议的设计带来了很大的难度。而且，协议还必须能够经受所有匪夷所思的攻击，这使得SSL/TLS协议变得异常复杂。



##运行机制 TLS 1.2？

  SSL/TLS协议的基本思路是采用[公钥加密法](http://en.wikipedia.org/wiki/Public-key_cryptography)，也就是说，客户端先向服务器端索要公钥，然后用公钥加密信息，服务器收到密文后，用自己的私钥解密。

但是，这里有两个问题。

**（1）如何保证公钥不被篡改？**

>   解决方法：将公钥放在[数字证书](http://en.wikipedia.org/wiki/Digital_certificate)中。只要证书是可信的，公钥就是可信的。证书的可信由CA和证书链来保证

**（2）公钥加密计算量太大，如何减少耗用的时间？**

>   解决方法：每一次对话（session），客户端和服务器端都生成一个"对话密钥"（session key），用它来加密信息。由于"对话密钥"是对称加密，所以运算速度非常快，而服务器公钥只用于加密"对话密钥"本身，这样就减少了加密运算的消耗时间。

因此，SSL/TLS协议的基本过程是这样的：

>   （1） 客户端向服务器端索要并验证公钥。
>
>   （2） 双方协商生成"对话密钥"。
>
>   （3） 双方采用"对话密钥"进行加密通信。

上面过程的前两步，又称为"握手阶段"（Handshake）。

基于**TLS 1.2 **[RFC5246](https://tools.ietf.org/html/rfc5246 )

TLS 在实现上分为 **记录层** 和 **握手层** 两层，其中握手层又含四个子协议: 握手协议 (handshake protocol)、更改加密规范协议 (change cipher spec protocol)、应用数据协议 (application data protocol) 和警告协议 (alert protocol) 

1.  changecipher spec 协议，the changecipher spec protocol, 用来通知对端从handshake切换到record协议(有点冗余，在TLS1.3里面已经被删掉了)
2.  alert协议，the alert protocol, 用来通知各种返回码，
3.  application data协议， The application data protocol，就是把http，smtp等的数据流传入record层做处理并传输。

![image-20190617090520105](http://ww4.sinaimg.cn/large/006tNc79ly1g43vn2qoixj30v80dmwi5.jpg)

### **握手协议** (handshake protocol)

 TLS握手阶段是发生在TCP建连之后开始进行的，握手其实就是在协商，协商加解密协议所需要的一些参数信息等内容。

 TLS握手过程有单向验证和双向验证之分，简单解释一下，

单向验证就是server端将证书发送给客户端，客户端验证server端证书的合法性等，例如百度、新浪、google等普通的https网站，

双向验证则是不仅客户端会验证server端的合法性，同时server端也会验证客户端的合法性，例如银行网银登陆，支付宝登陆交易等。

TLS握手过程如下：

![006tNc79ly1g4358if83oj30u018xasm](http://ww1.sinaimg.cn/large/006tNc79ly1g43adxr02aj30u018xdmz.jpg)

**Clent Hello**

包含：

>   client支持的协议版本 
>
>   client random value 
>
>   支持的加密套件列表 ……, 
>
>   例如：压缩方法

**Server Hello**

包含：

>   确认使用的协议版本 
>
>   server random value 
>
>   选择的加密套件 …

**加密套件命名**

>   `TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256` 
>
>   `TLS` 协议
>
>   `ECDHE` 密钥交换协议 
>
>   `ECDSA` 身份认证算法
>
>   `AES_128_GCM` 对称加密算法 
>
>   `SHA256` MAC

 **Server Certificate(可选)**

服务器证书，这一步紧随在Server Hello 之后，用来供客户端验证服务器的身份。

 **Server Key Exchange Message(可选)**

```javascript
This message will be sent immediately after the server Certificate message (or the ServerHello message, if this is an anonymous negotiation).
```

这个步骤在Server Certificate后，按照RFC的说法，如果没有Server Certificate，则在Server Hello之后。 

该环节也是可选的。如果秘钥协商算法选用的是诸如RSA这类，则不会发送这部分信息。RFC中的原文是

```javascript
The ServerKeyExchange message is sent by the server only when the server Certificate message (if sent) does not contain enough data to allow the client to exchange a premaster secret.
```

可简单的理解，如果是采用的非对称加密算法来进行秘钥协商，可以通过公钥加密发送预主秘钥的算法不需要发送这部分信息。如RSA，而像DH及其变种这种密钥交换算法则需要通过这个环节发送算法所需的参数信息。

RFC中给出的DH参数结构参考：

```javascript
struct {         
    opaque dh_p<1..2^16-1>;          
	opaque dh_g<1..2^16-1>;          
	opaque dh_Ys<1..2^16-1>;     
} ServerDHParams;     
/* Ephemeral DH parameters */
 dh_p         The prime modulus used for the Diffie-Hellman operation.
 dh_g         The generator used for the Diffie-Hellman operation.
 dh_Ys
```

 **Certificate Request(可选)**

SSL分为单向SSL(One-way SSL)和双向SSL(Two-way SSL)，两者区别主要是server端是否需要对client端进行身份验证，常见场景如银行提供的USB证书。双向SSL，这部分信息会在Server Key Exchange Message之后，单向SSL中，不会发送这部分信息。

 **Server Hello Done**

最后，server发送这部分信息来结束Sever hello， 等待客户端回应。

 **Client Certificate(可选)**

这部分信息是Server Hello Done 之后可以发送的第一部分信息，对应Certificate Request，也是可选部分。

 **Client Key Exchange Message**

这部分信息在Client Certificate之后发送，在单向SSL中，在Server Hello Done后发送。这部分信息包含的最重要的一部分信息是premaster secret(预主密钥)，permaster的说法对应的是RSA，而在DH中对应的是DH exponent。

如果密钥协商算法是RSA， client会生成一个48字节长的预主密钥，然后用server的公钥加密后发送。

如果是DH算法，则发送client端生成的DH public value(dh_Yc)(请参考DH的数学原理), 此外如果之前的client certificate已经加密发送了这个值，那这里也会发送一个空值过去。

 **Certificate Verify(可选)**

这部分信息如果需要发送，会跟随在Client Key Exchange Message部分后。

 **Finished**

在最后，发送完ChangeCipherSpec，验证了密钥交换协议和身份认证成功后，会发送finish信息。至此握手完成。

 **Master Secret**

无论用哪种密钥协商算法，最后的主密钥计算方法是相同的——TLS采用了一个PRF来做主密钥的计算，PRF的参数就是之前的两个随机数加上预主密钥。

```javascript
master_secret = PRF(pre_master_secret,ClientHello.random + ServerHello.random);
```





####**RSA握手**

​	![image-20190617090633930](http://ww1.sinaimg.cn/large/006tNc79ly1g43voe47ucj314b0u0nm9.jpg)

RSA有一个问题，就是如果私钥泄漏，即私钥被第三方知道，那么第三方就能从密码协商过程中解密得到整个通讯秘钥，即只要保存爱丽丝和鲍勃之间所有通讯的报文，等到私钥被泄漏的那一天，那么爱丽丝和鲍勃就没有什么私密性可言了。

这就是所谓的**前向不安全**，私钥参与了密钥交换，安全性取决于私钥是否安全保存。

**前向安全性（Forward Secrecy）**（缩写：FS），有时也被称为**完美前向安全**（英语：Perfect Forward Secrecy，缩写：PFS），是[密码学](https://baike.baidu.com/item/密码学/480001)中通讯协议的安全属性，指的是长期使用的主[密钥](https://baike.baidu.com/item/密钥)泄漏不会导致过去的[会话密钥](https://baike.baidu.com/item/会话密钥)泄漏。

**一对密钥只做一个用途，要么用作非对称加解密，要么用作签名验证，别混着用！**

**一对密钥只做一个用途，要么用作非对称加解密，要么用作签名验证，别混着用！**

**一对密钥只做一个用途，要么用作非对称加解密，要么用作签名验证，别混着用！**

这个要求，决定了一个协议的 PFS（前向安全性），在斯诺登曝光NSA的“[今日捕获，明日破解](https://news.ycombinator.com/item?id=5942534)”政策后，越发重要。	

为了足够安全，我们可以考虑把握手阶段的算法从默认的[RSA算法](http://www.ruanyifeng.com/blog/2013/06/rsa_algorithm_part_one.html)，改为 [Diffie-Hellman算法](http://zh.wikipedia.org/wiki/迪菲－赫尔曼密钥交换)（简称DH算法）。

当前流行的TLS工作过程，证书中的公钥，私钥仅仅签名身份认证使用，不会涉及到对称加密的密钥生成，对称加密的密钥协商算法都是具备前向安全性的DHE算法，RSA密钥协商逐渐成为过去时。

####**DH握手**

采用DH算法后，Premaster secret不需要传递，双方只要交换各自的参数，就可以算出这个随机数。

![img](http://www.ruanyifeng.com/blogimg/asset/2014/bg2014092007.png)

上图中，第三步和第四步由传递Premaster secret变成了传递DH算法所需的参数，然后双方各自算出Premaster secret。DH密钥交换时，服务器私钥没有参与进来。也就是说，私钥即使泄漏，也不会导致会话加密密钥被第三方解密。

###**Session的恢复**

握手阶段用来建立SSL连接。如果出于某种原因，对话中断，就需要重新握手。

这时有两种方法可以恢复原来的session：一种叫做session ID，另一种叫做session ticket。

session ID的思想很简单，就是每一次对话都有一个编号（session ID）。如果对话中断，下次重连的时候，只要客户端给出这个编号，且服务器有这个编号的记录，双方就可以重新使用已有的"对话密钥"，而不必重新生成一把。

![img](http://www.ruanyifeng.com/blogimg/asset/2014/bg2014092009.png)

上图中，客户端给出session ID，服务器确认该编号存在，双方就不再进行握手阶段剩余的步骤，而直接用已有的对话密钥进行加密通信。

Session ID是目前所有浏览器都支持的方法，但是它的缺点在于Session ID往往只保留在一台服务器上。所以，如果客户端的请求发到另一台服务器，就无法恢复对话。session ticket就是为了解决这个问题而诞生的，目前只有Firefox和Chrome浏览器支持。

![img](http://www.ruanyifeng.com/blogimg/asset/2014/bg2014092011.png)

上图中，客户端不再发送Session ID，而是发送一个服务器在上一次对话中发送过来的session ticket。这个session ticket是加密的，只有服务器才能解密，其中包括本次对话的主要信息，比如对话密钥和加密方法。当服务器收到session ticket以后，解密后就不必重新生成对话密钥了。

###**记录协议**

记录协议负责在传输连接上交换的所有底层消息，并且可以配置加密。每一条 TLS 记录以一个短标头开始。标头包含记录内容的类型 (或子协议)、协议版本和长度。原始消息经过分段 (或者合并)、压缩、添加认证码、加密转为 TLS 记录的数据部分。

![image-20190617090728045](http://ww4.sinaimg.cn/large/006tNc79gy1g43vp9mm79j30vo0mc43y.jpg)



记录协议的具体内容这里就不做详述了，有兴趣的可以参考：https://www.codercto.com/a/24035.html



## **TLS 1.3**

TLS 1.3版本从2014年开始开发，到2018年8月份历经了四年，可见是非常大的一个工程，一共有28个草案。

作为TLS1.3协议最重要、最著名的实现，OpenSSL也发布了OpenSSL 1.1.1版本，该版本全面支持TLS 1.3，是一个长期支持版本（LTS），将会有5年的支持，该版本兼容1.1.0版本，OpenSSL官方建议尽快从1.1.0版本升级到1.1.1版本。

另外 Facebook 开源了一个 TLS 1.3 协议实现软件 Fizz，仅仅支持 TLS 1.3版本，不用考虑老的 TLS 版本，会让代码简洁不少

###TLS 1.3的变化

TLS 1.3 废除了RSA 密钥协商机制，而DH可以强制每次生成随机私钥，之后强制销毁，可以保证PFS，这种DH变种叫做DHE。

TLS1.3 废除了HMAC(SHA1, MD5), 只采用AEAD验证完整性，AEAD是AE的变种，可以在解密的同时验证完整性

TLS1.3中，对称加密算法只保留了AES。压缩特性废除。

TLS1.3由于废除了RSA的密钥协商机制，所以握手协议的过程变动较大，比如DH算法的参数1.2前的版本由server生成，整个握手过程2-RTT (round-trip time)，而1.3中，DH参数直接在第一步由client生成，整个握手过程1-RTT。

| TLS1.2 | ![image-20190616150842846](http://ww3.sinaimg.cn/large/006tNc79ly1g430iufffwj318q0r8di6.jpg) |
| ------ | ------------------------------------------------------------ |
| TLS1.3 | ![image-20190616150902542](http://ww3.sinaimg.cn/large/006tNc79ly1g430j6gwhcj313y0q8wgd.jpg) |

1.  在一次新的握手流程中，客户端不仅会发送 Client Hello 同时也会将支持的密码套件以及客户端密钥发送给服务端，相比于 TLS1.2，该步骤节约了一个 RTT

2.  服务端发送 Server Hello ，服务端密钥和证书

3.  客户端接收服务端发过来的信息，使用服务端密钥，同时检查证书完整性，此时加密连接已经建立可以发送 HTTP 请求，整个过程仅仅一个 RTT

    | TLS 1.2 | ![image-20190616151142941](http://ww4.sinaimg.cn/large/006tNc79ly1g430lynsmbj31cc0tgac3.jpg) |
    | ------- | ------------------------------------------------------------ |
    | TLS 1.3 | ![image-20190616151246569](http://ww2.sinaimg.cn/large/006tNc79ly1g430n2hb9rj31a80k40ue.jpg) |

    TLS 1.2 中通过 1 个 RTT 即可完成会话恢复，那么 TLS 1.3 是如何做到 0 RTT 连接的？

    当一个支持 TLS 1.3 的客户端连接到同样支持 TLS 1.3 的服务器时， 客户端会将收到服务器发送过来的 Ticket 通过相关计算，一起组成新的 预共享密钥，PSK （PreSharedKey）。客户端会将该 PSK 缓存在本地，在会话恢复时在 Client Hello 上带上 PSK 扩展，同时通过之前客户端发送的完成（finished）计算出恢复密钥 （Resumption Secret）通过该密钥加密数据发送给服务器。服务器会从会话 Ticket 中算出 PSK，使用它来解密刚才发过来的加密数据。

    至此完成了该 0-RTT 会话恢复的过程。

    

详细的TLS1.3参考[RFC 8446](https://tools.ietf.org/html/rfc8446#page-133) [中文参考](https://www.oschina.net/translate/rfc-8446-aka-tls-1-3?lang=chs&p=1)



参考文档：

https://www.cnblogs.com/qiniu/p/6856012.html

https://www.jianshu.com/p/41f7ae43e37b

https://www.cnblogs.com/814467783sweet/p/9647197.html

<https://www.wosign.com/news/2018-0604-01.htm>

<https://yq.aliyun.com/articles/192991>

https://mp.weixin.qq.com/s/StqqafHePlBkWAPQZg3NrA

https://www.jianshu.com/p/fcd0572c4765

[http://www.ruanyifeng.com/blog/2014/02/ssl_tls.html](http://www.ruanyifeng.com/blog/2014/02/ssl_tls.html)

[http://www.ruanyifeng.com/blog/2014/09/illustration-ssl.html](http://www.ruanyifeng.com/blog/2014/09/illustration-ssl.html)

https://www.jianshu.com/p/9531ac4e29a4

https://www.oschina.net/translate/rfc-8446-aka-tls-1-3?lang=chs&p=1

