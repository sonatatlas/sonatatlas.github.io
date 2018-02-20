---
layout: post
title: My Crypto-currency
categories: blockchian
---

based on [eth constract][eth]  

# basic token 
```solidity
contract MyToken {
	/* create an array with all balances */
	// 遍历获得所有地址的余额到 public 变量 balanceOf
	mapping (address => uint256) public balanceOf;
	
	/* Initializes contract with initial supply tokens to the creator of the contract */
	// 初始化一个带有一定量 token 的合约 MyToken
	func MyToken( uint256 initialSupply ){
		balanceOf[msg.sender] = initialSuply;
		// Give the creator all initial tokens
		// 给合约指定初始 tokens
	}
	
	/* Send coins */
	// 转账
	function transfer(address _to, uint256 _value){
		require(balanceOf[msg.sender] >= _value)
		// Check if the sender has enough
		// 发送 tokens 的地址是否有足够余额
		
		require(balanceOf[_to] + _value >= balanceOf[_to]);
		// Check for overflows
		// 接收 tokens 的地址是否会溢出 tokens, 丢失 tokens
		
		balanceOf[msg.sender] -= _value
		// Add the same to the recipient
		// 更新交易双方的 token 量
		balanceOf[_to] += _value
	}
}

```

# one more complete code
```solidity
pragma solidity ^0.4.16
interface tokenRecipient{
	function receiveApproval(address _form, uint256 _value, address _token, bytes _extraData) public;
}

contract TokenERC20 {
	// Public variables of the token
	string public name;
	string public symbol
	uint8 public decimals = 18;
}
```

[eth]:https://ethereum.org/token
