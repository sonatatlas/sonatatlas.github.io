---
layout: post
title: Typescript Error
title: javascript
---

### TS4082  

- develop react-native use react-navigation

```ts
export default StackNavigator({
  EntranceScreen: { screen: EntranceScreen }
})

```  
> Default export of the module has or is using private name 'NavigationContainer'.  

after ts-lint:  

> The class method 'render' must be marked either 'private', 'public', or 'protected'  

solution:  

```

```

