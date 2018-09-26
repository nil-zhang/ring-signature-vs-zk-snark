# ring-signature-vs-zk-snark

## ring signature 和 zk-snark 特性比较

Ring signature 和 zk-snark 在 blockchain 场景都是确保交易私密性和保护用户隐私的解决方案。
但两种方案在私密性方面还有不小的差别，具体见下图：
1. ring signature 是通过在交易中混入多个public key image来对交易的发送方做隐私保护，但这种方案的私密性是比较有限的，和ring size相关；同时不能对交易接收方和交易金额做隐私保护。
2. zk-snark 是通过零知识证明的方式可以做到对交易发送方和交易金额的强保护，当然也会消耗更多的技术资源和内存空间；同时zk-snark 本身无法做到对交易接收方的隐私保护。
![image](https://github.com/nil-zhang/ring-signature-vs-zk-snark/blob/master/images_folder/key%20technology.png)

当然，单一的技术不可能完全解决实际问题，这就需要对多项技术做组合。如下图所示：
1. Monero with Ring CT 使用 ring signature 来保护发送者隐私，通过 stealth addresses 来保护接受者隐私，而 Pedersen Commitments 可以用来对交易金额做保护。
2. zcash 则使用 zk-snark 对交易发送方和交易金额做保护，使用stealth addresses 来保护接受者隐私。
![image](https://github.com/nil-zhang/ring-signature-vs-zk-snark/blob/master/images_folder/implementation1.png)

虽然通过多项技术组合都做到了发送方、接收方以及交易金额的保护，但ring signature 方案对发送方的保护强度还是比较有限的。
![image](https://github.com/nil-zhang/ring-signature-vs-zk-snark/blob/master/images_folder/implementation2.png)

当然 zcash 的方案在性能上相对于 monero(CryptoNote)会有比较大的差距，二者TPS对比如下：

|  crytocurrency     | zcash     | monero     |
| ---------- | :-----------:  | :-----------: |
| TPS     | 6     | 1600     |

## 增加 ring size (decoy) 对 ring signature 的影响

当前 monero 设置的 ring size 是 5，也就是有 4 个 decoy，社区正在考虑将 ring size 增加到 7 或者 11。下面看一下增加 ring size 带来的影响。
首先增加 ring size 一定会提高安全性，及发送者隐私泄露的比例会进一步降低，通过下图可以看到，在 ring size 为 10 的时候，安全性比 ring size 为 5时提升了 32 倍。
![image](https://github.com/nil-zhang/ring-signature-vs-zk-snark/blob/master/images_folder/ringsize1.png)

