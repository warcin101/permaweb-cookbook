---
locale: zh
---
# 创建React App入门套件

本指南将以逐步流程指导您配置开发环境以构建和部署永久Web反应应用程序。

## 先决条件

- 基本的Typescript知识（可选）- [https://www.typescriptlang.org/docs/](学习Typescript)
- NodeJS v16.15.0或更高版本-[https://nodejs.org/en/download/](下载NodeJS)
- 了解ReactJS-[https://reactjs.org/](学习ReactJS)
- 了解git和常用的终端命令

## 开发依赖

- TypeScript
- NPM或Yarn软件包管理器

## 步骤

### 创建项目

如果您对typescript不熟悉，可以排除额外的检查 `--template typescript`

<CodeGroup>
  <CodeGroupItem title="NPM">
  
```console:no-line-numbers
npx create-react-app permaweb-create-react-app --template typescript
```

  </CodeGroupItem>
  <CodeGroupItem title="YARN">
  
```console:no-line-numbers
yarn create react-app permaweb-create-react-app --template typescript
```

  </CodeGroupItem>
</CodeGroup>

## 转到项目目录

```sh
cd permaweb-create-react-app
```

### 安装react-router-dom

您必须安装此软件包以管理不同页面之间的路由

<CodeGroup>
  <CodeGroupItem title="NPM">
  
```console:no-line-numbers
npm install react-router-dom --save
```

  </CodeGroupItem>
  <CodeGroupItem title="YARN">
  
```console:no-line-numbers
yarn add react-router-dom -D
```

  </CodeGroupItem>
</CodeGroup>


### 运行应用程序

现在，在进入下一步之前，我们需要检查一切是否正常，运行
<CodeGroup>
<CodeGroupItem title="NPM">

```console:no-line-numbers
npm start
```

  </CodeGroupItem>
  <CodeGroupItem title="YARN">
  
```console:no-line-numbers
yarn start
```

  </CodeGroupItem>
</CodeGroup>
这将在本地计算机上启动一个新的开发服务器。默认情况下，它使用 `端口3000`，如果此端口已被使用
它可能会要求您切换到终端中的另一个可用端口


### 修改package.json以包含以下配置

```json
{
  ...
  "homepage": ".",
}
```

### 设置路由

现在修改应用程序并添加一个新的路由，如关于页面，首先创建2个其他的.tsx文件。（如果您已排除额外的检查 `--template typescript`，那么您的组件文件扩展名应为 `.jsx` 或 `.js`）

```sh
touch src/HomePage.tsx
touch src/About.tsx
```

#### HomePage.tsx

```ts
import { Link } from "react-router-dom";

function HomePage() {
  return (
    <div>
      欢迎来到永久Web！
      <Link to={"/about/"}>
        <div>关于</div>
      </Link>
    </div>
  );
}

export default HomePage;
```

#### About.tsx

```ts
import { Link } from "react-router-dom";

function About() {
  return (
    <div>
      欢迎来到关于页面！
      <Link to={"/"}>
        <div>首页</div>
      </Link>
    </div>
  );
}

export default About;
```

#### 修改App.tsx

我们需要更新App.tsx以管理不同的页面

```ts
import { HashRouter } from "react-router-dom";
import { Routes, Route } from "react-router-dom";

import HomePage from "./HomePage";
import About from "./About";

function App() {
  return (
    <HashRouter>
      <Routes>
        <Route path={"/"} element={<HomePage />} />
        <Route path={"/about/"} element={<About />} />
      </Routes>
    </HashRouter>
  );
}

export default App;
```

::: info Hash Routing
请注意，我们将路由包装在HashRouter中，并使用react-router-dom的Link组件来构建链接。
这对permaweb当前状态来说非常重要，这将确保路由正常工作，因为应用程序
使用类似于“https://[gateway]/[TX]”的路径服务
:::

## 永久部署

### 生成钱包

我们需要`arweave`软件包来生成一个钱包

<CodeGroup>
<CodeGroupItem title="NPM">

```console:no-line-numbers
npm install --save arweave
```

  </CodeGroupItem>
  <CodeGroupItem title="YARN">
  
```console:no-line-numbers
yarn add arweave -D
```

  </CodeGroupItem>
</CodeGroup>

然后在终端中运行此命令

```sh
node -e "require('arweave').init({}).wallets.generate().then(JSON.stringify).then(console.log.bind(console))" > wallet.json
```

### 设置bundlr

我们需要Bundlr来将应用程序部署到Permaweb，它提供了即时的数据上传和检索

<CodeGroup>
  <CodeGroupItem title="NPM">
  
```console:no-line-numbers
npm install --global @bundlr-network/client
```

  </CodeGroupItem>
  <CodeGroupItem title="YARN">
  
```console:no-line-numbers
yarn global add @bundlr-network/client
```

  </CodeGroupItem>
</CodeGroup>

::: info
您需要将AR添加到该钱包中，并为其充值以能够上传此应用程序。查看[https://bundlr.network](https://bundlr.network)和[https://www.arweave.org/](https://www.arweave.org/)了解更多信息。
:::

### 更新package.json

```json
{
  ...
  "scripts": {
    ...
    "deploy": "bundlr upload-dir ./build -h https://node2.bundlr.network --wallet ./wallet.json -c arweave --index-file index.html --no-confirmation"
  }
  ...
}
```

### 运行构建

现在是生成构建的时候了，运行

<CodeGroup>
  <CodeGroupItem title="NPM">
  
```console:no-line-numbers
npm run build
```

  </CodeGroupItem>
  <CodeGroupItem title="YARN">
  
```console:no-line-numbers
yarn build
```

  </CodeGroupItem>
</CodeGroup>

### 运行部署
最后，我们可以部署我们的第一个Permaweb应用程序

<CodeGroup>
  <CodeGroupItem title="NPM">
  
```console:no-line-numbers
npm run deploy
```

  </CodeGroupItem>
  <CodeGroupItem title="YARN">
  
```console:no-line-numbers
yarn deploy
```

  </CodeGroupItem>
</CodeGroup>

::: tip **成功**
您现在应该在Permaweb上拥有一个React应用程序！做得好！
:::

::: info **错误**
如果收到错误 `Not enough funds to send data`，您需要将一些AR充值到Bundlr钱包中，然后尝试重新部署运行
:::

<CodeGroup>
  <CodeGroupItem title="NPM">
  
```console:no-line-numbers
bundlr fund 1479016 -h https://node1.bundlr.network -w wallet.json -c arweave
```

  </CodeGroupItem>
  <CodeGroupItem title="YARN">
  
```console:no-line-numbers
bundlr fund 1479016 -h https://node1.bundlr.network -w wallet.json -c arweave
```

  </CodeGroupItem>
</CodeGroup>

::: info
上述数字1479016是以winston表示的AR金额，AR的最小单位。此操作需要一些时间传播到Bundlr钱包。请在10-20分钟后返回，然后尝试再次部署。
:::

## 存储库

此示例的完整版本可在此处找到：[https://github.com/VinceJuliano/permaweb-create-react-app](https://github.com/VinceJuliano/permaweb-create-react-app)

## 摘要

这是发布React应用程序在Permaweb上的创建React App版本。您可以发现在Permaweb上部署应用程序的新方式，或者在本指南中找到其他入门套件！
