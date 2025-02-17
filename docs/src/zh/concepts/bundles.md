---
locale: zh
---
# 交易捆绑/交易打包（Transaction Bundles）

### 什么是捆绑？

---

交易捆绑是一种特殊类型的Arweave交易。它可以将多个其他交易和/或数据项捆绑在其中。由于交易捆绑包含许多嵌套交易，它们是Arweave能够扩展到每秒数千个交易的关键。

用户将交易提交给捆绑服务器，例如[Bundlr.network](https://bundlr.network)，该服务将它们与其他交易组合成一个'bundle'（捆绑），然后将其发布到网络上。

### 捆绑如何帮助Arweave？

---

#### 可用性

捆绑服务保证捆绑的交易可靠地发布到Arweave而不会丢失。

捆绑交易的交易ID会立即可用，这意味着数据可以立即访问，就好像它已经在Arweave网络上一样。

#### 可靠性

由于网络活动频繁等原因，发布到Arweave的交易有时可能无法确认（导致交易丢失）。在这些情况下，交易可能变成**孤立交易**，即被卡在内存池中并最终被删除。

捆绑解决了这个问题，它持续不断地尝试将捆绑的数据发布到Arweave，以确保其不会失败或被卡在内存池中。

#### 可扩展性

捆绑可以存储多达2<sup>256</sup>笔交易，每笔交易都作为单笔交易在Arweave上结算。这使得Arweave的区块空间能够支持几乎任何用例。

#### 灵活性

由于捆绑由构建在Arweave之上的捆绑服务处理，所以它可以使用不同的货币进行存储付费。[Bundlr.network](https://bundlr.network)支持使用多种代币（如ETH、MATIC和SOL）支付将数据上传到Arweave。

### 什么是嵌套捆绑？

---

捆绑可以包含用于上传到Arweave的数据项，而这些数据项本身也可以是一个捆绑。

这意味着可以上传捆绑的捆绑，或者换句话说，**嵌套捆绑**。

嵌套捆绑在理论上没有嵌套深度的限制，这意味着交易吞吐量可以大大增加。

当您有不同的捆绑数据组，您希望保证这些数据组同时上传到Arweave，嵌套捆绑可能会有用。

来源和进一步阅读：

[Bundlr Docs](https://docs.bundlr.network)

[ANS-104 Standard](https://github.com/ArweaveTeam/arweave-standards/blob/master/ans/ANS-104.md)
