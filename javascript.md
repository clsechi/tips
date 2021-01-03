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

## Init

Run a script file

```js
(async function init() {
  try {
    console.log('Working');

    // call the initial fuction

    console.log(`Done! :)`);
    process.exit(0);
  } catch (err) {
    console.error('Error on init', err);
    process.exit(1);
  }
}());
```
