非对称加密

公钥 - 私钥

公钥加密的东西只能通过私钥解开。私钥加密的数据，公钥也能解开

公钥一般是CA证书在浏览器端给出，私钥是网站后台所有


应用最广泛的是TLS 1.0，接下来是SSL 3.0。

证书下发是在握手阶段，明文

HTTPS和HTTP协议相比提供了：

1. 数据完整性：内容传输经过完整性校验。
2. 数据隐私性：内容经过对称加密，每个连接生成一个唯一的加密密钥。
3. 身份认证：第三方无法伪造服务端（客户端）身份。

TLS/SSL中使用了非对称加密，对称加密以及HASH算法
传输层安全/安全套接层

个人理解（白话）

服务端首先要将证书传给客户端。利用私钥加密。但是私钥加密的数据，公钥是可以解开的，而公钥是公开的(公私钥是一对，私钥只在网站服务端，非公开)，中间代理是可以截获到证书、并篡改公钥的。所以就需要一个机制来鉴别证书真伪。

这里用到了数字签名。第三方机构(比如CA)颁发证书时，将证书信息先HASH，再用自己(CA)的私钥加密为数字签名。然后服务端将证书（包含证书颁发机构名字、证书签名、公钥、Hash算法）传给客户端。

客户端拿到了证书，用CA公钥解密数字签名，得到了证书摘要HASHa；再用证书的Hash算法计算得出HASHb。对比HASHa，HASHb。如果相同，则证明证书是真实可信的。（数字签名无法伪造，因为攻击者不会有CA的私钥，如果有。。。那就事儿大了）

随后再用传来的公钥，生成随机密码，并且加密传回服务端。这个加密数据只有服务端的私钥能解开。待服务端私钥解开拿到密码。之后只有服务端和客户端有这个密码。可以通过对称加密来传输数据。中间代理截获也没用。

（https://www.zhihu.com/question/52493697）

