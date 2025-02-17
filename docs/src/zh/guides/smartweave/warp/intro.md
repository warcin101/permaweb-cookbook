---
locale: zh
---
# Warp (SmartWeave) SDK介绍

Warp 是一个流行的 SmartWeave Protocol SDK。使用 Warp和 Bundlr，您的 SmartWeave 部署和交互可以非常快速。

## 介绍

本指南是Warp SDK及其某些API方法的简短介绍。如果您想了解有关SmartWeave合同的更多信息，请访问[核心概念：SmartWeave](/concepts/smartweave.html)。

::: 提示
您可以在[github](https://github.com/warp-contracts)上找到Warp SDK。如果要深入了解Warp SmartWeave，请访问[Warp网站](https://warp.cc)。
:::

在服务器上使用SDK，您将需要访问wallet.json文件；在浏览器中使用SDK，您将需要连接到一个支持arweave的钱包。

## 安装

要在您的项目中安装warp，您可以使用`npm`或`yarn`或其他npm客户端。

<CodeGroup>
  <CodeGroupItem title="NPM">

```console
npm install warp-contracts
```

  </CodeGroupItem>
  <CodeGroupItem title="YARN">

```console
yarn add warp-contracts
```

  </CodeGroupItem>
</CodeGroup>

## 导入

在使用Warp与您的项目时，根据您的项目设置，有多种导入sdk的方式可供选择。

<CodeGroup>
  <CodeGroupItem title="Typescript">

```ts
import { WarpFactory } from 'warp-contracts'
```

  </CodeGroupItem>
  <CodeGroupItem title="ESM">

```js
import { WarpFactory } from 'warp-contracts/mjs'
```

  </CodeGroupItem>
  <CodeGroupItem title="CommonJS">

```js
const { WarpFactory } = require('warp-contracts')
```

  </CodeGroupItem>
</CodeGroup>


## 连接到环境

有几个不同的环境可以进行交互，您可以使用`forXXXX`辅助函数连接到这些环境。

<CodeGroup>
  <CodeGroupItem title="Mainnet">

```ts
const warp = WarpFactory.forMainnet()
```

  </CodeGroupItem>
  <CodeGroupItem title="Testnet">

```js
const warp = WarpFactory.forTestnet()
```

  </CodeGroupItem>
  <CodeGroupItem title="Local">

```js
const warp = WarpFactory.forLocal()
```

  </CodeGroupItem>
  <CodeGroupItem title="Custom">

```js
const warp = WarpFactory.custom(
  arweave, // arweave-js
  cacheOptions, // { ...defaultCacheOptions, inMemory: true}
  environment // 'local', 'testnet', 'mainnet'
)
```

  </CodeGroupItem>
</CodeGroup>


::: 警告
在使用本地环境时，需要在端口1984上运行 arLocal。
:::


## 摘要

本简介指南旨在帮助您设置 Warp。以下指南将向您展示如何使用Warp SDK部署SmartWeave合同，如何与这些合同进行交互，以及如何发展SmartWeave合同。