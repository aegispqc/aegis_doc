# Digital Signature
AEGIS uses a variety of different digital signature algorithms, including those based on modern cryptography and post-quantum cryptographym and use it in a so-called hybrid mode in combination with an established "pre-quantum" signature scheme.

**Example: Secp256k1 + Dilithium3, Secp256k1 + Falcon512, Secp256k1 + Dilithium5 + Falcon1024 etc.**

The current digital signature algorithms used by AEGIS are as follows:
| id | name | quantum-resistant |
| - | - | - |
| 0 | Secp256k1 | false |
| 1 | Dilithium3 [(Nist PQC Round 3 Submissions)](https://csrc.nist.gov/Projects/post-quantum-cryptography/round-3-submissions) | true |
| 2 | Dilithium5 [(Nist PQC Round 3 Submissions)](https://csrc.nist.gov/Projects/post-quantum-cryptography/round-3-submissions) | true |
| 3 | Falcon512 [(Nist PQC Round 3 Submissions)](https://csrc.nist.gov/Projects/post-quantum-cryptography/round-3-submissions) | true |
| 4 | Falcon1024 [(Nist PQC Round 3 Submissions)](https://csrc.nist.gov/Projects/post-quantum-cryptography/round-3-submissions) | true |

## List of algorithms and parameters
### I. secp256k1 (Not quantum resistant)
Parameters:
```
key seed: <32 bytes>
sk: <32 bytes>
pk: <33 bytes>
sign: <64 bytes>
```
Sign Parameters: 
```
input: 
  message:
    data:  <32 bytes> shake256(message)
    nonce: <32 bytes>
    sk: <32 bytes>Buffer
output:
  sign: <64 bytes>Buffer

verify:
  public key: <33 bytes>Buffer
  sign: <64 bytes>Buffer
```
### II. CRYSTALS-DILITHIUM (quantum-resistant) [Nist PQC Round 3 Submissions]
1. Dilithium3:
```
key seed: <32 bytes>
Parameters:
  sk: <4016 bytes>
  pk: <1952 bytes>
  sign: <3293 bytes>
```
2. Dilithium5:
```
key seed: <32 bytes>
Parameters:
  sk: <4880 bytes>
  pk: <2592 bytes>
  sign: <4595 bytes>
```

### III. Falcon (quantum-resistant) [Nist PQC Round 3 Submissions]
1. Falcon-512:
```
key seed: <48 bytes>
Parameters:
  sk: <1281 bytes>
  pk: <897 bytes>
  sign: <692 bytes>
```
2. Falcon-1024:
```
key seed: <48 bytes>
Parameters:
  sk: <2305 bytes>
  pk: <1793 bytes>
  sign: <1332 bytes>
```

For more information on digital signature structures in "[Signature_System.md](./Signature_System.md)".

## Question
### Q1: Why use secp256k1, which is not quantum-resistant?
A1: It takes a long time to prove the security of a new cryptosystem; therefore, cryptographers usually do not recommend adopting it directly, preferring to mix it with previous but stable algorithms. (After the third round of NIST submission, some digital signature algorithms have been identified as requiring adjustment to their parameter settings).



