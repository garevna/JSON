# JSON
###### Interesting tasks for my trainees

<sup>Special for those who are intrigued by the task of passing object methods in a json string 😂✊</sup><br>
<sup>Improve this solution on your own, or at least think about where improvement is needed 😉</sup>

### Methods

Let's add a couple of methods to JSON collection:

:one:
```js
JSON.stringifyUser = function (user, methodName) {
  user.methodName = methodName
  user.getMethod = `
  (function () {
    return ${user[methodName].toString()}
  })()
  `

  return JSON.stringify(user)
}
```

:two:
```js
JSON.parseUser = function (json) {
  const user = JSON.parse(json)
  
  user[user.methodName] = eval(user.getMethod)

  delete user.methodName
  delete user.getMethod

  return user
}
```

### Source object

Now let's create a user object:

```js
const user = {
  name: 'Piter',
  getName: function () { console.log(this.name) }
}
```

### Stringify
Now let's stringify this object with the new stringifyUser method, which has been added to JSON collection:

```js
const json = JSON.stringifyUser(user, 'getName')
```

### Parse

Let's parse the resulting json string with the new parseUser method, which we have added to JSON collection:

```js
JSON.parseUser(json)
```
