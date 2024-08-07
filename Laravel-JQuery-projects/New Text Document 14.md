Lỗi bạn đang gặp phải là do bạn đang cố gắng ghi lại một đối tượng `Illuminate\Database\Eloquent\Builder` trực tiếp vào log. Điều này không thể thực hiện được vì đối tượng này không thể được chuyển đổi trực tiếp thành chuỗi. Thay vào đó, bạn cần lấy dữ liệu từ đối tượng này trước khi ghi nó vào log.

Dưới đây là cách khắc phục lỗi này:

1. **Chuyển đổi dữ liệu thành chuỗi JSON trước khi ghi vào log**:

   - Bạn có thể sử dụng phương thức `toJson()` để chuyển đổi dữ liệu thành chuỗi JSON trước khi ghi vào log.

2. **Lấy dữ liệu thực tế**:
   - Sử dụng phương thức `get()` để thực hiện truy vấn và lấy kết quả trước khi ghi vào log.

Dưới đây là ví dụ mã được cập nhật:

```php
class CategoryController extends Controller
{
    public function index(Request $request)
    {
        // Thực hiện truy vấn và lấy kết quả
        $categories = Category::select(['id', 'name', 'type'])->get();

        // Ghi dữ liệu vào log dưới dạng chuỗi JSON
        Log::info('List Category: ' . $categories->toJson());

        // Xử lý tiếp yêu cầu AJAX của DataTables
        if ($request->ajax()) {
            return DataTables::of($categories)
                ->addColumn('action', function ($row) {
                    return '<a href="javascript:void(0)" data-bs-target="#editModal" class="btn btn-info editButton" data-id="' . $row->id . '">Edit</a>';
                })
                ->rawColumns(['action'])
                ->make(true);
        }

        // Trả về view nếu không phải là yêu cầu AJAX
        return view('categories.index');
    }
}
```

### Giải thích chi tiết:

1. **Thực hiện truy vấn và lấy kết quả**:

   - `Category::select(['id', 'name', 'type'])->get();` sẽ thực hiện truy vấn và trả về một tập hợp các kết quả từ cơ sở dữ liệu.

2. **Chuyển đổi dữ liệu thành chuỗi JSON trước khi ghi vào log**:

   - `Log::info('List Category: ' . $categories->toJson());` sẽ ghi dữ liệu vào log dưới dạng chuỗi JSON, giúp bạn dễ dàng kiểm tra dữ liệu mà không gặp lỗi chuyển đổi đối tượng thành chuỗi.

3. **Xử lý tiếp yêu cầu AJAX của DataTables**:

   - `DataTables::of($categories)...` sẽ tạo DataTable từ kết quả truy vấn và trả về dưới dạng JSON để DataTables có thể sử dụng.

4. **Trả về view nếu không phải là yêu cầu AJAX**:
   - `return view('categories.index');` sẽ trả về view nếu yêu cầu không phải là AJAX, giúp bạn hiển thị giao diện người dùng.

Bằng cách làm theo các bước này, bạn có thể ghi lại dữ liệu vào log mà không gặp lỗi và xử lý yêu cầu DataTables một cách chính xác.
