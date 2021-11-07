### 迭代器

```javascript
Object.prototype[Symbol.iterator] = function () {
  let index = 0;
  let keys = Object.keys(this);
  return {
    next: () => {
      let value = this[keys[index++]];
      let done = index > keys.length;
      return { value, done };
    },
  };
};
```

### 克隆

```javascript
function type(data) {
  return Object.prototype.toString.call(data).slice(8, -1);
}
function deepClone(data) {
  let res;
  let mType = type(data);
  if (mType === "Object") {
    res = {};
  } else if (mType === "Array") {
    res = [];
  } else {
    return data;
  }

  for (const key in data) {
    if (Object.hasOwnProperty.call(data, key)) {
      res[key] = deepClone(data[key]);
    }
  }

  return res;
}
```
