## Tham chiếu

Ngoài các hằng, bất kỳ đối tượng nào trong JavaScript (bao gồm cả hàm, mảng, regexp, v.v.) đều là tham chiếu. Điều này có nghĩa là:

### Các phép biến đổi ảnh hưởng đến tất cả các tham chiếu

```js
var foo = {};
var bar = foo; // bar là tham chiếu đến cùng một đối tượng

foo.baz = 123;
console.log(bar.baz); // 123
```

### Sự bằng nhau là cho các tham chiếu

```js
var foo = {};
var bar = foo; // bar là một tham chiếu
var baz = {}; // baz là một *đối tượng mới* khác với `foo`

console.log(foo === bar); // true
console.log(foo === baz); // false
```
