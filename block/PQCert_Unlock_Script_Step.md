# How does the PQCert Unlock Script work?
The PQCert unlocking script is based on the same concept as Bitcoin, which is a stack being processed from left to right.

## Summary of Operation Codes
| Opcode | Word |  input  | output | Description |
|-------|-------|-------|-------|-------|
| 1-75 | OP_PUSH(1~75) | (special) | data | The next opcode byte is data to be pushed onto the stack. |
| 76 | OP_PUSHDATA1 | (special) | data | The next 1 byte (uint8) contains the number of bytes to be pushed onto the stack. **(256 > number > 75)** |
| 77 | OP_PUSHDATA2 | (special) | data | The next 2 bytes (uint16 little endian order) contains the number of bytes to be pushed onto the stack. **(65536 > number > 255)** |
| 78 | OP_PUSHDATA4 | (special) | data | The next 4 bytes (uint32 little endian order) contains the number of bytes to be pushed onto the stack. **(2^32 > number > 65535)** |
| 252 | OP_CHECKPQCERT | PQCert_hash SIGHASH sign_0 sign_1 ... | True / False | Please see "[OP_CHECKPQCERT](#OP_CHECKPQCERT)" |


## OP_CHECKPQCERT
OP_CHECKPQCERT is a complex opcode that represents a series of PQCert verification steps.
Run different validation steps depending on the certificate type.
1. PQCert.type = 0: Run single identity verification. 
2. PQCert.type = 1: Wrong authentication, only public key cannot verify identity. return: false
3. PQCert.type = 2: Run group verification. (multiple identity verification)

## Signature format
```<sign_number> <sign_data>```

## PQCert.type = 0, script example: 
```
lock script: <PQCert_hash> <OP_CHECKPQCERT>
unlock script: <sign_0> <sign_1> ... <sign_n> <SIGHASH>
```
**The signature number of the unlock script must be incremental, during the execution of the unlock script.**

When executing the unlock script:
```
<unlock script> <lock script> 
-> <sign_0> <sign_1> ... <sign_n> <SIGHASH> <PQCert_HASH> <OP_CHECKPQCERT>
```

Step 1. Push in data until **OP_CHECKPQCERT** instruction is encountered, The stack is shown below:
```
| <PQCert_hash> |
|  <SIGHASH>    |
|   <sign_n>    |
|   .           |
|   .           |
|   .           |
|   <sign_1>    |
|   <sign_0>    |
```
Step 2. Pop up stacked data in order to OP_CHECKPQCERT:

	OP_CHECKPQCERT(PQCert_hash, SIGHASH, sign_n, ... sign_2, sign_1)

- Get PQCert by PQCert_hash
- SIGHASH
- Get the public key corresponding to the signature in turn, and verify the transaction.

## PQCert.type = 2 (Group), script example: 
```
lock script: <PQCert_hash> <OP_CHECKPQCERT>
unlock script: <sign_0_0> <sign_0_1> ... <sign_0_n> <member_0>  <sign_1_0> <sign_1_1> ... <sign1_n> <member_1> ...  <sign_n_n> <SIGHASH>
```

**The signature number of the unlock script must be incremental, during the execution of the unlock script.**

When executing the unlock script:
```
<unlock script> <lock script> 
-> <sign_0_0> <sign0_1> ... <sign0_n> <member_0> ... <signn_n> ... <SIGHASH> <PQCert_HASH> <OP_CHECKPQCERT>
```

Step 1. Push in data until **OP_CHECKPQCERT** instruction is encountered, The stack is shown below:
```
| <PQCert_hash> |
|  <SIGHASH>    |
|  <sign_n_n>   |
|   .           |
|   .           |
|   .           |
|   .           |
|   <sign0_1>   |
|   <sign0_0>   |
```
Step 2. Pop up stacked data in order to OP_CHECKPQCERT:

	OP_CHECKPQCERT(PQCert_hash, SIGHASH, sign_n_n, ... sign_0_2, sign_0_1)

- Get PQCert by PQCert_hash
- SIGHASH
- Get the public key corresponding to the signature in turn, and verify the transaction. (for all menber)

**See "PQCert.md" for the structure of the [tx_pqcert is Here](PQCert.md)**





	


