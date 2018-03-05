# Read Me
## Hyperledger Composer环境配置
内容来源：https://hyperledger.github.io/composer/latest/installing/development-tools.html
### CLI tools
```shell
npm install -g composer-cli
npm install -g composer-rest-server
npm install -g generator-hyperledger-composer
npm install -g yo
```

### Playground
```shell
npm install -g composer-playground
```

### IDE 的选用
Atom /  VS Code 均可，VS Code 下载之后可查找插件：Hyperledeger Composer

### Hyperledger Fabric
```shell
mkdir ~/fabric-tools && cd ~/fabric-tools

curl -O https://raw.githubusercontent.com/hyperledger/composer-tools/master/packages/fabric-dev-servers/fabric-dev-servers.zip
unzip fabric-dev-servers.zip

# cd ~/fabric-tools
./downloadFabric.sh
```

### 开始 / 停止 你的 Fabric 网络
#### 开始网络
```shell
cd ~/fabric-tools
./startFabric.sh
./createPeerAdminCard.sh
```
#### 停止网络
```shell
cd ~/fabric-tools
./stopFabric.sh
./teardownFabric.sh
```

### 打开 Playground
`composer-playground`
一般的，上面的命令会自动打开浏览器来到地址为：http://localhost:8080/login 的界面
![playground](https://github.com/tw-bc-group/HyperledgerComposerExample/blob/master/hyperledger-composer-example-code/Image/image1.png?raw=true)

---

## Playground 使用方法指南
内容来源：https://hyperledger.github.io/composer/latest/tutorials/playground-tutorial.html
Playground 使用方法较为简单，直接查看文档即可

---

## Developer Tool 使用方法指南
内容来源：https://hyperledger.github.io/composer/latest/tutorials/developer-tutorial.html
### 对比 Playground
从对比的角度来看，两者所做的事情是一样的，只不过一个在 web 直接编写，一个是在 VS Code / Atom 编写。
以下是两者对比：
![compare](https://github.com/tw-bc-group/HyperledgerComposerExample/blob/master/hyperledger-composer-example-code/Image/image2.png?raw=true)
注：
* .bna 文件是用来导入 Playground 的文件，或可理解为编译生成的文件，类似 Solidity 的 abi，但不等于。

### 建议
在 Hyperledger 编码过程中，两者可配合使用：
1. 用 Dev Tools 书写代码，为代码添加单元测试
2. 编译生成 .bna 文件
3. 导入 Playground
4. 进行链上模拟测试
5. 在 Playground 微调
6. 验证结果
7. 修改文件
8. 将 Dev Tools 文件提交 git

### Dev Tools 使用指南
#### 1. 代码初始化
使用 `yo hyperledger-composer:businessnetwork` 初始化代码。
注：
* 在选择 ::license::时，选择 ::Apache-2.0（默认）::
* 指定命名空间

#### 2. 编写代码
与 Playground 方法一致

#### 3. 生成 .bna 文件
```shell
cd /target-file/
composer archive create -t dir -n .
```
此时会在本地文件夹下生成 .bna 文件

#### 4. Deploy 文件或打开 Playground 导入文件
来源：https://hyperledger.github.io/composer/latest/tutorials/developer-tutorial.html
本地调试时，deploy 方法：
```shell
composer runtime install --card PeerAdmin@hlfv1 --businessNetworkName tutorial-network

composer network start --card PeerAdmin@hlfv1 --networkAdmin admin --networkAdminEnrollSecret adminpw --archiveFile tutorial-network@0.0.1.bna --file networkadmin.card

composer card import --file networkadmin.card

composer network ping --card admin@tutorial-network
```

#### 5. 生成 REST server
1. `composer-rest-server`
2. 选择名称
3. 选择::never usenamespaces::
4. 是否确保生成的 API — No
5. 是否启用事件发表 — Yes
6. 是否支持 TLS 安全 — No
注：可根据需要适当修改

#区块链/Hyperledger#