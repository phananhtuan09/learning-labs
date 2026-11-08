# Mini-project: Chính sách hiển thị bước đang chạy

2 buổi × 45 phút, chế độ challenge.
Mở rộng plugin `agent-activity` hiện có.

> **Cách đọc file này**
>
> - `✏️ BẠN QUYẾT ĐỊNH`: chỗ bạn phải tự chọn và ghi lý do; spec cố ý không có đáp án.
> - `✂️ BẠN CÓ THỂ ĐỔI`: bạn được giữ, cắt hoặc sửa, nhưng phải ghi rõ đổi gì và vì sao trong phần quyết định.
> - Không có ký hiệu: phần cố định dùng để review; muốn đổi thì nói với stakeholder trước.
> - Phần cần điền nằm ở mục **Quyết định của bạn (tự điền)** cuối file.

## Vấn đề

Ở Brief và Steps, bước đang chạy chỉ hiện chip hoặc dòng có spinner và thời gian chạy.
Khi agent chạy lệnh dài, bạn không biết nó đang tiến triển hay đang kẹt.
Muốn biết thêm thì phải mở body hoặc chuyển sang Full.

## Người dùng

Chính bạn: chủ yếu chạy Claude Code trong Paseo, để ở Brief cho dễ đọc lướt, và cần quyết định nhanh nên để agent chạy tiếp hay dừng nó.

## Bối cảnh hiện tại

- Plugin đã có ba mức Brief, Steps, Full.
  Full mở body khi đang chạy, Brief và Steps giữ thu gọn với spinner và thời gian chạy.
- Bạn dùng Claude Code trên Paseo 0.15.x chạy local.
- Câu trả lời và lỗi của turn giữ cách hiển thị mặc định của Paseo.
- Agent thường chạy test suite, build hoặc cài dependency kéo dài vài phút, và output có thể tiếp tục stream trong lúc chạy.

## Yêu cầu chức năng

1. Quy định bước đang chạy hiển thị gì ở Brief và ở Steps, gồm cả cách báo hiệu công việc đang tiến triển.
   `✏️ BẠN QUYẾT ĐỊNH`: hiển thị gì, Brief và Steps giống hay khác, và vì sao.
2. Quy định bước đang chạy thay đổi thế nào khi xong, lỗi, bị dừng, hoặc chạy lâu bất thường.
   `✏️ BẠN QUYẾT ĐỊNH`: trạng thái cuối trông thế nào; "lâu bất thường" là gì, hoặc vì sao không cần ngưỡng.
3. Làm chính sách đó trong plugin hiện có cho Claude Code, không đổi Full.

## Tiêu chí chấp nhận

- Khi một lệnh chạy vài phút ở Brief, bạn biết nó còn in output hay không mà không cần click.
  `✂️ BẠN CÓ THỂ ĐỔI`: nếu quan sát ở buổi 1 cho thấy plugin không nhận được thông tin này, ghi lại giới hạn đó và tiêu chí bạn thay thế.
- Ở Brief, nhìn qua là thấy bước lỗi, không cần đọc body.
- Ở Brief, một turn đã xong vẫn là danh sách gọn, đọc lướt được.
- Phần chính sách bạn viết liệt kê các tình huống đã dùng để kiểm tra, và trong mỗi tình huống người dùng thấy gì.

## Ràng buộc

- Mở rộng plugin `agent-activity` hiện có, không tạo plugin mới.
- Bạn tự viết chính sách trước khi giao code cho coding agent.
  Có thể viết dưới dạng ghi chú chính sách, decision record hoặc plan, miễn nói rõ người dùng thấy gì và vì sao.
  Khi giao task, ghi rõ chính sách đó để agent làm theo, không để agent tự chọn.
- Chỉ dùng React Native primitives.
- Giữ `requirements.paseo` tương thích Paseo 0.15.x.
- Không cần dịch vụ remote.

## Không làm

`✂️ BẠN CÓ THỂ ĐỔI`: muốn bỏ thêm hoặc kéo một mục vào scope thì ghi lý do; mục cố ý để ngoài scope cũng là một phần checklist khi nộp.

- Hỗ trợ Codex hoặc OMP.
- Card cho câu trả lời hoặc lỗi.
- Phân loại lệnh theo rủi ro.
- Thông báo, âm thanh, hoặc quy tắc làm gián đoạn người dùng.
- Cuộn timeline tới bước đang chạy.
- Màn hình settings ngoài các mức chi tiết đang có.

## Sản phẩm bàn giao

- Một commit trong repo plugin gồm phần chính sách bạn viết và phần implement.
- Demo trên Claude Code cho từng tình huống ghi trong chính sách, ở Brief và Steps.

## Định nghĩa hoàn thành

- Phần chính sách bạn tự viết nằm trong folder plugin, nói rõ người dùng thấy gì trong từng tình huống và vì sao, và được commit trước khi coding agent implement.
- Ở Brief và Steps, bước đang chạy hiện các tín hiệu chính sách quy định, không cần click.
- Bước xong, lỗi hoặc bị dừng chuyển sang trạng thái cuối như chính sách, và nhìn qua là phân biệt được.
- Full giữ nguyên hành vi hiện tại; tắt plugin thì Paseo về cách hiển thị mặc định.
- Plugin cài được trên daemon local và ở trạng thái running, không lỗi.

## Quyết định của bạn

Bước đang chạy hiển thị gì ở Brief và Steps.
Cách phân biệt bước đang tiến triển với bước im lặng.
Thế nào là chạy lâu bất thường.
Trạng thái cuối khi xong, lỗi hoặc bị dừng.

## Câu hỏi mở

- Điều gì cho bạn biết một bước đang tiến triển chứ không bị kẹt?
- Brief và Steps có nên hiển thị bước đang chạy khác nhau không, và vì sao?
- Khi nào một bước được coi là chạy lâu bất thường?

## Các mốc

- Buổi 1: liệt kê các tình huống bạn quan tâm, quan sát Paseo báo gì khi tool đang chạy, rồi viết chính sách trước khi giao code.
- Buổi 2: implement chính sách, demo từng tình huống trên Claude Code, rồi nộp bài.

Spec này cố ý chưa đầy đủ.
Hiểu đúng điều bạn thật sự cần khi theo dõi agent là một phần của bài.
Bạn có thể hỏi stakeholder bất cứ lúc nào.

## Quyết định của bạn (tự điền)

Viết bằng lời của bạn, commit phần này trước khi giao code cho coding agent.
Có thể chép sang folder plugin dưới dạng decision record hoặc plan.
Không cần dài; mỗi chỗ trống một hai câu là đủ.

### Quan sát buổi 1

- Trong lúc lệnh đang chạy, plugin nhận được gì từ Paseo: ___
- Điều này cho phép hoặc không cho phép hiển thị gì: ___

### Tình huống và hiển thị

| Tình huống | Ở Brief bạn muốn thấy | Ở Steps bạn muốn thấy | Vì sao |
|---|---|---|---|
| Lệnh chạy vài phút, có in output | ___ | ___ | ___ |
| Lệnh không in gì một lúc | ___ | ___ | ___ |
| Lệnh chạy lâu hơn bình thường | ___ | ___ | ___ |
| Bước xong | ___ | ___ | ___ |
| Bước lỗi | ___ | ___ | ___ |
| Bạn bấm stop agent | ___ | ___ | ___ |
| Tình huống khác bạn tự thêm | ___ | ___ | ___ |

### Lựa chọn và đánh đổi

- "Lâu bất thường" là: ___ (hoặc vì sao không cần ngưỡng: ___)
- Brief và Steps khác nhau ở: ___ (hoặc vì sao giống nhau: ___)
- Điều bạn chấp nhận hy sinh với lựa chọn này: ___

### Thay đổi scope (nếu có)

- Bạn đổi, cắt hoặc thêm gì so với spec: ___
- Vì sao: ___

### Còn chưa chắc

- ___

## Checklist khi nộp

- Đường dẫn folder, commit, và cách chạy demo.
- Các quyết định chính và lý do, nhất là chính sách hiển thị bước đang chạy.
- Giả định và những chỗ bạn còn chưa chắc.
- Góc nhìn sản phẩm: giúp ai, thế nào là thành công, và một thứ cố ý để ngoài scope kèm lý do.
- AI hoặc nguồn ngoài nào đã tác động tới phần nào.
- Tùy chọn: tài liệu bạn tự viết và muốn được đọc.
