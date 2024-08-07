Trong mã của bạn, `form` là một jQuery object được chọn bằng cách sử dụng ID `#ajaxForm`. Vì bạn chỉ có một form với ID `#ajaxForm`, nên `form[0]` là phần tử DOM đầu tiên (và duy nhất) trong jQuery object đó.

Khi bạn sử dụng jQuery để chọn một phần tử dựa trên ID, nó sẽ luôn trả về một jQuery object chứa một phần tử duy nhất. Trong trường hợp này, jQuery object đó chứa một phần tử DOM là form của bạn. Để truy cập trực tiếp vào phần tử DOM này, bạn sử dụng `form[0]`.

### Giải thích chi tiết

1. **Chọn phần tử với jQuery**:
   ```javascript
   var form = $("#ajaxForm");
   ```
   - Đây là jQuery object chứa tất cả các phần tử DOM khớp với selector `#ajaxForm`.
   - Trong trường hợp này, vì ID là duy nhất trong trang HTML, nó sẽ chỉ chứa một phần tử DOM.

2. **Truy cập phần tử DOM bên trong jQuery object**:
   ```javascript
   var formData = new FormData(form[0]);
   ```
   - `form[0]` truy cập vào phần tử DOM đầu tiên trong jQuery object.
   - Nếu bạn có nhiều phần tử DOM khớp với selector, bạn có thể truy cập chúng bằng cách thay đổi chỉ số, ví dụ: `form[1]`, `form[2]`, v.v.

### Tại sao không phải là `form[1]` hay `form[2]`?

- Trong trường hợp của bạn, chỉ có một form với ID `#ajaxForm` trên trang HTML.
- `form[1]` hay `form[2]` sẽ chỉ tồn tại nếu bạn có nhiều hơn một form với cùng ID, điều này không hợp lệ vì ID phải là duy nhất trong một trang HTML.
- Nếu bạn có nhiều form và muốn truy cập các form khác, bạn cần phải sử dụng class hoặc một selector khác để chọn chúng. Ví dụ:
  ```html
  <form class="ajaxForm"></form>
  <form class="ajaxForm"></form>
  ```
  ```javascript
  var forms = $(".ajaxForm");
  var formData1 = new FormData(forms[0]); // Form đầu tiên
  var formData2 = new FormData(forms[1]); // Form thứ hai
  ```

Trong trường hợp của bạn, vì bạn chỉ có một form với ID `#ajaxForm`, việc sử dụng `form[0]` là hoàn toàn hợp lý và đúng đắn.