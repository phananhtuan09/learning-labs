# Mini-project: Giữ hàng khi checkout

3 buổi × 45 phút, chế độ challenge.
Backend API, client FE mỏng, tích hợp cổng thanh toán bên thứ 3 ở chế độ sandbox, và script mô phỏng.

> **Cách đọc file này**
>
> - `✏️ BẠN QUYẾT ĐỊNH`: chỗ bạn phải tự chọn và ghi lý do; spec cố ý không có đáp án.
> - `✂️ BẠN CÓ THỂ ĐỔI`: bạn được giữ, cắt hoặc sửa, nhưng phải ghi rõ đổi gì và vì sao trong phần quyết định.
> - Không có ký hiệu: phần cố định dùng để review; muốn đổi thì nói với stakeholder trước.
> - Phần cần điền nằm ở mục **Quyết định của bạn (tự điền)** cuối file.

## Vấn đề

Một shop nhỏ bán hàng theo đợt, mỗi đợt số lượng ít, ví dụ 20 đơn vị, và thường hết trong vài phút đầu.
Cổng thanh toán xác nhận bất đồng bộ, từ vài giây đến vài phút sau khi khách bấm thanh toán, bằng cách gọi một endpoint của shop.
Đợt trước shop bán vượt tồn kho, và có khách bị trừ tiền nhưng không có hàng.

## Người dùng

- Khách mua hàng qua web frontend của shop trong một đợt mở bán.
- Chủ shop: không được bán vượt và không được thu tiền cho món không giao được.

## Yêu cầu chức năng

1. Khách giữ được một hoặc nhiều đơn vị của một sản phẩm trong một khoảng thời gian để thanh toán.
   `✏️ BẠN QUYẾT ĐỊNH`: giữ bao lâu, và điều gì quyết định con số đó.
2. Cổng thanh toán bên thứ 3 báo thành công hoặc thất bại cho thanh toán của một hold; thanh toán thành công biến hold thành đơn hàng.
3. Client FE biết kết quả cuối của khách mà không cần reload thủ công.
   `✏️ BẠN QUYẾT ĐỊNH`: client biết kết quả bằng cách nào, và cách đó tốn gì cho server trong một đợt mở bán.
4. Hold không được thanh toán kịp thì trả hàng lại cho khách khác.
5. Quy định chuyện gì xảy ra khi kết quả thanh toán đến sau khi hold đã hết hạn.
   `✏️ BẠN QUYẾT ĐỊNH`: kết quả cuối là gì, và khách thấy gì.

## Tiêu chí chấp nhận

- Khi mô phỏng nhiều khách cùng tranh những đơn vị cuối, số đơn được xác nhận không bao giờ vượt tồn kho.
- Khách luôn kết thúc với một kết quả nhìn thấy được ở client: đơn đã xác nhận, thanh toán thất bại, hold hết hạn, cộng với kết quả nào chính sách của bạn thêm vào.
- Hàng của hold hết hạn hoặc thất bại quay lại cho khách khác mua được.
- Chính sách bạn viết liệt kê các tình huống đã dùng để kiểm tra, và trong mỗi tình huống khách thấy gì.

## Ràng buộc

- Chạy local, trừ cổng thanh toán: dùng một cổng thanh toán bên thứ 3 ở chế độ sandbox hoặc test mode miễn phí.
  Dùng cổng nào là do bạn chọn.
- Ngôn ngữ, framework và storage của backend do bạn chọn.
  `✏️ BẠN QUYẾT ĐỊNH`: lý do chọn storage, gắn với yêu cầu chống bán vượt khi tranh chấp.
- Client FE chỉ là client mỏng để chạy luồng thật; giao diện không được chấm.
  Phần được đánh giá là tích hợp giữa FE và API.
- Client FE có ba màn hình cho khách:
  1. Trang đợt mở bán: thông tin sản phẩm, còn hàng hay hết, nút giữ hàng kèm số lượng.
  2. Trang checkout: hold đang có và thời gian còn lại, nút thanh toán.
  3. Trang kết quả: chờ và hiện kết quả cuối của khách.
- Kết quả thanh toán như thành công, thất bại hay chậm được tạo bằng công cụ sandbox của cổng, ví dụ thẻ test hoặc CLI của họ.
- Bạn tự viết chính sách trước khi giao code cho coding agent.
  Có thể viết dưới dạng ghi chú chính sách, decision record hoặc plan, miễn bằng lời của bạn và nói rõ khách thấy gì và vì sao.
  Khi giao task, ghi rõ chính sách đó để agent làm theo, không để agent tự chọn.

## Không làm

`✂️ BẠN CÓ THỂ ĐỔI`: muốn bỏ thêm hoặc kéo một mục vào scope thì ghi lý do; mục cố ý để ngoài scope cũng là một phần checklist khi nộp.

- Tài khoản người dùng, đăng nhập hoặc hệ thống xác thực đầy đủ.
- Quản lý danh mục sản phẩm hoặc màn hình admin.
- Thanh toán live bằng tiền thật, hoàn tiền thật, hoặc giao hàng.
- Review giao diện, responsive hay accessibility của FE.
- Deploy production hoặc scale ngang nhiều máy.

## Sản phẩm bàn giao

- Một repo gồm chính sách bạn viết, API, phần tích hợp cổng thanh toán sandbox, client FE mỏng và script mô phỏng tranh chấp.
- Demo từng tình huống ghi trong chính sách, kèm kết quả của script mô phỏng.

## Định nghĩa hoàn thành

- Chính sách vòng đời hold và tích hợp do bạn viết bằng lời của mình nằm trong folder project, liệt kê tình huống đã kiểm và khách thấy gì trong từng tình huống, và được commit trước khi coding agent implement.
- Khách giữ hàng qua client FE, thanh toán qua sandbox của cổng thanh toán, và thấy kết quả cuối trong client mà không reload trang.
- Script mô phỏng cho nhiều khách tranh những đơn vị cuối và không bao giờ bán vượt tồn kho.
- Hold không thanh toán kịp thì trả hàng; thanh toán đến sau khi hold hết hạn kết thúc đúng như chính sách quy định và khách thấy được.
- API và client khởi động local bằng lệnh được ghi lại, kèm cách cấu hình sandbox của cổng và cách kết quả thanh toán về tới API.

## Quyết định của bạn

Vòng đời của hold: thời hạn, các trạng thái, và trạng thái kết thúc.
Cách chống bán vượt khi nhiều khách tranh món cuối.
Thanh toán đến muộn xử lý thế nào.
Client FE biết kết quả bằng cách nào.

## Câu hỏi mở

- Hold nên kéo dài bao lâu, và điều gì quyết định con số đó?
- Client biết kết quả thanh toán bằng cách nào, và cách đó tốn gì cho server trong một đợt mở bán?
- Một thanh toán thành công sau khi hold đã hết hạn thì sao?

## Các mốc

- Buổi 1: liệt kê tình huống của khách và của thanh toán, quyết định vòng đời hold và cách client nhận kết quả, viết và commit chính sách trước khi giao code.
- Buổi 2: implement endpoint giữ hàng, nhận kết quả thanh toán và trạng thái, tích hợp sandbox của cổng thanh toán, và luồng client mỏng.
- Buổi 3: chạy mô phỏng tranh chấp, demo từng tình huống trong chính sách, rồi nộp bài.

Spec này cố ý chưa đầy đủ.
Hiểu đúng điều khách và chủ shop thật sự cần, nhất là ở chỗ FE tích hợp với API, là một phần của bài.
Bạn có thể hỏi stakeholder bất cứ lúc nào.

## Quyết định của bạn (tự điền)

Viết bằng lời của bạn, commit phần này trước khi giao code cho coding agent.
Mỗi chỗ trống một hai câu là đủ; phần "vì sao" là phần được chấm, không phải độ dài.

### Vòng đời hold

- Thời hạn hold là: ___ vì ___
- Các trạng thái và trạng thái kết thúc: ___
- Cách chống bán vượt khi tranh món cuối: ___ vì ___
- Storage chọn: ___ vì ___

### Tích hợp FE và API

- Client biết kết quả bằng cách: ___ vì ___
- Điều bạn lo nhất khi FE gọi API, và cách bạn xử lý: ___

### Tình huống và kết quả

| Tình huống | Khách thấy gì | Hệ thống làm gì | Vì sao |
|---|---|---|---|
| Hai khách cùng giữ đơn vị cuối | ___ | ___ | ___ |
| Thanh toán thành công trong thời hạn | ___ | ___ | ___ |
| Thanh toán thất bại | ___ | ___ | ___ |
| Hold hết hạn trước khi thanh toán | ___ | ___ | ___ |
| Thanh toán thành công sau khi hold hết hạn | ___ | ___ | ___ |
| Tình huống khác bạn tự thêm | ___ | ___ | ___ |

### Lựa chọn và đánh đổi

- Điều bạn chấp nhận hy sinh với lựa chọn này: ___

### Thay đổi scope (nếu có)

- Bạn đổi, cắt hoặc thêm gì so với spec: ___
- Vì sao: ___

### Còn chưa chắc

- ___

## Checklist khi nộp

- Đường dẫn folder, commit, và cách chạy demo.
- Các quyết định chính và lý do, nhất là vòng đời hold và cách client nhận kết quả.
- Giả định và những chỗ bạn còn chưa chắc.
- Góc nhìn sản phẩm: giúp ai, thế nào là thành công, và một thứ cố ý để ngoài scope kèm lý do.
- AI hoặc nguồn ngoài nào đã tác động tới phần nào; nói rõ phần nào bạn tự viết.
- Tùy chọn: tài liệu bạn tự viết và muốn được đọc.
