- [Bắt đầu với TypeScript](#getting-started-with-typescript)
- [Phiên bản TypeScript](#typescript-version)

# Bắt Đầu Với TypeScript

TypeScript biên dịch thành JavaScript. JavaScript là ngôn ngữ mà bạn sẽ thực thi (dù là trong trình duyệt hay trên máy chủ). Vì vậy, bạn sẽ cần những thứ sau:

- Trình biên dịch TypeScript (mã nguồn mở có sẵn [trên GitHub](https://github.com/Microsoft/TypeScript/) và trên [NPM](https://www.npmjs.com/package/typescript))
- Trình soạn thảo TypeScript (bạn có thể sử dụng notepad nếu muốn, nhưng tôi sử dụng [vscode 🌹](https://code.visualstudio.com/) với một [extension tôi viết](https://marketplace.visualstudio.com/items?itemName=basarat.god). Ngoài ra, [nhiều IDE khác cũng hỗ trợ TypeScript](https://github.com/Microsoft/TypeScript/wiki/TypeScript-Editor-Support))

## Phiên Bản TypeScript

Thay vì sử dụng trình biên dịch TypeScript ổn định, chúng ta sẽ đề cập đến nhiều tính năng mới trong cuốn sách này mà có thể chưa được gán với số phiên bản cụ thể. Tôi thường khuyên mọi người nên sử dụng phiên bản nightly vì **bộ kiểm tra của trình biên dịch chỉ ngày càng phát hiện nhiều lỗi hơn theo thời gian**.

Bạn có thể cài đặt nó bằng dòng lệnh:

```bash
npm install -g typescript@next
```

Bây giờ dòng lệnh `tsc` sẽ là phiên bản mới nhất và tốt nhất. Nhiều IDE cũng hỗ trợ phiên bản này, ví dụ:

- Bạn có thể yêu cầu vscode sử dụng phiên bản này bằng cách tạo tệp `.vscode/settings.json` với nội dung sau:

```json
{
  "typescript.tsdk": "./node_modules/typescript/lib"
}
```

## Lấy Mã Nguồn

Mã nguồn của cuốn sách này có sẵn trong kho lưu trữ trên GitHub tại <https://github.com/basarat/typescript-book/tree/master/code> Hầu hết các đoạn mã mẫu có thể được sao chép vào vscode và bạn có thể thử nghiệm trực tiếp. Với các ví dụ mã cần thiết lập thêm (như cài đặt npm), chúng tôi sẽ liên kết đến mã mẫu trước khi trình bày đoạn mã. Ví dụ:

`this/will/be/the/link/to/the/code.ts`

```ts
// Đây sẽ là đoạn mã đang được thảo luận
```

Sau khi đã chuẩn bị xong môi trường phát triển, chúng ta hãy cùng tìm hiểu về cú pháp của TypeScript.
