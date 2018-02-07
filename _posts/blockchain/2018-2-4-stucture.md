---
layout: post
categories: blockchain
title: Structure of Blockchain
---

<br/>
<ol>
<li><a href="#block">Block</a></li>
<li><a href="#blockchain">BlockChain</a></li>
</ol>
<br/>

## Block 
<br name="Block"/>
# List
+ package:
  + bytes
  + encoding/gob
  + log
  + time  
+ struct:
  + Block  
+ func:
  + NewBlock
  + NewGenesisBlock
  + HashTransactions
  + Serialize
  + DeserializeBlock  
<br/>

# Struct
```go
type Block struct {
	Timestamp      int64
	Transactions   []*Transaction
	PrevBlockHash  []byte
	Hash           []byte
	Nonce          int
	Height         int
}
```
<br/>
# Func

```go
// NewBlock creates and returns Block
func NewBlock (  transactions []*Transaction, prevBlockHash []byte, height int ) *Block {}

// NewGenesisBlock creates and returns genesis Block
func NewGenesisBlock(coinbase *Transaction) *Block {}

// HashTransactions returns a hash of the transactions in t
func (b *Block) HashTransactions() []byte {}

// Serialize serialize the block
func (b *Block) Serialize() []byte {}

// DeserializeBlock deserializes a block
func DeserializeBlock(d []byte) *Block {}

```
<br/>

## BlockChain
<br name="BlockChain"/>
# List

+ package
  + bytes
  + crypto/ecdsa
  + encoding/hex
  + errors
  + fmt
  + log
  + os
  + github.com/boltdb/bolt
+ struct
  + Blockchain
+ func
  + CreateBlockchain
  + NewBlockchain
  + AddBlock
  + FindTransaction
  + FindUTXO
  + Iterator
  + GetBestHeight
  + GetBlock
  + GetBlockHashes
  + MineBlock
  + SignTransaction
  + VerifyTransaction
  + dbExists
  
# Struct

```go
type Blockchain struct {
	tip []byte
	db  *bolt.DB
}

```
# Func

```go

func CreateBlockchain( address, nodeID string ) *Blockchain{}
func NewBlockchain( nodeID string) *Blockchain {}
func (bc *Blockchain) AddBlock(block *Block) {}
func (bc *Blockchain) FindTransaction(ID []byte) (Transaction, error){}
func (bc *Blockchain) FindUTXO() map[string]TXOutputs {}
func (bc *Blockchain) Iterator() *BlockchainIterator {}
func (bc *Blockchain) CetBestHeight() int {}
func (bc *Blockchain) GetBlock( blockHash []byte )(Block, error){}
func (bc *Blockchain) GetBlockHashes() [][]byte{}
func (bc *Blockchain) MineBlock(transactions []*Transaction) *Block{}
func (bc *Blockchain) SignTransaction(tx *Transaction, privKey ecdsa.PrivateKey) {}
func (bc *Blockchain) VerifyTransaction(tx *Transaction) bool {}
func dbExists(dbFile string) bool {}

```


## BlockchainIterator 

# List

+ package
  + log
  + github.com/boltdb/bolt
+ struct
  + BlockchainIterator
+ func
  + Next
  
# Struct

```go
type BlockchainIterator struct {
	currentHash  []byte
	db           *bolt.DB
}

```

# Func

```go
func (i *BlockchainIterator) Next() *Block {}

```

## PoofOfWork 

# List

+ package
  + bytes
  + crypto/sha256
  + fmt
  + mach
  + math/big
+ type
  + proofofwork
+ func
  + NewProofOfWork
  + prepareData
  + run
  + validate
  
# Struct

```go
type ProofOfWork struct {
	block  *Block
	target *big.Int
}

```

# Func

```go
func NewProofOfWork(b *Block) *ProofOfWork {}
func (pow *ProofOfWork) perpare(nonce int) []byte {}
func (pow *ProofOfWork) Run() (int, []byte) {}
func (pow *ProofOfWork) Validate() bool {}

```

## Transaction

# List

+ package
  + bytes
  + crypto/ecdsa
  + crypto/elliptic
  + crypto/rand
  + crypto/sha256
  + math/big
  + strings
  + encoding/gob
  + encoding/hex
  + fmt
  + log
+ struct
  + Transaction
+ func
  + IsCoinbase
  + Serialize
  + Hash
  + Sign
  + String
  + TrimmedCopy
  + Verify
  + NewCoinbaseTx
  + NewUTXOTransaction
  + DeserializeTransaction
  
# Struct

```go
type Transaction struct {
	ID    []byte
	Vin   []TXInput
	Vout  []TXOutput
}

```

# Func

```go
func (tx Transaction) IsCoinbase() bool {}
func (tx Transaction) Serialize() bool {}
func (tx Transaction) Hash() []byte {}
func (tx *Transaction) Sign( privKey ecdsa.PrivateKey, prevTXs map[string]Transaction) {}
func (tx Transaction) String() string {}
func (tx *Transaction) TrimmedCopy() Transaction {}
func (tx *Transaction) Verify(prevTxs map[string]Transaction) bool {}
func NewCoinbaseTX(to, data string) *Transaction {}
func NewUTXOTransaction(wallet *Wallet, to string, amount int, UTXOSet *UTXOSet) *Transaction {}
func DeserializeTransaction(data []byte) Transaction {}

```

## TXInput

# List

+ package
  + bytes
+ struct
  + TXInput
+ func
  + UsesKey
  
# Struct

```go
type TXInpute struct {
	Txid       []byte
	Vout       int
	Singature  []byte
	Pubkey     []byte
}

```

# Func

```go
func (in *TXInput) UsesKey(pubKeyHash []byte) bool {}
```

## TXOutput

# List

+ package
  + bytes
  + encoding/gob
  + log
+ struct
  + TXOutput
  + TXOutputs
+ func
  + Lock
  + IsLockedWithKey
  + NewTXOutput
  + Serialize
  + DeserializeOutput
  

# Struct

```go
type TXOutput struct {
	Value       int
	PubKeyHash  []byte
}

type TXOutputs struct {
	Outputs []TXOutput
}
```

# Func

```go
func (out *TXOutput) Lock(address []byte) {}
func (out *TXOutput) IsLockedWithKey(pubKeyHash []byte) bool {}
func NewTXOutput(value int, address string) *TXOutput {}
func (outs TXOutputs) Serialize() []byte {}
func DeserializeOutput(data []byte) TXOutputs {}

```

## UTXO_set

# List

+ package
  + encoding/hex
  + log
  + github.com/boltdb/bolt
+ struct
  + FindSpendobleOutputs
+ func
  + FindSpendableOutputs
  + FindUTXO
  + CountTransactions
  + Reindex
  + Update

## MerkleTree

# List

+ package
  + crypto/sha256
+ struct
  + MerkleTree
  + MerkleNode
+ Func
  + NewMerkleTree
  + NewMerkleNode

# Func

```go
func NewMerkleTree(data [][]byte) *Merkle
func NewMerkleNode(left, right *MerkleNode, data []byte) *MerkleNode {}

```

## CLI

# List
+ package
  + flag
  + fmt
  + log
  + os
+ struct
  + CLI
+ func
  + printUsage
  + validateArgs
  + Run
  + createBlockChain
  + createWallet
  + getBalance
  + listAddress

# Struct

```go
type CLI struct{}

```

# Func

```go
func (cli *CLI) printUsage() {}
func (cli *CLI) validateArgs() {}
func (cli *CLI) Run() {}
func (cli *CLI) createBlockchain(address, nodeID string) {}
func (cli *CLI) createWallet(nodeID string) {}
func (cli *CLI) getBalance(address, nodeID string) {}
func (cli *CLI) listAddress(nodeID string) {}
func (cli *CLI) printChain(nodeID string) {}
func (cli *CLI) reindexUTXO(nodeID string) {}
func (cli *CLI) send(from, to string, amount int, nodeID string, mineNow bool) {}
func (cli *CLI) startNode(nodeID, minerAddress string) {}

```

## Wallet

# List

+ package
  + bytes
  + crypto/ecdsa
  + crypto/elliptic
  + crypto/rand
  + crypto/sha256
  + log
  + golang.org/x/crypto/ripemd160
+ struct
  + Wallet
+ func
  + GetAddress
  + HashPubKey
  + ValidateAddress
  + checkSum
  + newKeyPair

# Struct

```go
type Wallet struct{
	PrivateKey  ecdsa.PrivateKey
	PublicKey   []byte
}

```

# Func

```go
func NewWallet() *Wallet {}
func (w Wallet) GetAddress() []byte {}
func (pubKey []byte) []byte {}
func ValidateAddress(address string) bool {}
func checksum(payload []byte) []byte {}
func newKeyPair() (ecdsa.PrivateKey, []byte) {}

```

## Wallets

# List
+ package
  + bytes
  + crypto/elliptic
  + encoding/gob
  + fmt
  + io/ioutil
  + log
  + os
+ struct
  + Wallets
+ func
  + NewWallets
  + CreateWallet
  + GetAddresses
  + SaveToFile
  
# Struct

```go
type Wallets struct{
	Wallets map[string]*Wallet
}

```

# Func

```go
func NewWallets(nodeID string) (*Wallets, error) {}
func (ws *Wallets) CreateWallet() string {}
func (ws *Wallets) GetAddresses() []string {}
func (ws *Wallets) GetWallet(address string) Wallet {}
func (ws *Wallets) LoadFromFile(nodeID string) error {}
func (ws Wallets) SaveToFile(nodeID string)
```

## Server

# List
+ package
  + bytes
  + encoding/gob
  + encoding/hex
  + fmt
  + io
  + io/ioutil
  + log
  + net
+ struct
  + addr
  + block
  + getBlock
  + getdata
  + inv
  + tx
  + verzion
+ func
  + commandToBytes
  + bytesToCommand
  + extractCommand
  + requestBlocks
  + sendAddr
  + sendBlock
  + sendData
  + sendInv
  + sendGetBlocks
  + sendGetData
  + sendTx
  + sendVersion
  + handleAddr
  + handleBlock
  + handleInv
  + handleGetBlocks
  + handleGetData
  + handleTx
  + handleVersion
  + handleConnection
  + StartServer
  + gobEncode
  + nodeIsKnown
