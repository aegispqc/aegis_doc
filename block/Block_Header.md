# Block Header
A block header is used to identify a particular block on an entire blockchain and is hashed repeatedly to create proof of work for mining rewards. A blockchain consists of a series of various blocks that are used to store information related to transactions that occur on a blockchain network. Each of the blocks contains a unique header, and each such block is identified by its block header hash individually. 

| Name | Bytes |  Type  | Description |
|-------|:-------:|-------:|-------|
| versoin | 4 | uint32 | Block version |
| preHash | 32 | Buffer[32] | Hash value of the previous block. |
| merkleroot | 32 | Buffer[32] | The merkle root of all transactions in the block. |
| time | 4 | uint32 | The time to start the proof of work calculation, which should be strictly greater than the time of the previous block. |
| nBit | 2 | uint16 | Difficulty of Proof of Work. (Please refer to "[PoW.md](./PoW.md)" for proof of work)|
| nonce | 32 | Buffer[32] | Input for Proof of Work. (Please refer to "[PoW.md](./PoW.md)" for proof of work)|





