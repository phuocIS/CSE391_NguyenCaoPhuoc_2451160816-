# Phần A - Kiểm tra đọc hiểu

## Câu A1 — HTTP & Browser

- Khi gõ https://shopee.vn vào trình duyệt và nhấn Enter, thứ tự 5 bước xảy ra là:

1. Gửi Request: trình duyệt hỏi DNS Server "shopee.vn là IP nào?" và nhận về địa chỉ IP sau đó gửi yêu cầu đến Server thông qua mạng Internet
2. Server xử lý: "Trường muốn xem trang chủ shopee"
3. HTTP Response: Server sẽ gửi các file như html, css, js cho bên trình duyệt cũng thông qua mạng Internet
4. Parse html, css & execute js: Trình duyệt sẽ đọc các file html như bản kiến trúc, css như bản nội thất và xử lý js như lắp đặt hệ thống điện nước
5. Paint & render: Trình duyệt sẽ hoàn thiện và hiển thị giao diện lên trên màn hình cho Trường xem

- Tab Network cho thấy toàn bộ các request mà trình duyệt gửi đi khi tải trang

![CauA1](./screenshots/cauA1.png)

## Câu A2 — Semantic HTML

Lỗi 1 — Dùng `<div>` thay vì thẻ semantic
Google không hiểu đâu là header, nav, main, footer. Với `<div class="header">` thì class "header" chỉ là tên cho con người đọc, máy không hiểu.

Lỗi 2 — Không có thẻ `<h1>` hay heading nào
Google dùng heading để hiểu nội dung chính của trang. Tên sản phẩm "iPhone 16 Pro" đang nằm trong `<div class="title">` — Google không biết đây là tiêu đề quan trọng.

Lỗi 3 — Thẻ `<img>` thiếu thuộc tính alt
Google đọc alt để hiểu ảnh nói về cái gì. Thiếu alt thì ảnh vô nghĩa với cả Google lẫn người dùng dùng screen reader.

Lỗi 4 — Menu điều hướng không dùng `<nav>`
Google ưu tiên `<nav>` để xác định cấu trúc điều hướng của trang. Dùng `<div class="menu">` thì Google không nhận ra đây là menu.

### Sửa lại lỗi

```html
<header>
  <div class="logo">ShopTLU</div>
  <nav>
    <ul>
      <li><a href="/">Trang chủ</a></li>
      <li><a href="/products">Sản phẩm</a></li>
    </ul>
  </nav>
</header>

<main>
  <article class="product">
    <h1>iPhone 16 Pro</h1>
    <p class="price">25.990.000đ</p>
    <img src="iphone.jpg" alt="iPhone 16 Pro" />
  </article>
</main>

<footer>© 2026 ShopTLU</footer>
```

## Câu A3 - Block vs Inline

```
┌─────────────┐
│   Hộp 1     │  ← div: chiếm cả hàng
└─────────────┘
Text A Text B     ← span: nằm cùng hàng nhau
┌─────────────┐
│   Hộp 2     │  ← div: xuống hàng mới
└─────────────┘
Text C **Text D**  ← span + strong: cùng hàng, Text D in đậm
┌─────────────┐
│   Hộp 3     │  ← div: xuống hàng mới
└─────────────┘
```

## Câu A4 — Table

- `<thead>` là phần đầu bảng (tiêu đề cột)
- `<tbody>` là phần thân bảng (dữ liệu chính)
- `<tfoot>` là phần chân bảng (tổng kết)

Lý do không nên dùng table để tạo layout trang web

1. Lý do 1 — Sai ngữ nghĩa (semantic)
   `<table>` sinh ra để hiển thị dữ liệu dạng bảng, không phải để chia cột layout. Google và screen reader hiểu `<table>` là "đây là bảng dữ liệu" — dùng sai mục đích làm SEO và accessibility kém đi.

2. Lý do 2 — Code phức tạp, khó bảo trì
   Layout bằng table phải lồng `<tr>`, `<td>` chằng chịt, rất khó đọc và sửa. Thêm một cột hay thay đổi bố cục là phải sửa rất nhiều chỗ.

3. Lý do 3 — Tải chậm hơn
   Trình duyệt phải đọc toàn bộ table trước khi render, vì cần biết kích thước tất cả các ô.

# Phần B: Thực hành code

## Bài B3 — Debug HTML

Lỗi 1: Dòng 1 — `<!DOCTYPE>` thiếu khai báo html — Sửa thành `<!DOCTYPE html>`

Lỗi 2: Dòng 2 — `<html>` thiếu thuộc tính `lang` — Sửa thành `<html lang="vi">`

Lỗi 3: Dòng 4 — `<title>Trang web` không có thẻ đóng — Sửa thành `<title>Trang web</title>`

Lỗi 4: Dòng 5 — `<meta charset="utf8">` sai giá trị charset — Sửa thành `<meta charset="UTF-8">`

Lỗi 5: Dòng 8 — `<h1>Welcome to ShopTLU<h1>` thẻ đóng thiếu dấu `/` — Sửa thành `<h1>Welcome to ShopTLU</h1>`

Lỗi 6: Dòng 11 — `<a href="home">Trang chủ<a>` thẻ đóng thiếu dấu `/` và href không dùng `#` — Sửa thành `<a href="#home">Trang chủ</a>`

Lỗi 7: Dòng 19 — `<img src=iphone.jpg>` src không có dấu nháy và thiếu thuộc tính `alt` — Sửa thành `<img src="iphone.jpg" alt="iPhone 16 Pro">`

Lỗi 8: Dòng 21 — `<p>Giá: <b>25.990.000đ</p></b>` thẻ đóng bị lồng sai thứ tự — Sửa thành `<p>Giá: <b>25.990.000đ</b></p>`

Lỗi 9: Dòng 26 — Hàng đầu tiên của bảng dùng `<td>` thay vì `<th>`, và bảng thiếu `<thead>`/`<tbody>` — Sửa bằng cách thêm `<thead><tbody>` và đổi `<td>` thành `<th>` cho hàng tiêu đề

Lỗi 10: Dòng 40 — Dùng `<main>` lần 2 cho sidebar — Một trang chỉ được có 1 thẻ `<main>`, sidebar phải dùng `<aside>` — Sửa thành `<aside>` nằm trong `<main>`

Lỗi 11: Dòng 17 — `<h1>` nằm ngoài `<header>` và đứng trước `<header>` — Semantic sai, `<h1>` nên nằm trong `<header>`

Lỗi 12: Dòng 45 — `<p>Copyright 2026` không có thẻ đóng `</p>` — Sửa thành `<p>Copyright 2026</p>`

Lỗi 13: Dòng 20 — `<h3>Sản phẩm hot</h3>` nhảy từ `<h1>` xuống thẳng `<h3>`, bỏ qua `<h2>` — Sai cấu trúc heading, sửa thành `<h2>`

## Bài B4 — Phân tích trang web thật

Trong trang web thegioididong.com:

1. Ba thẻ semantic HTML5 mà trang đó sử dụng

- Thẻ `<header>` ![thẻ header](./screenshots/cauB4_header.png)
- Thẻ `<section>` ![thẻ section](./screenshots/cauB4_section.png)
- Thẻ `<footer>` ![thẻ footer](./screenshots/cauB4_footer.png)
- Thẻ `<body>` mà trang đó KHÔNG dùng đúng semantic ![thẻ body](./screenshots/cauB4_body_sai.png)

2. Thẻ `<table>` hiển thị chi tiết nội dung sản phẩm, thẻ đó chỉ dùng `tbody>` không `<thead>`![thẻ table](./screenshots/cauB4_table.png)
3. Thẻ `<form>` ![thẻ form](./screenshots/cauB4_form.png)

- Form có action là <`action="/tim-kiem"`>. Khi submit, dữ liệu sẽ được gửi đến đường dẫn `/tim-kiem`
- Không có method nên sẽ mặc định là GET
- Input có 2 loại là text để nhập và button để click

# Phần C: Suy luận

## Câu C1 — Thiết kế cấu trúc

```html
<!doctype html>
<html lang="vi">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>iPhone 16 Pro — ShopTLU</title>
  </head>
  <body>
    <header>
      <!-- header: phần đầu trang, chứa logo và nav -->
      <div class="logo">ShopTLU</div>
      <!-- div: nhóm logo -->
      <nav>
        <!-- nav: điều hướng chính của trang -->
        <ul>
          <!-- ul: danh sách menu không có thứ tự -->
          <li><a href="#home">Trang chủ</a></li>
          <li><a href="#products">Sản phẩm</a></li>
          <li><a href="#contact">Liên hệ</a></li>
        </ul>
      </nav>
    </header>

    <nav aria-label="breadcrumb">
      <!-- nav: điều hướng phụ, aria-label phân biệt với nav chính -->
      <ol>
        <!-- ol: có thứ tự rõ ràng (Trang chủ > Điện thoại > Sản phẩm) -->
        <li><a href="#">Trang chủ</a></li>
        <li><a href="#">Điện thoại</a></li>
        <li aria-current="page">iPhone 16 Pro</li>
        <!-- aria-current: báo đây là trang hiện tại -->
      </ol>
    </nav>

    <main>
      <!-- main: nội dung chính, mỗi trang chỉ có 1 thẻ main -->

      <section id="product-detail">
        <!-- section: khu vực thông tin sản phẩm có chủ đề rõ ràng -->

        <figure>
          <!-- figure: nhóm ảnh có liên quan đến nhau -->
          <img src="https://placehold.co/600x400" alt="iPhone 16 Pro - ảnh chính" loading="lazy" />
          <!-- loading = lazy là khi người dùng lướt đến mới load ảnh -->
          <img src="https://placehold.co/100x100" alt="iPhone 16 Pro - ảnh 2" loading="lazy" />
          <img src="https://placehold.co/100x100" alt="iPhone 16 Pro - ảnh 3" loading="lazy" />
          <img src="https://placehold.co/100x100" alt="iPhone 16 Pro - ảnh 4" loading="lazy" />
          <img src="https://placehold.co/100x100" alt="iPhone 16 Pro - ảnh 5" loading="lazy" />
          <figcaption>iPhone 16 Pro — 5 góc nhìn</figcaption>
          <!-- figcaption: mô tả cho figure -->
        </figure>

        <article>
          <!-- article: thông tin sản phẩm là nội dung độc lập, có thể đứng riêng -->
          <h1>iPhone 16 Pro</h1>
          <!-- h1: tiêu đề quan trọng nhất trang -->
          <p><strong>25.990.000đ</strong></p>
          <!-- strong: nhấn mạnh giá, có ngữ nghĩa "quan trọng" -->
          <div class="rating">
            <!-- div: nhóm đánh giá sao, không có thẻ semantic phù hợp hơn -->
            <span>★★★★★</span>
            <!-- span: inline text, không cần block element -->
            <span>(1.234 đánh giá)</span>
          </div>
          <p>Chip A18 Pro, Camera 48MP, màn hình 6.3 inch Super Retina XDR, pin cả ngày.</p>
        </article>
      </section>

      <section id="specs">
        <!-- section: khu vực thông số kỹ thuật riêng biệt -->
        <h2>Thông số kỹ thuật</h2>
        <table border="1">
          <!-- table: đúng mục đích hiển thị dữ liệu dạng bảng -->
          <thead>
            <!-- thead: phân biệt phần tiêu đề với dữ liệu -->
            <tr>
              <th>Thông số</th>
              <!-- th: tiêu đề cột, Google hiểu đây là nhãn -->
              <th>Chi tiết</th>
            </tr>
          </thead>
          <tbody>
            <!-- tbody: chứa dữ liệu chính của bảng -->
            <tr>
              <td>Chip</td>
              <td>Apple A18 Pro</td>
            </tr>
            <tr>
              <td>RAM</td>
              <td>8GB</td>
            </tr>
            <tr>
              <td>Bộ nhớ</td>
              <td>256GB</td>
            </tr>
            <tr>
              <td>Camera</td>
              <td>48MP + 12MP + 12MP</td>
            </tr>
            <tr>
              <td>Pin</td>
              <td>3274mAh</td>
            </tr>
          </tbody>
        </table>
      </section>

      <section id="reviews">
        <!-- section: khu vực đánh giá riêng biệt -->
        <h2>Đánh giá từ khách hàng</h2>

        <article>
          <!-- article: mỗi bình luận là nội dung độc lập -->
          <h3>Nguyễn Văn A</h3>
          <p>Sản phẩm rất tốt, giao hàng nhanh!</p>
        </article>

        <article>
          <h3>Trần Thị B</h3>
          <p>Camera chụp đẹp, pin trâu, rất hài lòng.</p>
        </article>
      </section>

      <aside>
        <!-- aside: sản phẩm tương tự là nội dung phụ, bỏ đi không ảnh hưởng nội dung chính -->
        <h2>Sản phẩm tương tự</h2>
        <ul>
          <!-- ul: danh sách sản phẩm không có thứ tự -->
          <li>
            <a href="#">
              <img src="https://placehold.co/150x100" alt="iPhone 15 Pro" loading="lazy" />
              <p>iPhone 15 Pro</p>
              <p><strong>22.990.000đ</strong></p>
            </a>
          </li>
          <li>
            <a href="#">
              <img src="https://placehold.co/150x100" alt="Samsung Galaxy S25" loading="lazy" />
              <p>Samsung Galaxy S25</p>
              <p><strong>22.490.000đ</strong></p>
            </a>
          </li>
        </ul>
      </aside>
    </main>

    <footer>
      <!-- footer: chân trang -->
      <p>&copy; 2026 ShopTLU. All rights reserved.</p>
      <nav>
        <!-- nav: điều hướng footer -->
        <a href="#">Chính sách bảo mật</a>
        <a href="#">Liên hệ</a>
        <a href="#">FAQ</a>
      </nav>
    </footer>
  </body>
</html>
```

## Câu C2 — So sánh & Tranh luận

Quan điểm "dùng `<div>` cho mọi thứ rồi thêm class là được" nghe có vẻ tiện, nhưng thực ra đang bỏ qua những lợi ích kỹ thuật quan trọng. Về mặt SEO, Google không chỉ đọc nội dung mà còn đọc cấu trúc trang — khi dùng `<article>`, `<nav>`, `<header>`, Google biết ngay đâu là nội dung chính, đâu là điều hướng, từ đó xếp hạng trang cao hơn so với đối thủ chỉ dùng `<div>`. Về mặt Accessibility, người khiếm thị dùng screen reader để duyệt web — phần mềm này dựa vào semantic tags để nhảy thẳng đến `<main>` hay `<nav>` mà không cần đọc toàn bộ trang. Nếu tất cả là `<div>`, screen reader không biết đường mà nhảy. Ví dụ cụ thể: thay `<div class="nav">` bằng `<nav>`, người dùng bàn phím có thể nhấn phím tắt để nhảy thẳng đến menu — điều này hoàn toàn không làm được với `<div>`. Tuy nhiên, `<div>` vẫn hoàn toàn phù hợp khi cần nhóm phần tử để áp dụng CSS mà không có thẻ semantic nào phù hợp hơn, ví dụ `<div class="card-grid">` để tạo layout grid. Tóm lại, học thêm khoảng 10 thẻ semantic không tốn nhiều thời gian, nhưng lợi ích mang lại cho SEO, accessibility và khả năng đọc code là rất đáng giá.

# PHẦN D — VIDEO THỰC HÀNH OBS

- Link video PBT_01: https://www.youtube.com/watch?v=ZQZOHgTcCn0
