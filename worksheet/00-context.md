---
title: 00 — Bối cảnh sản phẩm của nhóm
section: Day 25 — dùng lại cho mọi cuộc trò chuyện với AI
format: Nhóm
time: Điền 5 phút đầu buổi
---

# 00-context.md — Bối cảnh sản phẩm của nhóm

Điền file này một lần ở đầu buổi. Sau đó, mỗi lần dùng AI, hãy đưa toàn bộ nội dung file này vào đầu cuộc trò chuyện.

Lý do: AI không tự nhớ bối cảnh giữa các cuộc trò chuyện. Nếu mỗi lần đưa bối cảnh khác nhau, câu trả lời cũng sẽ lệch.

---

## 1. Sản phẩm

- **Tên sản phẩm / bot**: Trợ lý AI đặt vé và chăm sóc khách hàng hàng không
- **Sản phẩm giúp ai làm gì**: Hỗ trợ khách hàng tìm kiếm thông tin chuyến bay, tư vấn giá vé, thực hiện quy trình đặt chỗ và giải đáp các thắc mắc về chính sách hàng không nhằm giảm tải cho đội ngũ CSHK.
- **Người dùng gặp sản phẩm ở đâu**: Trang web chính thức của hãng hàng không.
- **Giai đoạn hiện tại**: Đang thử nghiệm và đánh giá an toàn (Pre-launch/Testing).

---

## 2. Phạm vi

**AI được làm gì**

- Tra cứu và cung cấp thông tin chuyến bay, lịch trình, giá vé từ cơ sở dữ liệu chính thức.
- Hỗ trợ các bước trong quy trình đặt vé trực tuyến.
- Giải đáp các câu hỏi thường gặp (FAQ) về hành lý, thủ tục check-in, và chính sách chung.

**AI không được làm gì**

- Không được bịa đặt hoặc xác nhận các chuyến bay/lịch trình không tồn tại (Hallucination).
- Không được tự ý đưa ra các cam kết bồi thường hoặc giảm giá nằm ngoài chính sách chính thức (Sycophancy).
- Không được xử lý các trường hợp khiếu nại gay gắt hoặc yêu cầu pháp lý mà không có sự giám sát của con người (Escalation failure).

**Vì sao có giới hạn này**

Tránh rủi ro pháp lý và trách nhiệm bồi thường (như trường hợp Air Canada), bảo vệ uy tín thương hiệu và đảm bảo khách hàng không bị lỡ kế hoạch di chuyển do thông tin sai lệch.

---

## 3. Người dùng

- **Là ai**: Khách hàng có nhu cầu đặt vé máy bay hoặc cần hỗ trợ thông tin, đa dạng về độ tuổi và trình độ công nghệ.
- **Họ hỏi AI khi nào**: Trước khi đặt vé (tra cứu), trong khi đặt (hỗ trợ kỹ thuật) hoặc sau khi đặt (khiếu nại, thay đổi lịch trình).
- **Họ cần quyết định gì sau khi hỏi AI**: Quyết định thanh toán đặt chỗ, tin tưởng vào các thông tin bồi thường để sắp xếp công việc cá nhân.
- **Khi nào họ dễ bị tổn thương / dễ hiểu sai**: Khi đang trong trạng thái khẩn cấp (bay gấp, sự cố tang gia), hoặc khi AI sử dụng ngôn ngữ quá khẳng định về các thông tin ảo.
- **Họ thường tin AI đến mức nào**: Có xu hướng tin tưởng cao vào các xác nhận từ chatbot trên trang web chính thức (Over-reliance).

---

## 4. Bối cảnh ngành

- **Sự cố tương tự đã từng xảy ra**: Vụ việc chatbot của Air Canada cung cấp sai chính sách giảm giá dẫn đến việc hãng bay phải bồi thường theo thông tin sai lệch đó.
- **Quy định hoặc ràng buộc liên quan**: Quy định của ngành hàng không về tính minh bạch thông tin và luật bảo vệ quyền lợi người tiêu dùng.
- **Nguồn chính thức nên ưu tiên**: Hệ thống quản lý chuyến bay (Booking System), tài liệu chính sách bồi thường và điều khoản dịch vụ (TOS) của hãng.

---

## 5. Ghi chú thêm

- Ưu tiên hàng đầu: Đối soát dữ liệu thực tế trước khi phản hồi (RAG integrity).
- Cơ chế Fallback: Luôn cung cấp tùy chọn gặp nhân viên thật khi AI không chắc chắn hoặc khi người dùng có thái độ tiêu cực.
- Ví dụ câu hỏi nhạy cảm: Đặt vé vào các ngày không tồn tại (30/02) hoặc hỏi về các đường bay hãng chưa khai thác.

---

## Cách dùng

```text
1. Mở công cụ AI phù hợp với bước đang làm.
2. Đưa toàn bộ nội dung file này vào đầu cuộc trò chuyện.
3. Chọn prompt tham khảo từ thư mục ../prompts/ và chỉnh lại nếu cần.
4. Đọc lại bản nháp AI tạo ra.
5. Sửa lại cho đúng bối cảnh nhóm.
6. Lưu kết quả vào đúng file trong worksheet/.
```

Ghi chú: nội dung trong `[...]` là chỗ cần điền. Sau khi điền xong, xóa dấu ngoặc nếu không cần giữ.
