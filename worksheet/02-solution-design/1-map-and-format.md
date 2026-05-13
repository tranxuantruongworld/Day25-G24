---
artifact: 1 — FINAL kế hoạch giải pháp
bai-tap: 2 — Thiết kế giải pháp
phase: Chọn rủi ro + chọn tầng + chọn demo + chốt 3 lớp giải pháp
time: 11:00-11:55
input: 00-context.md + 01-test-set-review/3-FINAL-test-set-eval-plan.md
nop-cuoi: Có — file cuối Bài 2
---

# 1 — FINAL: Kế hoạch giải pháp

File này ghi lại quyết định chính của Bài 2:

- Rủi ro nào được chọn.
- Vì sao rủi ro đó quan trọng.
- Nguyên nhân gốc là gì.
- Nhóm sẽ xây 3 lớp giải pháp nào.
- Mỗi lớp dùng demo gì.

Lý do cần 3 lớp: một giải pháp đơn lẻ dễ lọt lỗi. Với rủi ro nặng, nhóm cần nhiều lớp cùng đỡ: lớp này ngăn, lớp kia phát hiện, lớp khác khắc phục hoặc thông báo cho người dùng.

Ba lớp giải pháp nằm trong thư mục `artifact/`:

| Lớp | Thư mục | Vai trò |
|---|---|---|
| Giao diện | `artifact/1-uiux/` | Cảnh báo, dẫn nguồn, nút chuyển sang người thật |
| Chỉ dẫn AI | `artifact/2-prompt/` | Hỏi lại, từ chối, bắt buộc dẫn nguồn |
| Kiến trúc dữ liệu | `artifact/3-architecture/` | Tra cứu nguồn đúng, lưu tạm dữ liệu, xử lý khi thiếu nguồn, giám sát |

Ba lớp này bổ sung cho nhau. Nếu một lớp lọt lỗi, lớp khác vẫn có thể chặn hoặc giảm hại.

## Thông tin nhóm

- **Chủ đề**: Track 2 — Trợ lý đặt vé và chăm sóc khách hàng hàng không
- **Thành viên**: Nguyễn Tuấn Khải (2A202600231), Trần Xuân Trường (2A202600321), Lê Hoàng Long (2A202600095)
- **Ngày**: 2026-05-13

---

## Phần A — Chọn rủi ro và tầng giải pháp

### Rủi ro chính được chọn

- **ID tình huống**: T-11
- **Mô tả ngắn**: Khi người dùng hỏi lời khuyên y tế trên máy bay (ví dụ: bị sốc phản vệ) hoặc hỏi về vật phẩm nguy hiểm (như pin sạc 50.000mAh), AI có xu hướng tự đưa ra lời khuyên hoặc đồng ý cho mang lên máy bay, gây nguy hiểm đến tính mạng, sức khỏe và an toàn bay.
- **Mức độ**: Nặng
- **Điểm rủi ro**: 25
- **Vì sao chọn tình huống này**: Đây là nhóm rủi ro safety-critical có điểm cao nhất (25). Hậu quả liên quan đến sức khỏe con người và an toàn bay là vô cùng nghiêm trọng, không thể đảo ngược, lớn hơn hẳn các lỗi trải nghiệm thông thường.

### Tìm nguyên nhân gốc

Đừng chỉ mô tả lỗi. Hãy trả lời: vì sao lỗi xảy ra?

- [x] Thiếu nguồn dữ liệu đúng. (AI không được nạp hoặc không ưu tiên các rule an toàn bay nghiêm ngặt/quy trình cấp cứu y tế)
- [x] AI đoán khi không biết. (AI tự suy diễn lời khuyên y tế thay vì từ chối)
- [ ] Giao diện khiến người dùng tin quá mức.
- [x] Quy trình thiếu người duyệt hoặc thiếu bước chuyển sang người thật. (Không có bước báo động khẩn cấp cho tổ bay/nhân viên mặt đất)
- [ ] Không có theo dõi sau khi ra mắt.
- [ ] Khác: [...]

### Bảng nối nguyên nhân với tầng sửa

| Nguyên nhân gốc | Tầng ưu tiên sửa | Lớp giải pháp liên quan |
|---|---|---|
| Thiếu nguồn đúng | Dữ liệu / tra cứu nguồn (RAG) / chính sách nguồn | `3-architecture` là chính |
| AI đoán bừa | Chỉ dẫn hệ thống / quy tắc từ chối / dẫn nguồn | `2-prompt` là chính |
| Người dùng tin quá mức | Giao diện cảnh báo / cách viết mức tin cậy | `1-uiux` là chính |
| Tình huống nhạy cảm | Người duyệt / chuyển sang người thật | `1-uiux` + `2-prompt` + `3-architecture` |
| Lỗi lặp lại sau khi ra mắt | Theo dõi / vòng phản hồi | `3-architecture` là chính |

Nguyên tắc: lỗi ở tầng nào, ưu tiên sửa ở tầng đó. Đừng chỉ thêm cảnh báo giao diện nếu nguyên nhân gốc là thiếu nguồn dữ liệu hoặc AI đoán khi không biết.

### 10 tầng giải pháp tham khảo

Không bắt buộc dùng đủ 10 tầng. Bảng này giúp nhóm chọn đúng hướng sửa.

| Tầng | Khi nào dùng |
|---|---|
| Giao diện | Người dùng tin AI quá mức, thiếu cảnh báo, thiếu nguồn, thiếu nút chuyển sang người thật |
| Chỉ dẫn AI | AI đoán khi không biết, không hỏi lại, không từ chối |
| Quy trình xử lý | Cần phân loại ý định, chuyển đúng nơi xử lý, có cách xử lý khi AI không nên trả lời |
| Dữ liệu / tra cứu nguồn (RAG) | Thiếu nguồn đúng, nguồn cũ, AI không dựa vào nguồn đáng tin cậy |
| Theo dõi | Lỗi lặp lại sau khi ra mắt nhưng không ai thấy |
| Chính sách / thông báo giới hạn | Người dùng không biết giới hạn của AI |
| Người duyệt / phê duyệt | Tình huống pháp lý, y tế, tài chính, tuyển dụng, hoặc tác động lớn |
| Vai trò trách nhiệm | Có cảnh báo nhưng không ai chịu trách nhiệm xử lý |
| Vòng phản hồi | Cần người dùng / người rà báo lỗi để cập nhật hệ thống |
| Kiến trúc lai | LLM một mình không đủ, cần rule, classifier, hoặc nhiều bước kiểm tra |

### 4 hành động phòng vệ

Mỗi lớp nên làm ít nhất một việc:

- **Ngăn**: giảm khả năng lỗi xảy ra từ đầu.
- **Phát hiện**: nhận ra lỗi hoặc tín hiệu nguy hiểm.
- **Khắc phục**: chuyển sang người thật, dùng câu trả lời dự phòng, hoặc dừng trả lời.
- **Thông báo**: giúp người dùng hiểu mức tin cậy và rủi ro.

Gợi ý theo mức rủi ro:

| Mức rủi ro | Nên có |
|---|---|
| Nhẹ | Ít nhất 1 hành động |
| Vừa | Ít nhất 2 hành động |
| Nặng | Ít nhất 3 hành động |
| Rất nặng / không đảo ngược được | Cố gắng đủ 4 hành động + có người chịu trách nhiệm |

### Kết luận Phần A

**Nguyên nhân gốc**: Hệ thống AI thiếu cơ chế bắt buộc từ chối (hard-rejection) đối với các chủ đề y tế/an toàn bay, dẫn đến việc AI tự suy diễn lời khuyên có hại. Đồng thời thiếu quy trình báo động khẩn cấp.

**Tầng chính cần sửa**: Chỉ dẫn AI (quy tắc từ chối/hỏi lại) và Giao diện (cảnh báo nguy hiểm, nút liên hệ khẩn cấp).

**Vì sao cần 3 lớp giải pháp**:

- Lớp giao diện: Cần hiển thị cảnh báo đỏ và hướng dẫn gọi cấp cứu/báo tiếp viên ngay lập tức thay vì để người dùng đọc text của AI.
- Lớp chỉ dẫn AI: Cần guardrails nghiêm ngặt yêu cầu AI TỪ CHỐI đưa ra lời khuyên y tế hoặc quyết định an toàn bay, trả về thông báo từ chối chuẩn mực.
- Lớp kiến trúc dữ liệu: Cần bộ lọc từ khóa/Intent Classifier nhạy cảm với các cụm từ "sốc phản vệ", "pin", "cháy nổ" để chặn luồng sinh chữ của LLM và kích hoạt luồng cảnh báo khẩn cấp.

---

## Phần B — Chọn định dạng demo

Mỗi lớp cần một bản demo. Demo giúp biến ý tưởng thành thứ trực quan để nhóm khác xem, kiểm tra và phản biện.

| Lớp | Thư mục | Định dạng demo chọn | Thời gian dự kiến |
|---|---|---|---|
| Giao diện | `1-uiux` | HTML / CSS UI Component | 15 phút |
| Chỉ dẫn AI | `2-prompt` | Bản prompt trong Markdown + ví dụ | 15 phút |
| Kiến trúc dữ liệu | `3-architecture` | Mermaid diagram sơ đồ hộp-mũi tên | 15 phút |

**Lý do chọn demo**

- Giao diện: HTML/CSS giúp trực quan hóa được màu sắc cảnh báo (đỏ/vàng) và nút "Gọi cấp cứu/Báo tiếp viên" hiển thị đè lên khung chat.
- Chỉ dẫn AI: Bản prompt Markdown cho thấy rõ các rule hard-rejection và câu trả lời mẫu an toàn bắt buộc AI phải học thuộc.
- Kiến trúc dữ liệu: Sơ đồ Mermaid mô tả rõ cách hệ thống chặn câu hỏi nhạy cảm trước khi gọi đến LLM và luồng xử lý an toàn.

Gợi ý: có thể dùng AI để dựng nhanh bản nháp demo, nhưng nhóm phải đọc lại và sửa.

### Chọn demo theo điều cần chứng minh

| Nếu cần chứng minh... | Demo phù hợp |
|---|---|
| Người dùng nhìn thấy gì | Sketch, Figma, HTML, ASCII UI |
| AI được chỉ dẫn thế nào | Bản prompt trong Markdown, ví dụ trả lời |
| Dữ liệu đi qua đâu | Sơ đồ hộp-mũi tên, ASCII, Mermaid |
| Quy trình chuyển sang người thật | Sơ đồ quy trình |

---

## Phần C — Ba lớp giải pháp

Ghi tóm tắt ở đây. Chi tiết nằm trong `card.md` và `demo.*` của từng thư mục.

### Lớp 1 — Giao diện (`artifact/1-uiux/`)

- **Cách tiếp cận**: Ngay khi nhận diện ý định liên quan đến an toàn tính mạng/bay, khóa khung chat, hiển thị cảnh báo đỏ rực yêu cầu báo ngay cho tiếp viên hoặc gọi cấp cứu.
- **Hành động phòng vệ bao phủ**: Ngăn / Thông báo
- **Demo**: HTML/CSS UI Component
- **Trạng thái**: Đang làm

Link chi tiết:

- `artifact/1-uiux/card.md`
- `artifact/1-uiux/demo.*`

### Lớp 2 — Chỉ dẫn AI (`artifact/2-prompt/`)

- **Cách tiếp cận**: Thiết lập System Prompt Guardrails cứng: "Nếu người dùng hỏi về y tế/cấp cứu hoặc vật phẩm nguy hiểm, tuyệt đối không suy diễn. Phải trả lời: 'Tôi không thể tư vấn y tế/an toàn. Vui lòng liên hệ nhân viên hoặc báo tiếp viên ngay lập tức!'".
- **Hành động phòng vệ bao phủ**: Ngăn / Từ chối
- **Demo**: Markdown bản prompt và test case
- **Trạng thái**: Đang làm

Link chi tiết:

- `artifact/2-prompt/card.md`
- `artifact/2-prompt/demo.md`

### Lớp 3 — Kiến trúc dữ liệu (`artifact/3-architecture/`)

- **Cách tiếp cận**: Xây dựng bộ Safety Classifier (Keyword/ML) ở lớp ngoài cùng. Nếu match chủ đề y tế/cháy nổ, hệ thống trả luôn predefined response và trigger hệ thống cảnh báo mặt đất/trên không thay vì gọi vào LLM.
- **Hành động phòng vệ bao phủ**: Phát hiện / Ngăn
- **Demo**: Sơ đồ Mermaid luồng kiến trúc
- **Trạng thái**: Đang làm

Link chi tiết:

- `artifact/3-architecture/card.md`
- `artifact/3-architecture/demo.md`

---

## Tổng kiểm tra

| Câu hỏi | Trả lời |
|---|---|
| Rủi ro chính đã chọn là gì? | T-11 — Lời khuyên y tế/Vật phẩm nguy hiểm |
| Nguyên nhân gốc là gì? | AI tự suy diễn khuyên bậy do thiếu cơ chế hard-rejection và luồng báo động khẩn cấp. |
| 3 lớp giải pháp đã đủ chưa? | Giao diện: Cảnh báo đỏ / Chỉ dẫn AI: Guardrail từ chối / Kiến trúc: Safety Classifier |
| 4 hành động đã bao phủ chưa? | Ngăn: Có / Phát hiện: Có / Khắc phục: Có / Thông báo: Có |
| Nhóm khác đã góp ý chưa? | Chưa |
| Nhóm đã sửa gì sau phản biện? | Chưa |

## Phản biện chéo: 4 câu phải trả lời

Khi nhóm khác góp ý, hoặc khi nhóm tự rà lại, dùng 4 câu này:

| Góc phản biện | Câu hỏi |
|---|---|
| Đúng tầng | Giải pháp có sửa đúng nguyên nhân gốc không? |
| Cụ thể | Demo có đủ rõ để hiểu cách vận hành không? |
| Đủ lớp | 3 lớp có bổ sung cho nhau không, hay đang lặp cùng một ý? |
| Tác dụng phụ | Giải pháp có làm chậm, tốn kém, rối giao diện, hoặc gây hiểu nhầm mới không? |

Ghi góp ý cụ thể vào `card.md` hoặc phần tổng kiểm tra. Không ghi chung chung "ổn" hoặc "chưa ổn".

## Gợi ý chia việc

Nhóm 3 người:

- Thành viên A: `artifact/1-uiux/`
- Thành viên B: `artifact/2-prompt/`
- Thành viên C: `artifact/3-architecture/`

Nhóm 2 người:

- Một người phụ trách 2 lớp.
- Người còn lại phụ trách 1 lớp và rà lại 2 lớp kia.

5 phút cuối: cả nhóm đọc chéo 3 lớp, sửa lại bảng tổng kiểm tra, rồi chuẩn bị phản biện chéo.
