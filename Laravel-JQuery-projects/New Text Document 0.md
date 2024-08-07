Việc sử dụng `FormData` không phải là một tính năng của jQuery mà là một tính năng có sẵn trong JavaScript. `FormData` là một API của JavaScript cho phép bạn dễ dàng xây dựng một tập hợp các cặp khóa-giá trị đại diện cho các trường form và giá trị của chúng. Bạn có thể sử dụng nó để gửi dữ liệu form thông qua AJAX.

### Ví dụ sử dụng `FormData` với JavaScript thuần

Dưới đây là cách sử dụng `FormData` với JavaScript thuần mà không cần jQuery:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <!-- Required meta tags -->
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />

    <!-- Bootstrap CSS -->
    <link
      href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/css/bootstrap.min.css"
      rel="stylesheet"
      integrity="sha384-EVSTQN3/azprG1Anm3QDgpJLIm9Nao0Yz1ztcQTwFspd3yD65VohhpuuCOmLASjC"
      crossorigin="anonymous"
    />

    <meta name="csrf-token" content="{{ csrf_token() }}" />
    <title>Create categories</title>
  </head>

  <body>
    <!-- Modal -->
    <div
      class="modal fade"
      id="exampleModal"
      tabindex="-1"
      aria-labelledby="exampleModalLabel"
      aria-hidden="true"
    >
      <form action="" id="ajaxForm">
        <div class="modal-dialog">
          <div class="modal-content">
            <div class="modal-header">
              <h5 class="modal-title" id="modal-title"></h5>
              <button
                type="button"
                class="btn-close"
                data-bs-dismiss="modal"
                aria-label="Close"
              ></button>
            </div>
            <div class="modal-body">
              <div class="form-group mb-3">
                <label for="">Name:</label>
                <input type="text" name="name" id="name" class="form-control" />
              </div>
              <div class="form-group mb-1">
                <label for="">Type:</label>
                <select id="type" name="type" class="form-control">
                  <option disabled selected>Choose Option</option>
                  <option value="electronic">Electronic</option>
                  <option value="mobile">Mobile</option>
                </select>
              </div>
            </div>
            <div class="modal-footer">
              <button
                type="button"
                class="btn btn-secondary"
                data-bs-dismiss="modal"
              >
                Close
              </button>
              <button
                type="button"
                class="btn btn-primary"
                id="saveBtn"
              ></button>
            </div>
          </div>
        </div>
      </form>
    </div>

    <div class="row">
      <div class="col-md-6 offset-3" style="margin-top: 100px">
        <!-- Button trigger modal -->
        <button
          type="button"
          class="btn btn-info"
          data-bs-toggle="modal"
          data-bs-target="#exampleModal"
        >
          Add category
        </button>
      </div>
    </div>

    <script
      src="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/js/bootstrap.bundle.min.js"
      integrity="sha384-MrcW6ZMFYlzcLA8Nl+NtUVF0sA7MsXsP1UyJoMp4YLEuNSfAP+JcXn/tWtIaxVXM"
      crossorigin="anonymous"
    ></script>

    <script>
      document.addEventListener("DOMContentLoaded", function () {
        var csrfToken = document
          .querySelector('meta[name="csrf-token"]')
          .getAttribute("content");

        document.getElementById("modal-title").innerHTML = "Create category";
        document.getElementById("saveBtn").innerHTML = "Save category";

        document
          .getElementById("saveBtn")
          .addEventListener("click", function () {
            var form = document.getElementById("ajaxForm");
            var formData = new FormData(form);

            fetch('{{ route("categories.store") }}', {
              method: "POST",
              headers: {
                "X-CSRF-TOKEN": csrfToken,
              },
              body: formData,
            })
              .then((response) => response.json())
              .then((data) => {
                console.log(data);
              })
              .catch((error) => {
                console.error("Error:", error);
              });
          });
      });
    </script>
  </body>
</html>
```

### Giải thích

- **Tạo đối tượng `FormData`**: `new FormData(form)` tạo ra một đối tượng `FormData` từ phần tử form, thu thập tất cả các trường và giá trị của chúng.
- **Sử dụng `fetch` API**: Gửi yêu cầu POST đến server với body là `FormData` và headers chứa CSRF token.

### So sánh với jQuery

- **JavaScript thuần**:
  ```javascript
  var form = document.getElementById("ajaxForm");
  var formData = new FormData(form);
  ```
- **jQuery**:
  ```javascript
  var form = $("#ajaxForm")[0];
  var formData = new FormData(form);
  ```

Như vậy, `FormData` là một tính năng của JavaScript và không phụ thuộc vào jQuery. Việc sử dụng jQuery chỉ là để dễ dàng thao tác với DOM và thực hiện các yêu cầu AJAX.
