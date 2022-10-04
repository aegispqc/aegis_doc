Wallet Definition
=======

The wallet file is stored in Object format (most of the data belongs to BUFFER) for easy reading.

A complete wallet should have keypairs + addresses

Object format:
```
{
    keypairs: {
   
        // signType = Signature Type enum. Ex: falcon-512 = 0, xxx = 1 ... falcon-1024 = ??
        [ PqcertPubkey hash ]: { version, signType, privateKey, publicKey },
        ... 
    },
    
    addresses: {
    
        [address]: { 
        
            version,
            level,
            keyes: [
            
               { fake: false, value: hash }, 
               // value is equal to the keypairs corresponding to the secret pair, which can generate PQCertPubKey.
               { fake: true, value: hash },  
               // value is equal to the fake PQCERTPUBK HASH used to join the non-existent Pubhash in PQCertRoot.
               ...
            ],
        },
        ...
    }
}
```


Save the wallet file with lmDB.
-------

Data format: 
```
{
    [seed] : 32 byte,
    keypair : [0, 1, ...], //Signature Type enum.
    address : [
        { 
            version,
            level,
            pubkeyes: [
   	         
                { fake: false, kn: number } //kn = keypair number. UINT8
                { fake: true }, //fake pubkeye
                ...
            ],
        }, 
        ...
    ]
}
```

Secret Key Group Preservation
-------
```
{
    seed: 32 byte,
    sk amount: 4 bytes (uint32),
    skTypes: (4 bytes + 2 byte) * (sk amount), // 4bytes version
    
    addr amount: 4 bytes (uint32),
    addrs: {
    
        version: 4 bytes,
        level: 1 byte (uint32),
        pk amount: 1 byte,
        pkhashs: 
        {
            fakeFlag: 1byte
            value: 32 bytes
        }[]
    }[]
}
```
