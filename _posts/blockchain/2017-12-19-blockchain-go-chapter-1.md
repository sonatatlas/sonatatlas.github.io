---
layout: post
categories: blockchain
title: Basic Prototype
---

_accroding to [Ivan Kuznetsov`s blog][1]_
<br/><br/>

# intro

>
so, what is blockchain? blockchain is just a distributed database of redcords. But what makes it unique is not a private database, but a public one.
i.e. everyone who uses it has a full or partial copy of it. And a new record can be added only with a consent of other keepers of the database.

# Block

```go

type Block struct {
     Timestamp	  int64
     Data	  []btye
     PrevBlockHash	[]byte
     Hash		[]byte
}

```

__field:__

```go
func (b *Block) SetHash() {
     time := []byte(strconv.FormatInt(b.Timestamp, 10))
     headers := bytes.Join([][]byte{b.PrevBlockHash, b.Data, timestamp}, []byte{})
     hash := sha256.Sum256(headers)

     b.Hash = hash[:]
}
```

__newBlock:__

```go

func NewBlock(data string, prevBlockHash []byte) *Block {
     block := &Block{
     	   time.Now().Unix(),
	   []byte(data),
	   prevBlockHash,
	   []byte{}
     }
     block.SetHash()
     return block
}

```

# BlockChain

__now we need: [Block, Block, Block, ...]__


```go
type Blockchain struct{
     blocks []*Block
}

```

__AddBlock__


```go

func (bc *Blockchain) AddBlock(data string){
     prevBlock := bc.blocks[len(bc.blocks)-1]
     newBlock := NewBlock(data, prevBlock.Hash)
     bc.blocks = append(bc.blocks, newBlock)
}

```

__genesis block__


```go

func NewGenesisBlock() *Block {
     return NewBlock("Genesis Block", []byte)
}

func NewBlockchain() *Blockchain {
     return &Blockchain{
     	    []*Block{NewGenesisBlock()}
}
}

```

[1]:https://jeiwan.cc

