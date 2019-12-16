
在互联网公司做安全的IM已经一段时间，研究Signal也有一段时间。Signal是在IT界与安全界都非常有名的一个端对端加密产品，它既符合FS(Forward secrecy，前向安全)，也同时符合PCS(Post-Compromise security，后向安全)。

Signal的核心技术是X3DH（3倍增加版的Diffie Hellman），以及Double Ratchet（双棘轮）。

我打算分开两篇文章详解相关的技术细节：
第一篇：简单讲解相关的技术背景，以及代码级别详解X3DH。
第二篇：详解Double Ratchet双棘轮的算法。

下面开始第一篇，我们先讲讲刚刚提到的技术点：FS前向安全，PCS后向安全，DH算法。然后再讲密码学中的HMAC, KDF, HKDF，这些跟双棘轮有关。然后再细讲X3DH。

## 一些技术背景

### Forward secrecy，前向安全

前向安全，一般人的理解是：如果某一轮的密钥泄漏了，不会导致之前的消息被破解。但我查过一些相关的文献，如Wiki，Handbook of applied cryptography等，定义可能比较多，综合了一下，我更倾向于将前向安全定义为：

**FS/前向安全 = 无论long-term key长期密钥，或者中期密钥，或者某轮密钥泄露，都不会导致之前的消息被破解。**

### Post-Compromise security / Future Secrecy / 后向安全

同样，**我更倾向于将后向安全定义为：在密钥Compromise之后， 在一定时间内，可以恢复。(recovery from compromise)**

### DH (Diffie Hellman) / ECDH

这个到处都有说，不展开了，最简单的理解是：

DH： A的私钥 + B的公钥 = 密钥 = A的公钥 + B的私钥

ECDH就是基于椭圆曲线的Diffie Hellman。

### HMAC

全称Hash-based Message Authentication Code，就是用于生成摘要，验证消息完整性以及源身份。不再展开了。

### KDF

KDF全称是key derivation function，我也不知道怎么翻译好。像上面说的DH出来的密钥，其实不是离散均匀的，更多情况下需要KDF或HKDF

### HKDF

基于HMAC的KDF，细节可以看看其它文章，简单地说，就是

HKDF(key, salt, info) => T(0), T(1), T(2), T(..)个密钥。


## X3DH

我们刚刚说了X3DH就是三倍的DH。从signal官方文档说，X3DH就是下图的样子：

[图1]

图中：
IKA：A的长期Key Pair；
EKA：A的临时Key Pair；
IKB：B的长期Key Pair；
SPKB：B的中期Key Pair；
OPKB：B的临时Key Pair;

图中的1,2,3,4。其实就是做4次ECDH。我们从代码看看他是如何实现的。

PS:我们拿Javascript的代码，更好理解

[图2]

我已经在图上标注了如何做的。简单说，就是：

Final = (DH1 + DH2 + DH3 + DH4)

值得注意的是，像上图的虚线，X3DH并不一定需要OPKB，从代码也可以看到，ECDH4不一定会做。

## Double Ratchet双棘轮

上面说的内容算是比较简单的，双棘轮才是Signal的经典，我们将在下一篇文章详细讲解。如果你对HKDF，HMAC，X3DH还不太清楚，可以多看几遍此文章。

