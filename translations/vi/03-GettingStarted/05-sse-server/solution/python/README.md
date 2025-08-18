<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "69ba3bd502bd743233137bac5539c08b",
  "translation_date": "2025-08-18T17:22:07+00:00",
  "source_file": "03-GettingStarted/05-sse-server/solution/python/README.md",
  "language_code": "vi"
}
-->
# Chạy mẫu này

Bạn được khuyến nghị cài đặt `uv` nhưng không bắt buộc, xem [hướng dẫn](https://docs.astral.sh/uv/#highlights)

## -0- Tạo môi trường ảo

```bash
python -m venv venv
```

## -1- Kích hoạt môi trường ảo

```bash
venv\Scrips\activate
```

## -2- Cài đặt các phụ thuộc

```bash
pip install "mcp[cli]"
```

## -3- Chạy mẫu

```bash
uvicorn server:app
```

## -4- Kiểm tra mẫu

Với máy chủ đang chạy trong một terminal, mở một terminal khác và chạy lệnh sau:

```bash
mcp dev server.py
```

Điều này sẽ khởi động một máy chủ web với giao diện trực quan cho phép bạn kiểm tra mẫu.

Khi máy chủ đã kết nối:

- thử liệt kê các công cụ và chạy `add`, với tham số 2 và 4, bạn sẽ thấy kết quả là 6.
- đi đến tài nguyên và mẫu tài nguyên, gọi hàm get_greeting, nhập một tên và bạn sẽ thấy lời chào với tên bạn đã cung cấp.

### Kiểm tra ở chế độ CLI

Trình kiểm tra mà bạn đã chạy thực chất là một ứng dụng Node.js và `mcp dev` là một wrapper xung quanh nó.

Bạn có thể khởi động trực tiếp ở chế độ CLI bằng cách chạy lệnh sau:

```bash
npx @modelcontextprotocol/inspector --cli http://localhost:8000/sse --method tools/list
```

Điều này sẽ liệt kê tất cả các công cụ có sẵn trong máy chủ. Bạn sẽ thấy đầu ra sau:

```text
{
  "tools": [
    {
      "name": "add",
      "description": "Add two numbers",
      "inputSchema": {
        "type": "object",
        "properties": {
          "a": {
            "title": "A",
            "type": "integer"
          },
          "b": {
            "title": "B",
            "type": "integer"
          }
        },
        "required": [
          "a",
          "b"
        ],
        "title": "addArguments"
      }
    }
  ]
}
```

Để gọi một công cụ, nhập:

```bash
npx @modelcontextprotocol/inspector --cli http://localhost:8000/sse --method tools/call --tool-name add --tool-arg a=1 --tool-arg b=2
```

Bạn sẽ thấy đầu ra sau:

```text
{
  "content": [
    {
      "type": "text",
      "text": "3"
    }
  ],
  "isError": false
}
```

> [!TIP]
> Thông thường chạy trình kiểm tra ở chế độ CLI nhanh hơn nhiều so với trên trình duyệt.
> Đọc thêm về trình kiểm tra [tại đây](https://github.com/modelcontextprotocol/inspector).

**Tuyên bố miễn trừ trách nhiệm**:  
Tài liệu này đã được dịch bằng dịch vụ dịch thuật AI [Co-op Translator](https://github.com/Azure/co-op-translator). Mặc dù chúng tôi cố gắng đảm bảo độ chính xác, xin lưu ý rằng các bản dịch tự động có thể chứa lỗi hoặc không chính xác. Tài liệu gốc bằng ngôn ngữ bản địa nên được coi là nguồn tham khảo chính thức. Đối với các thông tin quan trọng, nên sử dụng dịch vụ dịch thuật chuyên nghiệp từ con người. Chúng tôi không chịu trách nhiệm cho bất kỳ sự hiểu lầm hoặc diễn giải sai nào phát sinh từ việc sử dụng bản dịch này.