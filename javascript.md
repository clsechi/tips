# JavaScript tips

## Dictionary

```js
const defineHandler = (type, param) => {
    const dictionary = {
      option1: doSomething,
      option2: doOtherThing,
      generic: () => null,
    };

    const handler = dictionary[type];

    return handler ? handler : dictionary.generic
}

defineHandler(type)(param)
```
