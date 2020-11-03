# JS tips

## Dictonary

```js
// works

const authorizeUser = (param) => console.log('authorizeUser', param)

const authorizeUserCorrespondent = (param) => console.log('authorizeUserCorrespondent', param)

const handler = (type, param) => {
    const authorizers = {
      user: authorizeUser,
      user_correspondent: authorizeUserCorrespondent,
    };

    const method = authorizers[type];

    return method ? method(param) : 'generic'
}

const param = { name: 'ronaldo' }

const type = 'user'

handler(type, param)
```

```js
// wrong implementation

const authorizeUser = (param) => console.log('authorizeUser', param)

const authorizeUserCorrespondent = (param) => console.log('authorizeUserCorrespondent', param)

const handler = (type, param) => {
    const authorizers = {
      user: authorizeUser(param),
      user_correspondent: authorizeUserCorrespondent(param),
    };

    const method = authorizers[type];

    return method ? method(param) : 'generic'
}

const param = { name: 'ronaldo' }

const type = 'user'

handler(type, param)
```

```js
// works, but use parent params doesn't look like a good pattern, as they can be changed.

const authorizeUser = (param) => console.log('authorizeUser', param)

const authorizeUserCorrespondent = (param) => console.log('authorizeUserCorrespondent', param)

const handler = (type, param) => {
    const authorizers = {
      user: () => authorizeUser(param), // using parent params
      user_correspondent: () => authorizeUserCorrespondent(param), // using parent params
    };
    
    param.name = 'gaucho'

    const method = authorizers[type];

    return method ? method(param) : 'generic'
}

const param = { name: 'ronaldo' }

const type = 'user'

handler(type, param)
```

```js
// works, but all the dictionary fuctions are being called before the method definition

const authorizeUser = (param) => { throw new Error('authorizeUser') } // this will throw an error, even if the type is not "user"

const authorizeUserCorrespondent = (param) => console.log('authorizeUserCorrespondent', param)

const handler = (type, param) => {
    const authorizers = {
      user: authorizeUser(param), // this function is being executed
      user_correspondent: authorizeUserCorrespondent(param), // this function is being executed
    };

    const method = authorizers[type];

    return method ? method(param) : 'generic'
}

const param = { name: 'ronaldo' }

const type = 'generic'

handler(type, param)
```
