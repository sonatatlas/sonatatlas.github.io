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
	string public symbol;
	uint8 public decimals = 18;
	// 18 decimals is the strongly suggested default, avoid changing it
	uint256 public totalSupply;
	
	mapping (address => uint256) public balanceOf;
	// this creates an array with all balances
	mapping (address => mapping (address => uint256)) public allowance;
	// this generates a public event on the blockchain that will notify clients
	
	event Transfer(address indexed from, address indexed to, uint256 value);
	event Burn(address indexed from, uint256 value);
	
	/**
	 * Constructor function 
	 *
	 * Initializes contract with initial supply tokens to the creator of the contract
	 */
	function TokenERC20(
		uint256 initialSupply,
		string tokenName,
		string tokenSymbol
	) public {
		totalSupply = initialSupply * 10 ** uint256(decimals);
		// Update total supply with the decimal amount
		balanceOf[msg.sender] = totalSupply;
		// Give the creator all initial tokens
		name = tokenName;
		// Set the name for display purposes
		symbol = tokenSymbol;
		// Set the symbol for display purposes
	}
	/**
	 * Internal transfer, only can be called by this contract
	 */
	function _transfer(address _form, address _to, uint _value) internal {
		// Prevent transfer to 0x0 address, Use burn() instead
		require(_to != 0x0);
		// Check if the sender has enough
		require(balanceOf[_from] >= _value);
		// Save this for an assertion in the future
		uint previousBalances = balanceOf[_form] + balanceOf[_to];
		// Subtract from the sender
		balanceOf[_from] -= _value;
		// Add the same to the recipient
		balanceOf[_to] += _value;
		// Add the same to the recipient
		balanceOf[_to] += _value;
		Transfer(_from, _to, _value)
	}
}
```

[eth]:https://ethereum.org/token
