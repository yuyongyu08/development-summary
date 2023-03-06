# 数组转树

## 题目

实现一个函数，将input转成output

```javascript
const input = [
  { id: "1", data: "中国", pid: null },
  { id: "2", data: "北京", pid: "1" },
  { id: "3", data: "上海", pid: "1" },
  { id: "4", data: "海淀", pid: "2" },
];

const output = [
  {
    id: "1",
    data: "中国",
    pid: null,
    children: [
      { id: "2", data: "北京", pid: "1", children: [{ id: "4", data: "海淀", pid: "2" }] },
      { id: "3", data: "上海", pid: "1" },
    ],
  },
];
```

## 答案

遍历方式：O(n²)

```javascript
function list2tree1(list) {
  // 深拷贝，防止对输入的数据结构造成影响
  let input = JSON.parse(JSON.stringify(list));
  let result = [];

  input.forEach((item) => {
    if (item.pid) {
      let parent = input.find((node) => node.id === item.pid);
      parent.children = parent.children ? [...parent.children, item] : [item];
    } else {
      result.push(item);
    }
  });

  return result;
}
```

遍历优化：O(2n)，提前将数组放到Map中

```javascript
function list2tree2(list) {
  // 深拷贝，防止对输入的数据结构造成影响
  let input = JSON.parse(JSON.stringify(list));
  let result = [];
  let map = new Map();
  input.forEach((item) => {
    map.set(item.id, item);
  });

  input.forEach((item) => {
    if (item.pid) {
      let parent = map.get(item.pid);
      parent.children = parent.children ? [...parent.children, item] : [item];
    } else {
      result.push(item);
    }
  });

  return result;
}
```



遍历再优化：O(n)，在遍历过程中放到map中<mark style="color:red;">【推荐】</mark>

```javascript
function list2tree3(list) {
  // 深拷贝，防止对输入的数据结构造成影响
  let input = JSON.parse(JSON.stringify(list));
  let map = new Map();
  let result = [];

  for (const item of input) {
    const id = item.id;
    const pid = item.pid;

    let mapItem = map.get(id);
    mapItem = { ...item, children: mapItem?.children || [] };
    map.set(id, mapItem);

    if (pid) {
      let parent = map.get(pid);
      if (parent) {
        parent.children.push(mapItem);
      } else {
        map.set(pid, { children: [mapItem] });
      }
    } else {
      result.push(mapItem);
    }
  }

  return result;
}
```



递归方式：

```javascript
function list2tree4(list, pid = null) {
  return list.filter((item) => item.pid === pid).map((item) => ({ ...item, children: list2tree4(list, item.id) }));
}
```

