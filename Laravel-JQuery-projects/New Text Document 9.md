Đoạn mã này sử dụng thư viện Yajra DataTables để tạo một cột tùy chỉnh trong bảng DataTable hiển thị trên client side. Cụ thể, đoạn mã này thêm một cột mới có tên là `action`, chứa các nút hành động như chỉnh sửa hoặc xóa. Dưới đây là giải thích chi tiết về các phương thức `addColumn` và `rawColumns`.

### Giải thích chi tiết

#### 1. `->addColumn('action', function () { ... })`
- **Mục đích**: Thêm một cột mới có tên là `action` vào DataTable.
- **Tham số**:
  - `'action'`: Tên của cột mới.
  - `function () { ... }`: Một hàm ẩn danh (anonymous function) để xác định nội dung của cột `action`.
- **Nội dung**:
  - Hàm ẩn danh trả về HTML của một nút `<a>`. Trong trường hợp này, nó tạo ra một nút `<a>` với lớp CSS là `btn btn-info`.
  - Nút này hiện tại không có URL (`href=""`) và không có nội dung hiển thị. Bạn có thể thêm URL và nội dung tùy chỉnh dựa trên nhu cầu của mình.

```php
->addColumn('action', function () {
    return '<a href="" class="btn btn-info"></a>';
})
```

#### 2. `->rawColumns(['action'])`
- **Mục đích**: Cho phép DataTables render nội dung HTML thô trong cột `action`.
- **Tham số**:
  - `['action']`: Mảng chứa tên của các cột mà bạn muốn render nội dung HTML thô.
- **Chi tiết**:
  - Mặc định, DataTables sẽ escape (loại bỏ) các ký tự đặc biệt trong dữ liệu để ngăn chặn các lỗ hổng XSS (Cross-Site Scripting). Điều này có nghĩa là HTML sẽ được hiển thị dưới dạng chuỗi văn bản, không phải là HTML.
  - `rawColumns(['action'])` cho phép DataTables render nội dung HTML trong cột `action`, tức là nút `<a>` sẽ được hiển thị như một nút thực sự thay vì là một chuỗi văn bản.

```php
->rawColumns(['action'])
```

### Tổng kết

Đoạn mã hoàn chỉnh của bạn:

```php
public function index(Request $request)
{
    $categories = Category::all();

    if ($request->ajax()) {
        return DataTables::of($categories)
            ->addColumn('action', function () {
                return '<a href="" class="btn btn-info"></a>';
            })
            ->rawColumns(['action'])
            ->make(true);
    }
}
```

- **`addColumn('action', function () { ... })`**: Thêm một cột mới có tên `action` và định nghĩa nội dung của cột này là một nút `<a>` với lớp `btn btn-info`.
- **`rawColumns(['action'])`**: Cho phép DataTables render nội dung HTML thô trong cột `action`.

Kết quả là DataTable sẽ có thêm một cột `action` với các nút hành động được hiển thị như HTML thực sự, cho phép bạn thêm các hành động như chỉnh sửa hoặc xóa trực tiếp từ bảng.

Nếu bạn có thêm câu hỏi hoặc cần giải thích chi tiết hơn, hãy cho tôi biết!