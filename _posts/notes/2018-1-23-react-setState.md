---
layout: post
categories: react
title: setting reactState value with dynamic key
---

# output like title

_


#### state
```js
state={
	wrapkey: 'secret'
}

```

#### func

```js
let changeState = porps =>{
    this.setState({
	[props.key] : props.value
    })
}

```

_