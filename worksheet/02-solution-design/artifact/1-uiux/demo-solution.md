### Ý tưởng 1: Emergency Modal Overlap (Cửa sổ bật lên chặn màn hình)

**Bối cảnh:** Dùng cho các tình huống đe dọa tính mạng ngay lập tức (như sốc phản vệ, co giật, khó thở).
**Cơ chế:** Khi AI phát hiện từ khóa y tế khẩn cấp, nó lập tức khóa khung chat (làm mờ phía sau) và hiển thị một Popup màu đỏ rực ở giữa màn hình. Người dùng bắt buộc phải tương tác với các nút khẩn cấp, ngăn họ tiếp tục nhắn tin vòng vo với Bot.

```text
+---------------------------------------+
|  < Trợ lý Hàng Không              (i) |
+---------------------------------------+
| [User]: Tôi đang bị khó thở, hình như |
|         bị sốc phản vệ, có thuốc gì   |
|         uống được không?              |
|                                       |
| ▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒ |
| ▒ +-------------------------------+ ▒ |
| ▒ | [!] CẢNH BÁO Y TẾ KHẨN CẤP    | ▒ |
| ▒ |                               | ▒ |
| ▒ | Tôi không thể tư vấn y tế.    | ▒ |
| ▒ | Tình trạng của bạn cần được   | ▒ |
| ▒ | cấp cứu ngay lập tức!         | ▒ |
| ▒ |                               | ▒ |
| ▒ | Hãy nhấn chuông gọi tiếp viên | ▒ |
| ▒ | hoặc liên hệ nhân viên y tế!  | ▒ |
| ▒ |                               | ▒ |
| ▒ |   [ 🆘 BÁO ĐỘNG TỚI TỔ BAY ]  | ▒ |
| ▒ |   [ 📞 GỌI CẤP CỨU SÂN BAY ]  | ▒ |
| ▒ +-------------------------------+ ▒ |
| ▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒ |
+---------------------------------------+
| (Khung chat bị khóa tạm thời...)      |
+---------------------------------------+
```

### Ý tưởng 2: Inline Red Alert Message (Tin nhắn đỏ cảnh báo trong chat)

**Bối cảnh:** Dùng cho các câu hỏi về vật phẩm nguy hiểm, rủi ro an toàn bay (như mang pin 50.000mAh, hóa chất).
**Cơ chế:** Chatbot trả về câu trả lời nhưng giao diện tin nhắn của Bot được đổi sang style Cảnh báo (Viền đỏ/vàng, icon ⚠️), tách biệt hoàn toàn với màu bong bóng chat thông thường. Đi kèm bên dưới là các nút Call-to-Action (CTA) để chuyển hướng người dùng sang kênh xác minh chính thức.

```text
+---------------------------------------+
|  < Trợ lý Hàng Không              (i) |
+---------------------------------------+
| [User]: Mình mang pin dự phòng 50.000 |
|         mAh lên máy bay được không?   |
|                                       |
| [Bot]:                                |
| ------------------------------------- |
| | ⚠️ TỪ CHỐI TƯ VẤN AN TOÀN BỘ    | |
| | Tôi không thể tư vấn hay xác nhận | |
| | về vật phẩm nguy hiểm. Việc mang  | |
| | pin sai quy định có thể gây ra    | |
| | cháy nổ nghiêm trọng.             | |
| |                                   | |
| | Vui lòng liên hệ nhân viên ngay!  | |
| ------------------------------------- |
|                                       |
|   [ 📞 Gọi Nhân viên Mặt đất ]        |
|   [ 📖 Xem Danh mục Hàng Cấm ]        |
+---------------------------------------+
| Nhập tin nhắn...                  [>] |
+---------------------------------------+
```

### Ý tưởng 3: Chat Lockout & Handoff (Khóa chat và tự động kết nối người thật)

**Bối cảnh:** Dùng khi rủi ro ở mức độ cực cao và người dùng tỏ ra hoảng loạn (ví dụ: cấp cứu y tế mà user không biết làm gì).
**Cơ chế:** AI tung ra câu trả lời từ chối theo Guardrails, đồng thời tự động trigger một API kết nối tới Live Agent (Nhân viên y tế trực tuyến). Bàn phím chat biến mất, thay bằng thanh trạng thái hiển thị tiến trình kết nối.

```text
+---------------------------------------+
|  < Trợ lý Hàng Không              (i) |
+---------------------------------------+
| [User]: Trẻ nhỏ đi cùng tôi đang bị   |
|         co giật liên tục, làm sao đây?|
|                                       |
| [Bot]:                                |
| ------------------------------------- |
| | 🚨 YÊU CẦU HỖ TRỢ TRỰC TIẾP     | |
| | Tôi không thể cung cấp hướng dẫn  | |
| | sơ cứu. Xin giữ bình tĩnh!        | |
| | Hệ thống đang kết nối khẩn cấp    | |
| | bạn với bộ phận Y tế mặt đất!     | |
| ------------------------------------- |
|                                       |
|  >> ⏳ Đang kết nối với Nhân viên... |
+---------------------------------------+
|  [ ✖️ Hủy kết nối ] [ 📞 Gọi 115 ]    |
+---------------------------------------+
```
