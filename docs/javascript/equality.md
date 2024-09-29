## So Sánh Bằng

Một điều cần lưu ý trong JavaScript là sự khác biệt giữa `==` và `===`. Vì JavaScript cố gắng "kiên nhẫn" với các lỗi lập trình, nên `==` sẽ cố gắng thực hiện _ép kiểu_ giữa hai biến, ví dụ như chuyển một chuỗi sang số để có thể so sánh với số như minh họa dưới đây:

```js
console.log(5 == "5"); // true   , TS Error
console.log(5 === "5"); // false , TS Error
```

Tuy nhiên, những lựa chọn mà JavaScript đưa ra không phải lúc nào cũng lý tưởng. Ví dụ, trong ví dụ dưới đây, câu lệnh đầu tiên là `false` vì `""` và `"0"` đều là chuỗi và rõ ràng là không bằng nhau. Tuy nhiên, trong trường hợp thứ hai, cả `0` và chuỗi rỗng (`""`) đều là giá trị giả (falsy) (tức là hành xử như `false`) và do đó bằng nhau khi so với `==`. Cả hai câu lệnh đều sai khi bạn sử dụng `===`.

```js
console.log("" == "0"); // false
console.log(0 == ""); // true

console.log("" === "0"); // false
console.log(0 === ""); // false
```

> Lưu ý rằng `string == number` và `string === number` đều là lỗi biên dịch trong TypeScript, vì vậy bạn thường không cần phải lo lắng về điều này.

Tương tự như `==` so với `===`, còn có `!=` so với `!==`.

Vì vậy, mẹo chuyên nghiệp: Luôn sử dụng `===` và `!==`, trừ khi kiểm tra null, mà chúng ta sẽ đề cập sau.

## So Sánh Bằng Cấu Trúc

Nếu bạn muốn so sánh hai đối tượng để kiểm tra tính bằng cấu trúc, `==`/`===` là **_không_** đủ. Ví dụ:

```js
console.log({ a: 123 } == { a: 123 }); // False
console.log({ a: 123 } === { a: 123 }); // False
```

Để thực hiện các kiểm tra như vậy, hãy sử dụng gói npm [deep-equal](https://www.npmjs.com/package/deep-equal), ví dụ:

```js
import * as deepEqual from "deep-equal";

console.log(deepEqual({ a: 123 }, { a: 123 })); // True
```

Tuy nhiên, thường thì bạn không cần kiểm tra sâu và tất cả những gì bạn thực sự cần là kiểm tra theo một số `id`, ví dụ:

```ts
type IdDisplay = {
  id: string;
  display: string;
};
const list: IdDisplay[] = [
  {
    id: "foo",
    display: "Foo Select",
  },
  {
    id: "bar",
    display: "Bar Select",
  },
];

const fooIndex = list.map((i) => i.id).indexOf("foo");
console.log(fooIndex); // 0
```
