# 调用链码
部署后的链码作为Docker镜像或者是本地进程运行在Peer节点所在服务器。区块链应用客户端不能直接访问链码，所有链码操作通过请求Peer节点的背书服务实现。对于交易类链码操作，Peer节点只是模拟执行，并不会记录到账本，区块链应用客户端需要通过Orderer节点的广播服务提交交易。超级账本中交易提交过程上是异步的，Orderer节点的广播服务只是接受交易提交请求，只有在Orderer节点生成区块，传播到Peer节点，Peer节点记录区块后，才真正完成交易的处理。Peer节点提供事件服务，区块链应用客户端可以通过注册事件服务，从区块链事件中获取交易处理结果。

超级账本是有许可的区块链，区块链应用客户端需要有身份证书才可以访问超级账本。超级账本可配置开启TLS通信协议，若开启TLS通信协议，区块链应用客户端需要进行TLS相关设置。

BaaS平台在启动超级账本网络时，自动生成身份许可相关的证书，并提供用户证书下载功能。此外，为了降低使用的难度，BaaS平台默认超级账本部署中未开启TLS。

## 获取连接参数

访问超级账本网络中的链码，需要建立与超级账本网络中相关服务的连接，连接参数包括Channel名称、Orderer服务地址、Peer背书服务地址、Peer事件服务地址等，参数列表及格式如表-超级账本连接参数表。

可以根据BaaS平台提供的信息属性获取超级账本网络连接参数，属性来源参见表-超级账本连接参数来源表，具体示例参见图-超级账本网络列表示例图、图-超级账本共识信息示例图、图-超级账本通道信息示例图、图-下载MSP证书示例图和图-MSP证书下载内容示例图。

| 参数名                                               | 参数格式                                | 参数示例                                                                                         |
|------------------------------------------------------|---------------------------------------|--------------------------------------------------------------------------------------------------|
| Channel名                                            |                                       | mychannel                                                                                        |
| Ordererer服务地址                                    | gprc://%网络域名%/%Ordererer服务端口% | grpc://k8s.3.cn/32123                                                                            |
| Peer背书服务地址                                     | gprc://%网络域名%/%Peer背书服务端口%  | grpc://k8s.3.cn/31093                                                                            |
| Peer事件服务地址                                     | gprc://%网络域名%/%Peer事件服务端口%  | grpc://k8s.3.cn/32511                                                                            |
| MSP标识                                              |                                       | jdMSP                                                                                            |
| 用户名                                               |                                       | User1                                                                                            |
| 用户私钥文件                                         |                                       | msp/keystore/key.pem                                                                             |
| 用户证书文件                                         |                                       | msp/signcerts/User1@org0.peer.baas.jd.com-cert.pem                                               |

表-超级账本连接参数表

<table class="tg">
  <tr>
    <th class="tg-s268"><br>&nbsp;&nbsp;属性名称<br>&nbsp;&nbsp;</th>
    <th class="tg-s268"><br>&nbsp;&nbsp;属性来源<br>&nbsp;&nbsp;</th>
    <th class="tg-s268"><br>&nbsp;&nbsp;属性示例<br>&nbsp;&nbsp;</th>
  </tr>
  <tr>
    <td class="tg-s268" colspan="3"><br>&nbsp;&nbsp;超级账本界面（图-超级账本网络列表示例图）<br>&nbsp;&nbsp;</td>
  </tr>
  <tr>
    <td class="tg-s268"><br>&nbsp;&nbsp;网络域名<br>&nbsp;&nbsp;</td>
    <td class="tg-s268"><br>&nbsp;&nbsp;网络列表中“网络域名”列<br>&nbsp;&nbsp;</td>
    <td class="tg-s268"><br>&nbsp;&nbsp;k8s.3.cn<br>&nbsp;&nbsp;</td>
  </tr>
  <tr>
    <td class="tg-s268" colspan="3"><br>&nbsp;&nbsp;网络详情界面.共识管理页（图-超级账本共识信息示例图）<br>&nbsp;&nbsp;</td>
  </tr>
  <tr>
    <td class="tg-s268"><br>&nbsp;&nbsp;Ordererer服务端口<br>&nbsp;&nbsp;</td>
    <td class="tg-s268"><br>&nbsp;&nbsp;Ordererer列表中“Ports”列<br>&nbsp;&nbsp;</td>
    <td class="tg-s268"><br>&nbsp;&nbsp;32123<br>&nbsp;&nbsp;</td>
  </tr>
  <tr>
    <td class="tg-s268" colspan="3"><br>&nbsp;&nbsp;网络详情界面.通道管理页（图-超级账本通道信息示例图）<br>&nbsp;&nbsp;</td>
  </tr>
  <tr>
    <td class="tg-s268"><br>&nbsp;&nbsp;Channel名<br>&nbsp;&nbsp;</td>
    <td class="tg-s268"><br>&nbsp;&nbsp;页面左上角下拉框<br>&nbsp;&nbsp;</td>
    <td class="tg-s268"><br>&nbsp;&nbsp;mychannel<br>&nbsp;&nbsp;</td>
  </tr>
  <tr>
    <td class="tg-s268"><br>&nbsp;&nbsp;MSP标识<br>&nbsp;&nbsp;</td>
    <td class="tg-s268"><br>&nbsp;&nbsp;组织列表视图中“MSP标识”列<br>&nbsp;&nbsp;</td>
    <td class="tg-s268"><br>&nbsp;&nbsp;jdMSP<br>&nbsp;&nbsp;</td>
  </tr>
  <tr>
    <td class="tg-s268"><br>&nbsp;&nbsp;Peer背书服务端口<br>&nbsp;&nbsp;</td>
    <td class="tg-s268"><br>&nbsp;&nbsp;组织列表视图中“Ports”列中第一个端口<br>&nbsp;&nbsp;</td>
    <td class="tg-s268"><br>&nbsp;&nbsp;31093<br>&nbsp;&nbsp;</td>
  </tr>
  <tr>
    <td class="tg-s268"><br>&nbsp;&nbsp;Peer事件服务端口<br>&nbsp;&nbsp;</td>
    <td class="tg-s268"><br>&nbsp;&nbsp;组织列表视图中“Ports”列中第二个端口<br>&nbsp;&nbsp;</td>
    <td class="tg-s268"><br>&nbsp;&nbsp;32511<br>&nbsp;&nbsp;</td>
  </tr>
  <tr>
    <td class="tg-s268" colspan="3"><br>&nbsp;&nbsp;下载MSP证书界面（图-下载MSP证书示例图）<br>&nbsp;&nbsp;</td>
  </tr>
  <tr>
    <td class="tg-s268"><br>&nbsp;&nbsp;用户名<br>&nbsp;&nbsp;</td>
    <td class="tg-s268"><br>&nbsp;&nbsp;下载框中选中的用户名<br>&nbsp;&nbsp;</td>
    <td class="tg-s268"><br>&nbsp;&nbsp;User1<br>&nbsp;&nbsp;</td>
  </tr>
  <tr>
    <td class="tg-s268" colspan="3"><br>&nbsp;&nbsp;MSP证书下载内容（图- MSP证书下载内容示例图）<br>&nbsp;&nbsp;</td>
  </tr>
  <tr>
    <td class="tg-0lax"><br>&nbsp;&nbsp;用户私钥文件<br>&nbsp;&nbsp;</td>
    <td class="tg-0lax"><br>&nbsp;&nbsp;keystore目录下key.pem文件<br>&nbsp;&nbsp;</td>
    <td class="tg-0lax"><br>&nbsp;&nbsp;msp/keystore/key.pem<br>&nbsp;&nbsp;</td>
  </tr>
  <tr>
    <td class="tg-0lax"><br>&nbsp;&nbsp;用户证书文件<br>&nbsp;&nbsp;</td>
    <td class="tg-0lax"><br>&nbsp;&nbsp;signcerts目录下的pem文件<br>&nbsp;&nbsp;</td>
    <td class="tg-0lax"><br>&nbsp;&nbsp;msp/signcerts/User1@org0.peer.baas.jd.com-cert.pem<br>&nbsp;&nbsp;</td>
  </tr>
</table>

表-超级账本连接参数来源表

![图片](../../../../image/JD-Blockchain-Open-Platform/Getting-Started/Pic/image010.jpg)

图-超级账本网络列表示例图
 
![图片](../../../../image/JD-Blockchain-Open-Platform/Getting-Started/Pic/image012.jpg)

图-超级账本共识信息示例图

![图片](../../../../image/JD-Blockchain-Open-Platform/Getting-Started/Pic/image014.jpg)
 
图-超级账本通道信息示例图

![图片](../../../../image/JD-Blockchain-Open-Platform/Getting-Started/Pic/image016.jpg)
 
图-下载MSP证书示例图

![图片](../../../../image/JD-Blockchain-Open-Platform/Getting-Started/Pic/image017.png)
 
图-MSP证书下载内容

## 开发应用程序

超级账本提供Java、Node.js和Java版SDK，建议采用Java或Node.js开发超级账本区块链应用客户端。
## Java版开发环境
使用Java版Fabric SDK开发应用客户端，需要准备如下开发环境：
1.	JDK，建议使用JDK 1.8以上版本；
2.	IDE，可使用熟悉的IDE，建议使用Eclipse;
3.	Fabric Java SDK，建议使用与Fabric版本保持一致；
## API说明
Java Fabric SDK中链码调用相关的主要API类关系下图所示。
 
![图片](../../../../image/JD-Blockchain-Open-Platform/Getting-Started/Pic/image019.png) 

HFClient提供客户端环境，通过该类实例初始化超级账本交互的对象。需要注意的是，HFClient中参数初始化有依赖关系，具体细节可参见示例代码。

CryptoSuite定义了PKI接口，PKI相关秘钥生成、签名和验证方法都在此接口中定义，所有PKI实现都要继承该接口。SDK中在CryptoPrimitives提供了基础实现，可通过CryptoSuite.Factory工厂类创建该实现实例。

链码调用功能由Chanel类提供，包括链码查询（queryByChaincode）、发送交易背书（sendTransactionProposal）和发送交易（sendTransaction）。Peer、Ordererer和Event服务分别用于定义Peer节点、Ordererer节点和事件通知服务地址，Channel通过这些定义的地址调用对应服务。

User和Enrollment接口用于提供操作账本时的身份认证信息，User定义了用户基本信息，Enrollment提供证书和对应签名私钥，SDK中未提供User实现，仅提供了Fabric CA对应的Enrollment实现，应用中需要提供自己的实现。

## 示例代码

超级账本是有许可的区块链，只有授权用户才能操作，因此访问超级账本时，需要提供用户身份信息。在Fabric Java SDK中，用户身份认证信息通过User和Enrollment接口定义，应用中通过实例化接口对象提供身份认证信息。

在基于BaaS平台部署管理的链码开发中，通过用户证书下载功能可以获取实例化身份认证信息所需参数，主要包括用户名、MSP标识、签名私钥和CA证书。Enrollment实例化参见示例代码-Enrollment实例化，User实例化参见示例代码-User实例化。

通过Fabric Java SDK 调用链码前，需要指定Channel、Peer背书服务地址、Ordererer广播服务地址、Peer Event服务地址。除此之外，还需要初始化链码调用请求和响应数据的签名和验签等依赖的PKI组件，以及用户的身份标识信息。调用链码前的环境初始化代码参见示例代码-初始化Channel，初始化过程中需要注意各个模块的依赖关系，详情见示例中的NOTE。

超级账本中链码操作可分为两类，一类是执行交易，一类是查询状态。交易类操作，发送请求到一个或多个Peer背书，将Peer背书结果广播到Ordererer服务，通过Peer Event服务监听执行结果，实现方式可参见示例代码-执行交易。查询状态实现比较简单，调用Peer背书服务即可，实现方式可参见示例代码-查询链码数据状态。

```
/**
 * load enrollment from local key and certificate files.
 * 
 * @param keyFile file path of private key
 * @param certFile file path of CA certificate
 * @return  enrollment loaded from local key and certificate files
 * @throws Exception  any exception occurred during  enrollment loading
 */
private static Enrollment loadEnrollment(String keyFile, String certFile) throws Exception {
    PemReader reader = null;
    PemObject pemObj = null;

    // read private key PEM file
    try {
        reader = new PemReader(new java.io.FileReader(keyFile));
        pemObj = reader.readPemObject();
    } finally {
        if(reader != null) {
            try {
                reader.close();
            } catch(Exception e) {}
        }
    }

    // generate private key from PKCS8 encoded data
    EncodedKeySpec privateKeySpec = new PKCS8EncodedKeySpec(pemObj.getContent());;
    KeyFactory generator = KeyFactory.getInstance("ECDSA", BouncyCastleProvider.PROVIDER_NAME);
    final PrivateKey privateKey = generator.generatePrivate(privateKeySpec);


    // read CA certificate content
    final String cert =  IOUtils.toString(new File(certFile).toURI());

    return new Enrollment() {
        public PrivateKey getKey() {
            return privateKey;
        }

        public String getCert() {
            return cert;
        }
    };

}
```

示例代码-Enrollment实例化

```
/**
 * create user with specified MSP, user name and enrollment.
 * 
 * @param user  ID, i.e., unique name of user
 * @param mspId ID of MSP which user belongs to
 * @param enrollment user's enrollment
 * @return  user instance with attributes provided by parameters, and others as default.
 */
private static User createUser(String user, String mspId,  final Enrollment enrollment) {
    return new User() {
        public String getName() {
            return user;
        }

        public Set<String> getRoles() {
            return null;
        }

        public String getAccount() {
            return null;
        }

        public String getAffiliation() {
            return null;
        }


        public Enrollment getEnrollment() {
            return enrollment;
        }

        public String getMspId() {
            return mspId;
        }
    };
}
```

示例代码-User实例化

```
HFClient hfClient = HFClient.createNewInstance();

// NOTE: CryptoSuite must be set first.
hfClient.setCryptoSuite(CryptoSuite.Factory.getCryptoSuite());

// NOTE: User must be set before Ordererer, Peer and EventHub.
hfClient.setUserContext(createUser("User1", "houseMSP",
        loadEnrollment("data/msp/keystore/key.pem", "data/msp/signcerts/User1@house.peer.k8s.3.cn-cert.pem")));

Channel channel = hfClient.newChannel("mychannel");

// NOTE: Ordererer is used to send transaction.
Properties OrderererProp = new Properties();
OrderererProp.setProperty("OrderererWaitTimeMilliSecs", "30000");
channel.addOrdererer(hfClient.newOrdererer("Ordererer", "grpc://k8s.3.cn:30094", OrderererProp));

// NOTE: Peer is used to interact with ChainCode, including transaction and query. 
channel.addPeer(hfClient.newPeer("peer0org0", "grpc://k8s.3.cn:31636"));

// NOTE: EventHub is used to listen block events.
// NOTE: EventHub must be added if transactions state is needed.
channel.addEventHub(hfClient.newEventHub("peer0org0", "grpc://k8s.3.cn:30512"));

// NOTE: channel must be initialized before any ledger operation.
channel.initialize();
```

初始化Channel客户端

```
TransactionProposalRequest txReq = hfClient.newTransactionProposalRequest();
ChaincodeID cid = ChaincodeID.newBuilder().setName("cdemo").build();
        txReq.setChaincodeID(cid);
        txReq.setFcn("invoke");
        txReq.setArgs(new String[] {"12"});
Collection<ProposalResponse> txRsps = channel.sendTransactionProposal(txReq);
CompletableFuture<TransactionEvent> eFuture = channel.sendTransaction(txRsps);
// NOTE: if no EventHub, this function will be blocked. 
TransactionEvent txEvent = eFuture.get();
```

示例代码-执行交易

```
QueryByChaincodeRequest qryReq = hfClient.newQueryProposalRequest();
        qryReq.setChaincodeID(cid);
        qryReq.setFcn("query");
        qryReq.setArgs(new String[] {});
        Collection<ProposalResponse> 
Collection<ProposalResponse> qryRsps =channel.queryByChaincode(qryReq);
```
示例代码-查询链码数据状态

## Nodejs版开发环境

1.	Node, Node需要6.9.x 或者更高版本, 8.4.0 或者更高版本，不支持Node v7+;  NPM版本支持3.10.x 或者更高版本;
2.	IDE, 推荐使用vscode，其他如Sublime Text甚至记事本都可以;
3.	Fabric Nodejs SDK，建议使用与Fabric版本保持一致；

## API说明
SDK由三个模块组成:
1.	api: 为应用程序开发人员提供可插入的api，以提供SDK使用的关键接口的替代实现。对于每个接口都有内置的默认实现;
2.	fabric-client: 这个模块提供api来与基于Hypreledger构建的区块链网络的核心组件交互，即对等体、定序器和事件流;
3.	fabric-ca-client: 该模块提供api与可选组件fabric-ca交互，该组件包含用于成员管理的服务;

## 示例代码
Query：

```
var Fabric_Client = require('fabric-client');
var path = require('path');
var util = require('util');
var os = require('os');
var console = require("console")
var fabric_client = new Fabric_Client();
// setup the fabric network
var channel = fabric_client.newChannel('mychannel');
var peer = fabric_client.newPeer('grpc://192.168.*.*:32683');
channel.addPeer(peer);
var member_user = null;
var store_path = path.join(__dirname, 'hfc-key-store');
console.error('Store path:'+store_path);
var tx_id = null;
// create the key value store as defined in the fabric-client/config/default.json 'key-value-store' setting
Fabric_Client.newDefaultKeyValueStore({ path: store_path
}).then((state_store) => {
    // assign the store to the fabric client
    fabric_client.setStateStore(state_store);
    var crypto_suite = Fabric_Client.newCryptoSuite();
    var crypto_store = Fabric_Client.newCryptoKeyStore({path: store_path});
    crypto_suite.setCryptoKeyStore(crypto_store);
    fabric_client.setCryptoSuite(crypto_suite);
    // get the enrolled user from persistence, this user will sign all requests
    var userOpt = {
            username: 'User1',
            mspid: 'org0MSP',
            //  这里是从网页上下载的证书跟私钥
            cryptoContent: {
                privateKey: './key.pem',
                signedCert: './cert.pem'
            }
        }
        return fabric_client.createUser(userOpt)
}).then((user_from_store) => {
    if (user_from_store && user_from_store.isEnrolled()) {
        console.log('Successfully loaded user1 from persistence');
        member_user = user_from_store;
    } else {
        throw new Error('Failed to get user1.... run registerUser.js');
    }
    fabric_client.setUserContext(user_from_store, true)
    const request = {
        chaincodeId: 'cdemo',
        fcn: 'query',
        args: ['']
    };
    console.log("pass")
    // send the query proposal to the peer
    return channel.queryByChaincode(request);
}).then((query_responses) => {
    console.log("Query has completed, checking results");
    // query_responses could have more than one  results if there multiple peers were used as targets
    if (query_responses && query_responses.length == 1) {
        if (query_responses[0] instanceof Error) {
            console.error("error from query = ", query_responses[0]);
        } else {
            console.log("Response is ", query_responses[0].toString());
        }
    } else {
        console.log("No payloads were returned from query");
    }
}).catch((err) => {
    console.error('Failed to query successfully :: ' + err);
});
```
Invoke：

```
'use strict';
var hfc = require('fabric-client');
var path = require('path');
var util = require('util');
var sdkUtils = require('fabric-client/lib/utils')
const fs = require('fs');
var options = {
    user_id: 'User1',
    msp_id:'Org0MSP',
    channel_id: 'mychannel',
    chaincode_id: 'cdemo',
    peer_url: 'grpc://192.168.*.*:32683',
    event_url: 'grpc://192.168.*.*:32134',
    Ordererer_url: 'grpc://192.168.*.*:31048',
    privateKeyFolder:'./keystore',
    signedCert:'./cert.pem',
};
var channel = {};
var client = null;
var targets = [];
var tx_id = null;
Promise.resolve().then(() => {
    console.log("Load privateKey and signedCert");
    client = new hfc();
    var createUserOpt = {
        username: 'Admin',
        mspid: 'org0MSP',
        cryptoContent: {
            privateKey: './key.pem',
            signedCert: './cert.pem'
        }
    }
//以上代码指定了当前用户的私钥，证书等基本信息
return sdkUtils.newKeyValueStore({
                        path: "/tmp/fabric-client-stateStore/"
                }).then((store) => {
                        client.setStateStore(store)
                        return client.createUser(createUserOpt)
                })
}).then((user) => {
    channel = client.newChannel(options.channel_id);
    let peer = client.newPeer(options.peer_url,
        {}
    );
    var Ordererer = client.newOrdererer(options.Ordererer_url, {});
    channel.addOrdererer(Ordererer);
    targets.push(peer);
    return;
}).then(() => {
    tx_id = client.newTransactionID();
    console.log("Assigning transaction_id: ", tx_id._transaction_id);
    var request = {
        targets: targets,
        chaincodeId: options.chaincode_id,
        fcn: 'invoke',
        args: ['12'],
        chainId: options.channel_id,
        txId: tx_id
    };
    return channel.sendTransactionProposal(request);
}).then((results) => {
    var proposalResponses = results[0];
    var proposal = results[1];
    var header = results[2];
    let isProposalGood = false;
    if (proposalResponses && proposalResponses[0].response &&
        proposalResponses[0].response.status === 200) {
        isProposalGood = true;
        console.log('transaction proposal was good');
    } else {
        console.error('transaction proposal was bad');
    }
    if (isProposalGood) {
        console.log(util.format(
            'Successfully sent Proposal and received ProposalResponse: Status - %s, message - "%s", metadata - "%s", endorsement signature: %s', 
            proposalResponses[0].response.status, proposalResponses[0].response.message,
            proposalResponses[0].response.payload, proposalResponses[0].endorsement.signature));
        var request = {
            proposalResponses: proposalResponses,
             proposal: proposal,
            header: header
        };
         // set the transaction listener and set a timeout of 30sec
        // if the transaction did not get committed within the timeout period,
        // fail the test
        var transactionID = tx_id.getTransactionID();
        var eventPromises = [];
        let eh = client.newEventHub();
        //接下来设置EventHub，用于监听Transaction是否成功写入
        eh.setPeerAddr(options.event_url, {});
        eh.connect();
        let txPromise = new Promise((resolve, reject) => {
            let handle = setTimeout(() => {
                eh.disconnect();
                reject();
            }, 30000);
            //向EventHub注册事件的处理办法
            eh.registerTxEvent(transactionID, (tx, code) => {
                clearTimeout(handle);
                eh.unregisterTxEvent(transactionID);
                eh.disconnect();
                if (code !== 'VALID') {
                    console.error(
                        'The transaction was invalid, code = ' + code);
                    reject();
                 } else {
                    console.log(
                         'The transaction has been committed on peer ' +
                         eh._ep._endpoint.addr);
                    resolve();
                };
            });
        });
        eventPromises.push(txPromise);
        var sendPromise = channel.sendTransaction(request);
        return Promise.all([sendPromise].concat(eventPromises)).then((results) => {
            console.log(' event promise all complete and testing complete');
             return results[0]; // the first returned value is from the 'sendPromise' which is from the 'sendTransaction()' call
        }).catch((err) => {
            console.error(
                'Failed to send transaction and get notifications within the timeout period.'
            );
            return 'Failed to send transaction and get notifications within the timeout period.';
         });
    } else {
        console.error(
            'Failed to send Proposal or receive valid response. Response null or status is not 200. exiting...'
        );
        return 'Failed to send Proposal or receive valid response. Response null or status is not 200. exiting...';
    }
}, (err) => {
    console.error('Failed to send proposal due to error: ' + err.stack ? err.stack :
        err);
    return 'Failed to send proposal due to error: ' + err.stack ? err.stack :
        err;
}).then((response) => {
    if (response.status === 'SUCCESS') {
        console.log('Successfully sent transaction to the Ordererer.'); 
        return tx_id.getTransactionID();
    } else {
        console.error('Failed to Orderer the transaction. Error code: ' + response.status);
        return 'Failed to Orderer the transaction. Error code: ' + response.status;
    }
}, (err) => {
    console.error('Failed to send transaction due to error: ' + err.stack ? err
         .stack : err);
    return 'Failed to send transaction due to error: ' + err.stack ? err.stack :
        err;
});
```
