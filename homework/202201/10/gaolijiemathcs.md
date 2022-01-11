# 简述http与https的区别，简述TLS/SSL, HTTP, HTTPS的关系。

## http与https区别

|              | http                                                     | https                                                  |
| ------------ | -------------------------------------------------------- | ------------------------------------------------------ |
| 名称         | Hypertext Transfer protocol 超文本传输协议               | HyperText Transfer Protocol Secure 超文本传输安全协议  |
| 信息是否明文 | http信息明文传输                                         | https通过tls/ssl加密传输协议                           |
| 联系         | 不安全明文传输，未经安全加密协议，传输过程中容易被攻击。 | 可以视为HTTP+TLS/SSL协议组成。                         |
| 地址栏       | http://开头                                              | https://开头                                           |
| 默认端口     | 80                                                       | 443                                                    |
| 通信过程     | TCP连接(3个包)+HTTP通信+关闭TCP连接                      | TCP连接(3个包)+SSL/TLS握手(9个包)+加密通信+关闭TCP连接 |

## 简述TLS/SSL, HTTP, HTTPS的关系。

### 1、HTTPS与HTTP关系

不是新的协议，HTTPS=HTTP+加密+认证+完整性保护【HTTP+TLS/SSL】

TLS可以看做是安全升级版的SSL。

### 2、SSL/TLS解决的问题：

**两种加密方式**

（1）共享秘钥加密：

方式：发送方和接收方用公共的私钥加密，优点较快。

缺点：无法安全的将秘钥从A传递到B

（2）公开秘钥加密：

非对称加密(公钥加密+私钥解密)：

方式：公钥加密，私钥解密，发送放密文用公钥加密，接收方用私钥解密。

缺点：

①无法确保公钥加密，公钥的正确性，例如将公钥替换，那么公钥传输的内容就会被攻击。

②速度慢

**HTTPS采取的方案**

混合加密制度：为了兼顾速度与效率，采用【公开秘钥加密(非对称加密方式)】对【共享秘钥方式的秘钥加密】后面使用共享秘钥进行通信。

但是为了避免【公开秘钥加密方式公钥不可靠问题】提出了一个数字认证机构：CA对公开秘钥颁布证书。

采取的过程：

①使用公钥加密方式交换共享秘钥方式用的秘钥。

②确保交换的秘钥正确，用共享秘钥加密方式进行加密。

例如C S通信：

（1）服务器S将公钥登录到CA机构，CA将私钥向服务器的公钥进行数字签名，颁布公钥证书。【得到服务器公钥+数字证书认证机构的数字签名】

（2）服务器将CA颁发的【公钥+CA数字签名】发给客户端。

（3）客户端去CA验证公钥上的数字签名，确定服务器端的公钥正确性。

（4）客户端用这个可信的公钥去加密发送给服务器端（发送共享秘钥的私钥）。

（5）服务器用自己的私钥解，得到共享秘钥的私钥。

SSL是用于保证HTTPS用于验证公钥正确性，能够争取将公开秘钥取出，在TCP建立连接后，经过TLS握手，客户端获取到经过验证的公钥，就能使用可靠的公钥进行非对称加密的方式通信，在服务端和客户端进行通信。

但是不是都用HTTPS，因为非对称加密以后会有加密解密的开销，并且服务端去CA机构开证书需要钱。因此不是需要加密的，一般使用HTTP即可。
