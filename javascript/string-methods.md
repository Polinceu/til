# JS：字符串常用方法

```js
const s = "  hello world  ";
s.trim();            // "hello world"
s.includes("world"); // true
s.startsWith("he");  // false（开头有空格）
s.split(" ");        // ["", "", "hello", "world", "", ""]
"a-b-c".split("-");  // ["a", "b", "c"]
"abc".toUpperCase(); // "ABC"
```

- 字符串是不可变的，这些方法都返回新字符串，原字符串不动。
- `includes` 判断包含，`startsWith/endsWith` 判断开头结尾。
- `split` 切分，`join` 是反过来的操作（数组变字符串）。
