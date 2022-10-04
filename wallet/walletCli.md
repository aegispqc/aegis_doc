Wallet Cli Method
=======

## help
	help [ method: string, [ detail: boolean ]]  
          
Arguments:  
1. method (type string, optional)   
Show usage of the method. If not set show all method.  
  
2. detail (type boolean, optional)   
Show more detail.  

---------- 


## setJsonSpace
	setJsonSpace [ indent: boolean ]  
Use space indentation when displaying JSON format.  
  
Arguments:  
1. indent (type boolean, required)   
whether to indent.  
  

---------- 


## setJsonColor
	setJsonColor [ colored: boolean ]
setJsonColor  
Display color when displaying JSON format.  
  
Arguments:  
1. colored (type boolean, required)   
  

---------- 


## clear
	clear  
Clear Screen.  

---------- 


## exit
	exit

<br/>

***wallet***
===========

## generateWallet
	generateWallet (Q&A Wizard)  
Create a new wallet use Q&A Wizard.  

---------- 


## importWalletFile
	importWalletFile [ path: string ]  
Import the wallet file.  
  
Arguments:  
1. path (type string, required)   
Wallet file location.  
  

---------- 


## exportWalletFile
	exportWalletFile [ path: string ] [ exportAllFlag: boolean = false ]  
Export the Wallet file.  
  
Arguments:  
1. path (type string, required)   
Export wallet file location.  
  
2. exportAllFlag (type boolean, optional)   
Whether to export all wallet files.  
  

---------- 


## walletGetSignSysList
	walletGetSignSysList   
  
Get Wallet Sign System List.  
  
Exapmle:  
```
> walletGetSignSysList  
[  
    {  
        pubHash: 'b50fef02252c5f9f____________________________48944fd90e189ad86ab2',  
        version: 0,  
        signType: 0,  
        signName: 'Secp256k1'  
    },  
    {  
        pubHash: 'e89e31e61700e030_____________________________277f06385d607b53370',  
        version: 0,  
        signType: 1,  
        signName: 'Nist_round3_Dilithium2'  
    },  
    {  
        pubHash: '5a114d80df41e71b_____________________________3212d332da1569b5273',  
        version: 0,  
        signType: 2,  
        signName: 'Nist_round3_Dilithium3'  
    },  
    {  
        pubHash: '8d24c577cf1b8d2f_____________________________fe8cd8f9e0662335026',  
        version: 0,  
        signType: 3,  
        signName: 'Nist_round3_falcon512'  
    },  
    {  
        pubHash: 'be759e4cada79d07____________________________1da3cf353e8b0d441d8a',  
        version: 0,  
        signType: 4,  
        signName: 'Nist_round3_falcon1024'  
    }  
]  
```
  

---------- 


## walletAddAddress
	walletAddAddress (Q&A Wizard)  
Create a wallet address use Q&A Wizard.  
  
  * [level] The number of required signatures out of the addresses.  
  * [fakeAmount] Number of fake pqcert, default is 1.  
  * [shuffle] Whether to switch the order of signatures.  
  
  

---------- 


## walletGetAddressList
	walletGetAddressList  
Get all addresses for the wallet.  
  
Result:  
```
[  
    "address1",  
    "address2",  
    ...  
]  
```
  

---------- 


## walletGetAddressDetails
	walletGetAddressDetails [ address: string ] [ origin: boolean = false ]  
          
Arguments:  
1. address (type string, required)  
The wallet address.  
  
2. origin (type boolean, optional, default = false)  
show address origin data.  
  

---------- 


## walletGetBalance
	walletGetBalance
Returns the total available balance for all wallet address.  
  
Result:  
```
{  
    "sub": {  
        "walletAddress1": {  
            "avl": "available balance",  
            "lock": "0"  
        },  
        "walletAddress2": {  
            "avl": "available balance",  
            "lock": "0"  
        }  
    },  
    "total": {  
        "avl": "total available balance",  
        "lock": "0"  
    }  
}  
```


---------- 


## walletSend
	walletSend [ srcAddress: string ] [ tgtAddress: string ] [ value: number ] [ signSelect: number[], [ opReturnStr: string, [ feeRatio: number = 1, [ checkFlag: boolean ]]]]  
The easy method. One-time transaction generation.  
  
Arguments:  
1. srcAddress (type string, required)  
Send address.  
  
2. tgtAddress (type string, required)  
Target address.  
  
3. value (type number, required)  
send amount of coin.  
  
4. signSelect (type number[], optional)  
This transaction is signed using the selected signature. And the length of the signature is related to the renewal fee.  
  
5. opReturnStr (type string, optional)  
Message  
  
6. feeRatio (type number, optional, default = 1)  
Fee ratio. Do not less than 1.   
  
7. checkFlag (type boolean, optional, default = true)  
check Flag. Whether to make the final confirmation. 


---------- 


## walletSendMany: 
	walletSendMany [ srcAddress: string ] [ target: { address: string, value: string }[] ] [ signSelect: number[], [ opReturnStr: string, [ feeRatio: number = 1, [ useAllUTXO: boolean, [ changeAddress: string, [ checkFlag: boolean ]]]]]]
Send to multiple addresses.

Arguments:
1. srcAddress (type string, required)
Send address.

2. target (type Array, required)
Target address and amount.</br>
```
Format:
{ address: string, value: string }[]

Example:
[{ "address": "address1", "value": "100" }, { "address": "address2", "value": "100" }]
```
3. signSelect (type number[], optional)
This transaction is signed using the selected signature. And the length of the signature is related to the renewal fee.

4. opReturnStr (type string, optional)
Message

5. feeRatio (type number, optional, default = 1)
Fee ratio. Do not less than 1. 

6. useAllUTXO (type boolean, optional)
Whether to use all the UTXO.

7. changeAddress (type string, optional)
Address for change.

8. checkFlag (type boolean, optional, default = true)
check Flag. Whether to make the final confirmation.


---------- 


## walletASend:
	walletASend [ srcAddressList: string[] ] [ target: {address: string, value: string }[]} ]  [ feeRatio: number = 1 ]
Advanced walletSend.

Arguments:
1. srcAddress (type string[], required)
Send address.
```
Example:
[ "address1", "address2", "address3", ... ]
```

2. target (type object[], required)
Target address and amount.
```
Format:
{ address: string, value: string }[]

Example:
[{ "address": "address1", "value": "100" }, { "address": "address2", "value": "100" }]
```

3. feeRatio (type number, optional, default = 1)
Fee ratio. Do not less than 1. 
`



## walletCreateNewTransation
	walletCreateNewTransation [ srcAddress: string ] [ tgtAddress: string ] [ value: number ] [ extraValue: number = 10000, [ rawFlag: boolean = true, [ tempFlag: boolean = true ]]]
Add a new transaction.  
          
Arguments:  
1. srcAddress (type string, required)  
Send address.  
  
2. tgtAddress (type string, required)  
Target address.  
  
3. value (type number, required)  
send amount of coin.  
  
4. extraValue (type number, optional, default = 10000n)  
Amount reserved for fee.  
  
5. rawFlag (type boolean, optional, default = true)  
Whether the transaction is expressed in raw.  
  
6. tempFlag (type boolean, optional, default = true)  
Save this transaction raw temporarily.  
  

---------- 


## txAddPqcertRoot
	txAddPqcertRoot [ address: string ] [ txRaw?: string ]  
Transaction add pqcert root.  
     
Arguments:  
1. address (type string, required)  
address requires Pqcert.  
  
2. txRaw (type string, optional)  
Transaction raw.  
  

---------- 


## txAddPqcertPubKey
	txAddPqcertPubKey [ pubHash: string ] [ txRaw?: string ]  
Adding pqcert public keys to transaction.  
  
Arguments:  
1. pubHash (type string, required)  
pqcert public keys hash.  
  
2. txRaw (type string, optional)  
Transaction raw.  
  

---------- 


## signTx
	signTx [ address: string ] [ signSelect: number[] ] [ feeRatio: number = 1, [ rawFlag: boolean = true, [ tempFlag: boolean = true, [ autoAddPqcert: boolean = true, [ txRaw: string ]]]]  
sign transaction.  
  
Arguments:  
1. address (type string, required)  
address requires sign.  
  
2. signSelect(type number[], required)  
This transaction is signed using the selected signature. And the length of the signature is related to the renewal fee.  
  
3. feeRatio (type number, optional, default = 1)  
Fee ratio. Do not less than 1.   
  
4. rawFlag (type boolean, optional, default = true)  
Whether the transaction is expressed in raw.  
  
5. tempFlag (type boolean, optional, default = true)  
Save this transaction raw temporarily.  
  
6. autoAddPqcert (type boolean, optional, default = true)  
Auto add pqcert.  
  
7. txRaw (type string, optional)  
Transaction raw.  
  

---------- 


## checkSignPqcert
	checkSignPqcert [ address: string ] [ signSelect: number[] ] [ returnObj: boolean = false ]  
Verify that the pqcert has been submitted.  
  
Arguments:  
1. address (type string, required)  
address requires sign.  
  
2. signSelect (type number[], required)  
This transaction is signed using the selected signature. And the length of the signature is related to the renewal fee.  
  
3. returnObj (type boolean, optional, default = false)  
Whether to send back object data.  
  

---------- 


## getTxTemp
	getTxTemp [ rawFlag: boolean = true ]  
get Temporary transaction data.  
  
Arguments:  
1. rawFlag (type boolean, optional, default = true)  
Whether the transaction is expressed in raw.  
  
  

---------- 


## sendTxTemp
	sendTxTemp
Send the temporary transaction data to rpc server.  
  

---------- 


## sendTx
	sendTx [ txRaw: string ]
Send the transaction by raw.  
  
Arguments:  
1. txRaw (type string, required)  
raw of transaction.  
  

---------- 


## switchWallet
	switchWallet [ walletID: number ]  
  
Arguments:  
1. walletID (type number, required)  
  

---------- 


## getWalletList
	getWalletList  

---------- 


## getStatus
	getStatus  
Get wallet & rpc server status.  

show info:	   
*  time  
*  nowHeight  
*  difficulty  
*  mining  
*  walletReindexing  
*  txPoolLen  
*  memoryUsed  
*  nowWalletID   
  

---------- 


## blockTxJson2Raw
	blockTxJson2Raw [ jsonData: object ]  
Serialize the block transaction in Json format to raw format.  
  
Arguments:  
1. jsonData (type object, required)   
The block transaction in Json format.  
  

---------- 


## blockTxRaw2Json
	blockTxRaw2Json [ rawStr: string ]  
Transform the block transaction in raw format to Json format.  
  
Arguments:  
1. rawStr (type string, required)   
The block transaction in raw format.  
  

<br/>

***rpc server***
==========
## getLastBlock
	getLastBlock [ txsFlag: boolean = false, [ rawFlag: boolean = false ]]
  
Arguments:  
1. txsFlag (type boolean, optional, default = false)  
Whether to return the transactions.  
  
2. rawFlag (type boolean, optional, default = false)  
Whether the transaction is expressed in raw.  
  

---------- 


## getBlockDataByHash
	getBlockDataByHash [ hash: string ] [ txsFlag: boolean = false, [ rawFlag: boolean = false ]]  
  
Arguments:  
1. hash (type string, required)  
This block hash.  
  
2. txsFlag (type boolean, optional, default = false)  
Whether to return the transactions.  
  
3. rawFlag (type boolean, optional, default = false)  
Whether the transaction is expressed in raw.  
  

---------- 


## getBlockDataByHeight
	getBlockDataByHeight [ height: number ] [ txsFlag: boolean = false, [ rawFlag: boolean = false ]] 
Get the block data by Height.  
  
Arguments:  
1. height (type number, required)  
Want to get height of the block.  
  
2. txsFlag (type boolean, optional, default = false)  
Whether to return the transactions.  
  
3. rawFlag (type boolean, optional, default = false)  
Whether the transaction is expressed in raw.  
  

---------- 


## getTransactionByTxid
	getTransactionByTxid [ txid: string ] [ rawFlag?: boolean ]  
Get transaction By transaction id.  
  
Arguments:  
1. txid (type string, required)  
Want to get the height of the block.  
  
2. rawFlag (type boolean, optional, default = false)  
Whether the transaction is expressed in raw.  
  

---------- 


## getPqcertByHash
	getPqcertByHash [ pqcertHash: string ] [ raw?: boolean ]  
Get pqcert By pqcert hash.  
  
Arguments:  
1. pqcertHash (type string, required)  
  
2. rawFlag (type boolean, optional, default = false)  
Whether the transaction is expressed in raw.  
  

---------- 


## getTxPoolList
	getTxPoolList #Get a list of cache and mining transactions  
Get a list of cache and mining transactions.  
  

---------- 


## getTxPool
	getTxPool [ txid: string ]  
Get the transaction in the list of cache and mining transactions with transaction ID.  
  
Arguments:  
1. txid (type string, required)  
Txid of the transaction in the list of cache and mining transactions.  
  

---------- 


## newBlock
	newBlock [ block: object ]  
Add a new block.  
  
Arguments:  
1. block (type object, required)  
```
{  
    hash:string,  
    header:string,  
    txs:string[]  
}  
```
  

---------- 


## createNewTransation
	createNewTransation [ data: object ] [ replaceLS: boolean = false, [ rawFlag: boolean = false ]]  
          
Arguments:  
1. data (type object, required)   
Transation data. 
``` 
Format:  
{   
    vin: {   
        txid: string,   
        voutn: number   
    }[][],   
    vout: {   
        address: string,   
        value: string   
    }[],   
    changeAddress: string,   
    opReturn?: string   
}  
```
  
2. replaceLS (type boolean, optional, default = false)  
Automatic replacement of unlock for transaction vin.  
  
3. rawFlag (type boolean, optional, default = false)  
Whether the transaction is expressed in raw.  
  

---------- 


## txValidator
	txValidator [ tx: object ]  
transaction validator.  
  
Arguments:  
1. tx (type object, required)   
```
tx object format:  
{  
    hash?: string;  
    version: number;  
    vin: vinJsonData[];  
    vout: voutJsonData[];  
    pqcert: PQCertJsonData[];  
    opReturn: string  
    nLockTime: number;  
}  
```
  
  

---------- 


## addTx
	addTx [ tx: object ]  
add transaction.  
  
Arguments:  
1. tx (type object, required)   
```
tx object format:  
{  
    hash?: string;  
    version: number;  
    vin: vinJsonData[];  
    vout: voutJsonData[];  
    pqcert: PQCertJsonData[];  
    opReturn: string  
    nLockTime: number;  
}  
```

---------- 


## mine
	mine [ address: string | false ]  
start mining or stop mining.  
  
Arguments:  
1. address (type string, required)   
Mining Address. If give 'false' then trun off the miner.  
  

---------- 


## getDifficulty
	getDifficulty [ raw: boolen ]  
Get PoW difficulty  
  

---------- 


## walletReindex
	walletReindex [ startHeight: number ]  
          
Arguments:  
1. startHeight (type number, required)   
Re-index the starting height of the wallet. If -1 is entered, re-indexing is stopped.  
  

---------- 


## walletClearHistory
	walletClearHistory  
Clear wallet history  
  

---------- 


## walletAddWatchAddress
	walletAddWatchAddress [ address: string ]  
Need to monitor the address of the wallet.  
  
Arguments:  
1. address (type string, required)   
Monitor the address.  
  

---------- 


## walletAutoWatch
	walletAutoWatch  
Monitor all addresses of the wallet.  


---------- 


## walletGetTxList
	walletGetTxList [ address: string | string[] ] [ limit: number ] [ skip: number ]  
Get transactions for single or multiple addresses.  
  
Arguments:  
1. address (type string or string[], required)   
2. limit (type number, default = 20)  
3. skip (type number, default = 0)  
  

---------- 


## walletGetUTXOList
	walletGetUTXOList [ address: string | string[] ] [ limit: number ] [ skip: number ] 
Get unused transactions for single or multiple addresses.  
  
Arguments:  
1. address (type string or string[], required)   
2. limit (type number, default = 20)  
3. skip (type number, default = 0) 
  

<br/>

***Peer2Peer***
========
## p2pAddPeer
	p2pAddPeer [ ip: string ] [ port?: number ] 
Add a new connectable node.  
Try to connect to the new node before joining and add to the connection table if you can connect.  
  
Arguments:  
1. peer (type string, required)    
Input ip. 

2. ip (type number, optional)    
Input port.
  

---------- 


## p2pDeletePeer
	p2pDeletePeer [ ip: string ] [ port?: number ]
Delete connectable nodes. Delete the specified node in the connection table.  
  
Arguments:  
1. ip (type string, required)    
Input ip.

2. ip (type number, optional)    
Input port.
  

---------- 


## p2pAddBlackPeer
	p2pAddBlackPeer [ ip: string ]  
Add a new list of blacklistable connections. Disable specified ip connection.  
  
1. ip (type string, required)    
ip address.  
  

---------- 


## p2pDeleteBlackPeer
	p2pDeleteBlackPeer [ ip: string ]  
Delete connectable blacklist.  
  
1. ip (type string, required)    
ip address.  
  

---------- 


## p2pStatus
	p2pStatus  
List the status of nodes that are currently connected.  
  

---------- 


## p2pGetPeerList
	p2pGetPeerList  
List connectable nodes.  
  

---------- 


## p2pGetBlackList
	p2pGetBlackList  
List all banned ip address.  
  

---------- 


