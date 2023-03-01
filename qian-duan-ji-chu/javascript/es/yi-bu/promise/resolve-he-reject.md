# resolve和reject

### 1、Promise.resolve(value)

```javascript
Promise.resolve("fulfiled").then((value) => {
  console.log("onResolve: ", value);
});
```

### 2、Promise.reject(reason)

* 有onRejected时，不再执行catch

```javascript
Promise.reject("fulfiled")
  .then(
    (value) => {
      console.log("onResolve: ", value);
    },
    (reason) => {
      console.log("onRejected: ", reason);
    }
  )
  .catch((err) => {
    console.log("catch: ", err);
  });
```

输出：

```
onRejected:  fulfiled
```

* 无onRejected时，执行catch

```
Promise.reject("fulfiled")
  .then((value) => {
    console.log("onResolve: ", value);
  })
  .catch((err) => {
    console.log("catch: ", err);
  });
```

输出：

```
catch:  fulfiled
```
