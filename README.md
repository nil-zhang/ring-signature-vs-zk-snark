# ring-signature-vs-zk-snark

Ring signature 和 zk-snark 在 blockchain 场景都是确保交易私密性和保护用户隐私的解决方案。
但两种方案在私密性方面还有不小的差别，具体见下图：
1. ring signature 是通过在交易中混入多个public key image来对交易的发送方做隐私保护，但这种方案的私密性是比较有限的，和ring size相关；同时不能对交易接收方和交易金额做隐私保护。
2. zk-snark 是通过零知识证明的方式可以做到对交易发送方和交易金额的强保护，当然也会消耗更多的技术资源和内存空间；同时zk-snark 本身无法做到对交易接收方的隐私保护。
![image](https://github.com/nil-zhang/ring-signature-vs-zk-snark/blob/master/images_folder/key%20technology.png)

当然，单一的技术不可能完全解决实际问题，这就需要对多项技术做组合。如下图所示：
1. Monero with Ring CT 使用 ring signature 来保护发送者隐私，通过 stealth addresses 来保护接受者隐私，而 Pedersen Commitments 可以用来对交易金额做保护。
2. zcash 则使用 zk-snark 对交易发送方和交易金额做保护，使用stealth addresses 来保护接受者隐私。
![image](https://github.com/nil-zhang/ring-signature-vs-zk-snark/blob/master/images_folder/implementation1.png)
