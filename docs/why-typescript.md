# Tại Sao Nên Dùng TypeScript

TypeScript có hai mục tiêu chính:

- Cung cấp một _hệ thống kiểu_ tùy chọn cho JavaScript.
- Cung cấp các tính năng dự kiến trong các phiên bản JavaScript tương lai cho các công cụ JavaScript hiện tại.

Lý do để đạt được các mục tiêu này sẽ được giải thích dưới đây.

## Hệ Thống Kiểu Trong TypeScript

Bạn có thể thắc mắc, "**Tại sao cần thêm kiểu vào JavaScript?**"

Các kiểu dữ liệu đã chứng minh được khả năng nâng cao chất lượng mã và tính dễ hiểu. Các đội ngũ lớn (Google, Microsoft, Facebook) đã liên tục đưa ra kết luận này. Cụ thể:

- Các kiểu dữ liệu tăng khả năng linh hoạt khi bạn thực hiện tái cấu trúc mã. _Tốt hơn là để trình biên dịch bắt lỗi thay vì phát hiện lỗi khi chạy._.
- Các kiểu dữ liệu là một trong những dạng tài liệu tốt nhất mà bạn có thể có. _Chữ ký của hàm là định lý, và thân hàm là lời chứng minh_.

Tuy nhiên, các kiểu dữ liệu cũng có thể khiến cho mã trở nên phức tạp không cần thiết. TypeScript rất chú trọng đến việc giữ mức độ cản trở gia nhập càng thấp càng tốt. Đây là cách TypeScript làm điều đó:

### JavaScript Của Bạn Là TypeScript

TypeScript cung cấp tính an toàn kiểu dữ liệu trong quá trình biên dịch cho mã JavaScript của bạn. Điều này không có gì ngạc nhiên vì tên gọi của nó. Điều tuyệt vời là các kiểu dữ liệu là hoàn toàn tùy chọn. Tập tin `.js` của bạn có thể được đổi tên thành `.ts` và TypeScript sẽ vẫn trả về mã `.js` hợp lệ tương đương với tập tin JavaScript gốc. TypeScript _cố tình_ và nghiêm ngặt\* là một phần mở rộng của JavaScript với việc kiểm tra kiểu dữ liệu tùy chọn.

\*Ghi chú của người dịch: Tác giả sử dụng từ nghiêm ngặt ở đây (tiếng Anh: "strictly") có ý nói mục tiêu chính của TypeScript chỉ là một phần mở rộng của JavaScript thôi, và TypeScript đã được cố tình xây dựng với triết lý này.

### Các Kiểu Dữ Liệu Có Thể Được Suy Luận

TypeScript sẽ cố gắng suy luận càng nhiều thông tin kiểu dữ liệu càng tốt để mang lại tính an toàn kiểu dữ liệu với chi phí tối thiểu trong quá trình phát triển mã. Ví dụ, trong đoạn mã sau, TypeScript sẽ biết rằng `foo` có kiểu `number` và sẽ báo lỗi ở dòng thứ hai như sau:

```ts
var foo = 123;
foo = "456"; // Error: cannot assign `string` to `number`

// Is foo a number or a string?
```

Việc suy luận kiểu này có động cơ rõ ràng. Nếu bạn viết mã như trong ví dụ này, thì trong phần còn lại của mã, bạn sẽ không chắc `foo` là `number` hay `string`. Những vấn đề như thế này thường xuất hiện trong các dự án lớn với nhiều tệp mã. Chúng ta sẽ đi sâu vào các quy tắc suy luận kiểu sau này.

### Các Kiểu Dữ Liệu Có Thể Được Chỉ Rõ

Như đã đề cập, TypeScript sẽ suy luận những gì có thể. Tuy nhiên, bạn có thể sử dụng các chú thích kiểu để:

1. Hỗ trợ trình biên dịch và quan trọng hơn là cung cấp tài liệu cho nhà phát triển tiếp theo (có thể là chính bạn trong tương lai!).
2. Đảm bảo rằng những gì trình biên dịch thấy là những gì bạn mong đợi. Điều đó có nghĩa là hiểu biết của bạn về mã phù hợp với phân tích thuật toán của mã (do trình biên dịch thực hiện).

TypeScript sử dụng chú thích kiểu dữ liệu hậu tố, phổ biến trong các ngôn ngữ _tùy chọn_ có chú thích kiểu dữ liệu khác (ví dụ: ActionScript và F#).

```ts
var foo: number = 123;
```

Vì vậy, nếu bạn làm sai điều gì đó, trình biên dịch sẽ báo lỗi, ví dụ:

```ts
var foo: number = "123"; // Error: cannot assign a `string` to a `number`
```

Chúng ta sẽ thảo luận chi tiết về tất cả các cú pháp chú thích mà TypeScript hỗ trợ trong một chương sau.

### Các Kiểu Dữ Liệu Là Cấu Trúc

Trong một số ngôn ngữ (cụ thể là những ngôn ngữ được đánh máy theo tên), việc đánh máy tĩnh dẫn đến các thủ tục không cần thiết vì ngay cả khi bạn biết mã sẽ hoạt động tốt, ngữ nghĩa của ngôn ngữ vẫn buộc bạn phải sao chép các thành phần. Đây là lý do tại sao những công cụ như [automapper cho C#](http://automapper.org/) _rất quan trọng_ đối với C#. Trong TypeScript, vì chúng tôi muốn dễ dàng cho các nhà phát triển JavaScript với mức độ nhận thức tối thiểu, các kiểu dữ liệu là _cấu trúc_. Điều này có nghĩa là _duck typing_ là một thành phần ngôn ngữ chính thức. Hãy xem xét ví dụ sau. Hàm `iTakePoint2D` sẽ chấp nhận bất cứ thứ gì chứa tất cả các thành phần (`x` và `y`) mà nó yêu cầu:

```ts
interface Point2D {
  x: number;
  y: number;
}
interface Point3D {
  x: number;
  y: number;
  z: number;
}
var point2D: Point2D = { x: 0, y: 10 };
var point3D: Point3D = { x: 0, y: 10, z: 20 };
function iTakePoint2D(point: Point2D) {
  /* do something */
}

iTakePoint2D(point2D); // exact match okay
iTakePoint2D(point3D); // extra information okay
iTakePoint2D({ x: 0 }); // Error: missing information `y`
```

### Lỗi Kiểu Dữ Liệu Không Ngăn Cản Việc Biên Dịch JavaScript

Để giúp bạn dễ dàng di chuyển mã JavaScript của mình sang TypeScript, ngay cả khi có lỗi biên dịch, mặc định TypeScript _vẫn sẽ biên dịch ra mã JavaScript hợp lệ_ tốt nhất có thể. Ví dụ:

```ts
var foo = 123;
foo = "456"; // Error: cannot assign a `string` to a `number`
```

sẽ biên dịch ra mã JavaScript như sau:

```ts
var foo = 123;
foo = "456";
```

Vì vậy, bạn có thể nâng cấp mã JavaScript của mình sang TypeScript theo từng bước nhỏ. Đây là điểm khác biệt rất lớn so với cách mà nhiều trình biên dịch ngôn ngữ khác hoạt động và là một lý do nữa để chuyển sang TypeScript.

### Các Kiểu Dữ Liệu Có Thể Là Môi Trường

Một mục tiêu thiết kế quan trọng của TypeScript là cho phép bạn sử dụng an toàn và dễ dàng các thư viện JavaScript hiện có trong TypeScript. TypeScript thực hiện điều này bằng cách sử dụng các khai báo. TypeScript cung cấp cho bạn một phạm vi linh hoạt về mức độ nỗ lực mà bạn muốn đặt vào các khai báo, nỗ lực càng nhiều thì bạn càng có nhiều tính an toàn kiểu dữ liệu + tính thông minh của mã. Lưu ý rằng định nghĩa cho hầu hết các thư viện JavaScript phổ biến đã được viết sẵn bởi cộng đồng [DefinitelyTyped community](https://github.com/borisyankov/DefinitelyTyped) vì vậy cho hầu hết các mục đích, hoặc:

1. Tệp định nghĩa đã tồn tại.
2. Hoặc ít nhất, bạn có sẵn một danh sách lớn các mẫu khai báo TypeScript đã được đánh giá tốt.

Lấy ví dụ nhanh về cách bạn có thể tự viết tệp khai báo cho [jquery](https://jquery.com/). Mặc định (như mong đợi từ mã JS tốt), TypeScript yêu cầu bạn khai báo (tức là sử dụng `var` ở đâu đó) trước khi sử dụng biến:

```ts
$(".awesome").show(); // Error: cannot find name `$`
```

Để khắc phục nhanh _bạn có thể nói với TypeScript_ rằng thực sự có thứ gọi là `$`:

```ts
declare var $: any;
$(".awesome").show(); // Okay!
```

Nếu muốn, bạn có thể mở rộng định nghĩa cơ bản này và cung cấp thêm thông tin để giúp tránh lỗi:

```ts
declare var $: {
  (selector: string): any;
};
$(".awesome").show(); // Okay!
$(123).show(); // Error: selector needs to be a string
```

Chúng ta sẽ thảo luận chi tiết việc tạo các khai báo TypeScript cho các thư viện JavaScript hiện có khi bạn đã hiểu thêm về TypeScript (ví dụ: `interface` và `any`).

## JavaScript Tương Lai => Hiện Tại

TypeScript cung cấp một số tính năng được lên kế hoạch trong ES6 cho các công cụ JavaScript hiện tại (chỉ hỗ trợ ES5, v.v.). Nhóm TypeScript đang tích cực bổ sung những tính năng này và danh sách này chỉ ngày càng lớn hơn theo thời gian. Chúng ta sẽ đề cập đến điều này trong một phần riêng. Nhưng ví dụ, dưới đây là một lớp:

```ts
class Point {
  constructor(
    public x: number,
    public y: number,
  ) {}
  add(point: Point) {
    return new Point(this.x + point.x, this.y + point.y);
  }
}

var p1 = new Point(0, 10);
var p2 = new Point(10, 20);
var p3 = p1.add(p2); // { x: 10, y: 30 }
```

và hàm mũi tên đẹp:

```ts
var inc = (x) => x + 1;
```

### Tóm Lược

rong phần này, chúng tôi đã cung cấp cho bạn lý do và các mục tiêu thiết kế của TypeScript. Giờ thì hãy bắt đầu tìm hiểu chi tiết về TypeScript.

[](Interfaces are open ended)
[](Type Inference rules)
[](Cover all the annotations)
[](Cover all ambients : also that there are no runtime enforcement)
[](.ts vs. .d.ts)
