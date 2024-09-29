# JavaScript của Bạn Là TypeScript

Đã có (và sẽ tiếp tục có) nhiều đối thủ cạnh tranh dưới dạng _các cú pháp khác nhau_ được biên dịch sang _JavaScript_. TypeScript khác biệt ở chỗ _JavaScript của bạn chính là TypeScript_. Dưới đây là một biểu đồ minh họa:

![JavaScript is TypeScript](https://raw.githubusercontent.com/basarat/typescript-book/master/images/venn.png)

Điều này có nghĩa là _bạn cần phải học JavaScript_ (tin vui là _bạn **chỉ cần** học JavaScript_). TypeScript chỉ đơn giản là chuẩn hóa tất cả các cách bạn cung cấp _documentation tốt_ cho JavaScript.

- Chỉ cung cấp một cú pháp mới không giúp bắt lỗi, nhưng có thể giúp bạn viết mã sạch hơn / ít lỗi hơn (ví dụ: CoffeeScript).
- Tạo ra một ngôn ngữ mới có thể khiến bạn rời xa khỏi môi trường runtime và cộng đồng của mình – nhưng có thể giúp bạn tiếp cận dễ dàng hơn nếu đó là một ngôn ngữ quen thuộc (ví dụ: Dart - gần gũi hơn với các nhà phát triển Java / C#).

TypeScript chỉ là JavaScript kèm tài liệu.

> JSNext có tính mở để diễn giải - không phải mọi đề xuất cho phiên bản JS tiếp theo đều sẽ đến được với các trình duyệt. TypeScript chỉ bổ sung hỗ trợ cho các đề xuất khi chúng đạt đến [giai đoạn 3](https://tc39.es/process-document/).

## Cải Tiến JavaScript

TypeScript sẽ cố gắng bảo vệ bạn khỏi những phần của JavaScript vốn không bao giờ hoạt động đúng (vì vậy bạn không cần phải nhớ những điều này):

```ts
[] + []; // JavaScript sẽ cho bạn "", TypeScript sẽ báo lỗi

//
// các thứ vô lý khác trong JavaScript
// - không báo lỗi tại runtime (khiến việc gỡ lỗi trở nên khó khăn)
// - nhưng TypeScript sẽ báo lỗi tại thời điểm biên dịch (giúp việc gỡ lỗi không còn cần thiết)
//
{} + []; // JS : 0, TS Error
[] + {}; // JS : "[object Object]", TS Error
{} + {}; // JS : NaN or [object Object][object Object] depending upon browser, TS Error
"hello" - 1; // JS : NaN, TS Error

function add(a, b) {
  return;
  a + b; // JS : undefined, TS Error 'unreachable code detected'
}
```

Về cơ bản, TypeScript đang thực hiện kiểm tra lỗi cho JavaScript, và thực hiện điều đó tốt hơn so với các công cụ kiểm tra lỗi khác không có _thông tin kiểu dữ liệu_.

## Bạn Vẫn Cần Phải Học JavaScript

Như đã đề cập, TypeScript rất thực tế về việc bạn sẽ viết JavaScript, vì vậy có một số điều về JavaScript mà bạn vẫn cần phải biết để không bị bất ngờ. Chúng ta sẽ thảo luận về những điều đó trong phần tiếp theo.

> Lưu ý: TypeScript là một phần mở rộng của JavaScript, chỉ khác là nó có tài liệu mà các trình biên dịch / IDE có thể sử dụng được ;)
