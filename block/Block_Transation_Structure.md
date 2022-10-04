# Block Transation Structure

## compactSize type
```
>= 0 && <= 252:  uint8_t
>= 253 && <= 0xffff: 0xfd + uint16_t
>= 0x10000 && <= 0xffffffff: 0xfe + uint32_t
>= 0x100000000 && <= 0xffffffffffffffff: 0xff **Disabled**
```
ex: 515 => 0xfd0302

## tx raw
```
tx_in_count: <compactSize>
tx_in: 
tx_out_count: <compactSize>
tx_out: 
tx_pqcert_count: <compactSize>
tx_pqcert: Refer to "PQCert.md"
opreturn:
lock_time: 4 bytes 
```
photon size: normal data(X1), unlockscript(X3), pqcert(X2), opreturn(X5)
[tx_pqcert is Here](PQCert.md)

## tx_in  (Non-Coinbase)
```
previous_output_count: <compactSize>
previous_output: 36 bytes * previous_output_count ( hash: 32 bytes; tx_out n: 4 bytes )
unlock_script_bytes: <compactSize>
unlock_script: unlock_script_bytes bytes
sequence: 4 bytes (Default: 0xffffffff)
```
## tx_in  (Coinbase) previous_output_count = 0x00
```
previous_output_count: 1 byte = 0x00
previous_output: 0 byte
unlock_script_bytes: 1 byte  = 0x04
unlock_script: 4 bytes = this block height (uint32)
sequence: 4 bytes (Default: 0xffffffff)
```

## tx_out
```
value: 8 bytes (uint64) **This value can not be zero, which is very important to avoid meaningless transactions.**
lock_script_bytes: <compactSize>
lock_script: lock_script_bytes
```

## opreturn
```
opreturn_bytes: <compactSize>
data: opreturn_bytes bytes
```

