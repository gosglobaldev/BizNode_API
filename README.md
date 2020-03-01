# BizNode_API
实现接入 Gos 主网



GOS API 接入文档

一、背景
GOS 公链备受交易所关注，为提供与各开发社区及交易所对接需求，提供本文档，帮助个接入公链的技术团队、组织实现与 GOS 公链对接，开发满足交易需求的去中心化应用。

二、功能
1、节点测试
提供接入测试节点：
ENDPOINT:  3.112.175.146
PORT: 8888

即可以通过该节点的8888端口获得 GOS 公链测试接入功能。
GOS目前提供 JS API 实现接入，可以使用如下的 js 库文件：

const { Api, JsonRpc, RpcError } = require(‘gosjs’);
   

2、公私钥创建
eosjs-ecc是gos处理密钥和签名的javascript开发包。

nodejs环境下，使用NPM安装nodejs包：
~$ npm install eosjs-ecc
浏览器环境下，可以在这里下载 预编译的eosjs-ecc库，然后在HTML中引用即可：
<html><head>
  <meta charset="utf-8">
  <!--
  sha512-cL+IQQaQ586s9DrXfGtDheRpj5iDKh2M+xlpfwbhNjRIp4BGQ1fkM/vB4Ta8mc+f51YBW9sJiPcyMDIreJe6gQ== lib/eosjs-ecc.js
  sha512-dYFDmK/d9r3/NCp6toLtfkwOjSMRBaEzaGAx1tfRItC0nsI0hVLERk05iNBQR7uDNI7ludYhcBI4vUiFHdjsTQ== lib/eosjs-ecc.min.js
  sha512-eq1SCoSe38uR1UVuQMwR73VgY8qKTBDc87n2nIiC5WLhn1o2y1U6c5wY8lrigVX7INM8fM0PxDlMX5WvpghKig== lib/eosjs-ecc.min.js.map
  -->
  <script src="https://cdn.jsdelivr.net/npm/eosjs-ecc@4.0.4/lib/eosjs-ecc.min.js"
    integrity="sha512-dYFDmK/d9r3/NCp6toLtfkwOjSMRBaEzaGAx1tfRItC0nsI0hVLERk05iNBQR7uDNI7ludYhcBI4vUiFHdjsTQ=="
    crossorigin="anonymous"></script>
</head><body>
  See console object: eosjs_ecc</body></html>


引用该库文件后，通过以下代码实现公钥创建：
import ecc from 'eosjs-ecc/lib'

// 密码加密       
 const seed = await util.PasswordService.encrypt(password);                // 
// 私钥加密        
const encryptedPrivateKey = util.CryptoAES.encrypt(privateKey, seed);        
// 公钥        
const publicKey =ecc.PrivateKey(privateKey).toPublic().toString('GOS');                



3、账号注册
引用gosjs库文件后，通过以下代码实现账号注册：
var accounts = await api.getKeyAccounts(publicKey); //注意是异步方法

4、转账交易
引用该库文件后，通过以下代码实现转账交易：
交易需要通过 API 对象连接节点：

import {Api,JsonRpc,JsSignatureProvider} from 'eosjs'
import { TextDecoder, TextEncoder } from 'text-encoding'

const rpc = new JsonRpc('http://'+ENDPOINT+':'+8888);const signatureProvider = new JsSignatureProvider(['....']);const api = new Api({rpc,signatureProvider,textDecoder: new TextDecoder(), textEncoder: new TextEncoder() })



5、查询交易
参见 GosJS 文档

6、查询高度
通过以下代码实现查询区块高度：

7、修改账号权限
通过以下代码实现查询区块高度：


8、交易格式分析：

三、接入步骤
1、下载 gosjs.js
2、创建私钥及账号
3、转账测试
4、查询交易
