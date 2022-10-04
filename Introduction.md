# AEGIS
AEGIS is a brand-new, experimental quantum-resistant cryptocurrency that conceptualizes the decentralization of the Bitcoin white paper, integrates a variety of digital signature algorithms based on modern cryptography and post-quantum cryptography, and improves the efficiency of various algorithmic applications.

## Features of AEGIS
| Name  | AEGIS PQC |
| - | - |
| Code  | AGS |
| Mining algorithm  | [AEGISPoW (PoW)](./block/PoW.md) |
| Type | Public blockchain |
| Core security  | [Multiple-PQC](./block/Digital_Signature.md) scheme, including but not limited to the various post-quantum digital signatures selected by NIST 2022. |
| Total number of issued AEGIS | 210,000,000 |
| Block Reward | The last coin is predicted to be mined in 2100. |
| Code base | Code base All the codes and documents are open source. |

## AEGIS currently use digital signatures, Bitcoin only uses Secp256k1.
AEGIS uses a variety of different digital signature algorithms, including those based on modern cryptography and post-quantum cryptographym and use it in a so-called hybrid mode in combination with an established "pre-quantum" signature scheme.

**Example: Secp256k1 + Dilithium3, Secp256k1 + Falcon512, Secp256k1 + Dilithium5 + Falcon1024 etc.**

| id | name | quantum-resistant |
| - | - | - |
| 0 | Secp256k1 | false |
| 1 | Dilithium3 [(Nist PQC Round 3 Submissions)](https://csrc.nist.gov/Projects/post-quantum-cryptography/round-3-submissions) | true |
| 2 | Dilithium5 [(Nist PQC Round 3 Submissions)](https://csrc.nist.gov/Projects/post-quantum-cryptography/round-3-submissions) | true |
| 3 | Falcon512 [(Nist PQC Round 3 Submissions)](https://csrc.nist.gov/Projects/post-quantum-cryptography/round-3-submissions) | true |
| 4 | Falcon1024 [(Nist PQC Round 3 Submissions)](https://csrc.nist.gov/Projects/post-quantum-cryptography/round-3-submissions) | true |

More about digital signatures in "[Digital_Signature.md](./block/Digital_Signature.md)"

## The difference between Bitcoin and AEGIS.
### 1. Hash
AEGIS uses **Shake256** as the HASH function; Bitcoin uses **Double-Sha256**, which includes the block hash, transaction ID, Merkle tree, etc.  A Shake256 hash value could not be inverted bytes, however a **Double-Sha256** value could be.  
AEGIS's hash is displayed without inverted bytes, while BTC has inverted bytes.

### 2. Data Architecture of Blockchain
#### bitcoin

<table>
<tbody>
	<tr>
		<td rowspan=6>Block Header (80 bytes)</td>
		<td>versoin (4 bytes)</td>
		<td></td>
		<td></td>
	</tr>
	<tr>
		<td>preHash (32 bytes)</td>
		<td></td>
		<td></td>
	</tr>
	<tr>
		<td>merkleroot (32 bytes)</td>
		<td></td>
		<td></td>
	</tr>
	<tr>
		<td>time (4 bytes)</td>
		<td></td>
		<td></td>
	</tr>
	<tr>
		<td>nBit (4 bytes)</td>
		<td></td>
		<td></td>
	</tr>
	<tr>
		<td>nonce (4 bytes)</td>
		<td></td>
		<td></td>
	</tr>
	<tr>
		<td rowspan=6>Transaction</td>
		<td rowspan=3>vin[]</td>
		<td rowspan=2>previous_output</td>
		<td>hash (32 bytes)</td>
	</tr>
	<tr>
		<td>vout_n (4 bytes)</td>
	</tr>
	<tr>
		<td>unlock_script</td>
		<td></td>
	</tr>
	<tr>
		<td rowspan=2>vout[]</td>
		<td>value (8 bytes)</td>
		<td></td>
	</tr>
	<tr>
		<td>lock_script</td>
		<td></td>
	</tr>
	<tr>
		<td>n_lcok_time (4 bytes)</td>
		<td></td>
		<td></td>
	</tr>
	</tbody>
</table>
<table>

```
blockheader (80 bytes)
├ versoin (4 bytes)
├ preHash (32 bytes)
├ merkleroot (32 bytes)
├ time (4 bytes)
├ nBit (4 bytes)
└ nonce (4 bytes)

transaction
├ vin[]
| ├ previous_output
| | ├ hash (32 bytes)
| | └ vout_n (4 bytes)
| └ unlock_script
├ vout[]
| ├ value (8 bytes)
| └ lock_script
└ n_lcok_time (4 bytes)
```
AEGIS:
<table>
<tbody>
	<tr>
		<td rowspan=6>Block Header (106 bytes)</td>
		<td>versoin (4 bytes)</td>
		<td></td>
		<td></td>
	</tr>
	<tr>
		<td>preHash (32 bytes)</td>
		<td></td>
		<td></td>
	</tr>
	<tr>
		<td>merkleroot (32 bytes)</td>
		<td></td>
		<td></td>
	</tr>
	<tr>
		<td>time (4 bytes)</td>
		<td></td>
		<td></td>
	</tr>
	<tr>
		<td><b>nBit (2 bytes)</b></td>
		<td></td>
		<td></td>
	</tr>
	<tr>
		<td><b>nonce (32 bytes)</b></td>
		<td></td>
		<td></td>
	</tr>
	<tr>
		<td rowspan=8>Transaction</td>
		<td rowspan=3>vin[]</td>
		<td rowspan=2><b>previous_output []</b></td>
		<td>hash (32 bytes)</td>
	</tr>
	<tr>
		<td>vout_n (4 bytes)</td>
	</tr>
	<tr>
		<td>unlock_script</td>
		<td></td>
	</tr>
	<tr>
		<td rowspan=2>vout[]</td>
		<td>value (8 bytes)</td>
		<td></td>
	</tr>
	<tr>
		<td>lock_script</td>
		<td></td>
	</tr>
	<tr>
		<td><b>pqcert[]</b></td>
		<td><a href='#pqcert-root-table'>pqcert_root</a>, <br><a href='#pqcert-pubkey-table'>pqcert_pubkey</a> <br>or <a href='#pqcert-group-table'>pqcert_group</a></td>
		<td></td>
	</tr>
	<tr>
		<td><b>op_return</b></td>
		<td></td>
		<td></td>
	</tr>
	<tr>
		<td>n_lcok_time (4 bytes)</td>
		<td></td>
		<td></td>
	</tr>
		<tr>
		<td rowspan=4 id='pqcert-root-table'>pqcert_root</td>
		<td>version (4 bytes)</td>
		<td></td>
		<td></td>
	</tr>
	<tr>
		<td>pqcert_type (1 byte)</td>
		<td></td>
		<td></td>
	</tr>
	<tr>
		<td>level (1 byte)</td>
		<td></td>
		<td></td>
	</tr>
	<tr>
		<td>pubkey_hashes[] (n * 32 bytes)</td>
		<td></td>
		<td></td>
	</tr>
		<tr>
		<td rowspan=4 id='pqcert-pubkey-table'>pqcert_pubkey</td>
		<td>version (4 bytes)</td>
		<td></td>
		<td></td>
	</tr>
	<tr>
		<td>pqcert_type (1 byte)</td>
		<td></td>
		<td></td>
	</tr>
	<tr>
		<td>sign_type (2 bytes)</td>
		<td></td>
		<td></td>
	</tr>
	<tr>
		<td>pubkey</td>
		<td></td>
		<td></td>
	</tr>
		<tr>
		<td rowspan=5 id='pqcert-group-table'>pqcert_group</td>
		<td>version (4 bytes)</td>
		<td></td>
		<td></td>
	</tr>
	<tr>
		<td>pqcert_type (1 byte)</td>
		<td></td>
		<td></td>
	</tr>
	<tr>
		<td>level (1 byte)</td>
		<td></td>
		<td></td>
	</tr>
	<tr>
		<td rowspan=5>member_address_lock_time[]</td>
		<td>hash (32 byte)</td>
		<td></td>
	</tr>
	<tr>
		<td>lock_time (4 byte)</td>
		<td></td>
	</tbody>
</table>

```
blockheader (106 bytes)
├ versoin (4 bytes)
├ preHash (32 bytes)
├ merkleroot (32 bytes)
├ time (4 bytes)
├ nBit (2 bytes) **diff.**
└ nonce (32 bytes) **diff.**
transaction
├ vin[]
| ├ previous_outputs[] **diff.**
| | ├ hash (32 bytes)
| | └ vout_n (4 bytes)
| └ unlock_script
├ vout[]
| ├ value (8 bytes)
| └ lock_script
├ pqcert[] **New**
| └ pqcert_root ---- or ---- pqcert_pubkey ---- or ---- pqcert_group
|   ├ version (8 bytes)      ├ version (4 bytes)        ├ version (4 bytes)
|   ├ pqcert_type (1 byte)   ├ pqcert_type (1 byte)     ├ pqcert_type (1 byte) 
|   ├ level (1 byte)         ├ sign_type (2 bytes)      ├ level (1 byte)
|   └ pubkey_hashes[]        └ pubkey                   └ member_address_lock_time[]
|                                                         ├ hash (32 bytes)
|                                                         └ look_time (4 bytes)
├ op_return **New**
└ n_lcok_time
```

### 3. The main differences between BTC and AEGIS block header.
| | BTC | AEGIS |
|-------|:-------:|-------:|
| nBit | 4 bytes | 2 bytes |
| nonce | 4 bytes | 32 bytes |
| total | 80 bytes | 106 bytes |

### 4. P2PQC
Bitcoin has different types of validation scripts (payments), for example: P2PK, P2PKH, P2SH and so on. AEGIS has "P2PQC (Pay to PQCert)", a unique payment. (Refer to [tx_script.md](./block/tx_script.md) and [PQCert.md](./block/PQCert.md))

### 5. Digital Signature
Refer to [Digital_Signature.md](./block/Digital_Signature.md)

### Efficiency of PQC on Blockchain
AEGIS has adopted multiple-PQC digital signature algorithms ([Digital_Signature.md](./block/Digital_Signature.md)) and solved the issues of PQC as follows:
1. Excessive length of the public key.
2. Excessive length of the Signatures.
These issues have a huge performance impact on the Bitcoin framework. The solved approach of AEGIS enhances the efficiency of post-quantum digital signature algorithms on blockchain technology.

### PQCert from AEGIS
1. AEGIS uses the decentralized post-quantum certificate (PQCert) design to get the "Excessive length of the public key" issue solved.
2. AEGIS has modified the previous_output excision of BTC's transaction vin to a special array structure, which can effectively solve the issue of "Excessive length of the Signatures" in most cases.