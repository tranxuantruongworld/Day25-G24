---
artifact: 3 — Demo kiến trúc dữ liệu
format: sơ đồ xử lý + bảng thành phần
---

# demo.md — Demo kiến trúc dữ liệu

File này dùng để đặt sơ đồ và mô tả ngắn cách hệ thống giảm rủi ro.

---

## 1. Sơ đồ cách hệ thống xử lý

```mermaid
graph TD
    A[Người dùng gửi tin nhắn] --> B{Safety & Intent Classifier}
    
    B -- "Y tế khẩn cấp\n(sốc phản vệ, co giật...)" --> C[Chặn luồng LLM]
    B -- "Vật phẩm nguy hiểm\n(pin >20000mAh, cháy nổ)" --> D[Chặn luồng LLM]
    B -- "Câu hỏi bình thường" --> E[Truy vấn LLM & RAG]
    
    C --> F[Sinh mã `[SYS_MEDICAL_EMERGENCY]`]
    D --> G[Sinh mã `[SYS_DANGEROUS_GOODS]`]
    
    F --> H[Trigger API Báo động tới Y tế/Tổ bay]
    G --> I[Trigger API Cảnh báo An ninh mặt đất]
    
    H --> J[Frontend Khóa chat & Bật Popup Đỏ]
    I --> K[Frontend Đổi màu Tin nhắn & Hiện Nút gọi]
    E --> L[Frontend Hiển thị tin nhắn như bình thường]
```

---

## 2. Thành phần chính

| Thành phần | Nhận gì? | Làm gì? | Trả ra gì? |
|---|---|---|---|
| **Safety Classifier (Lọc độc lập)** | Câu hỏi của người dùng | Quét từ khóa/Intent nhạy cảm về y tế, vũ khí, cháy nổ trước khi cho phép gọi LLM. | Lệnh đi tiếp vào LLM hoặc Lệnh Chặn khẩn cấp. |
| **API Báo động Khẩn cấp** | Mã trạng thái `[SYS_MEDICAL_EMERGENCY]` | Gọi Webhook/WebSocket đẩy cảnh báo ưu tiên cao nhất lên màn hình của Tiếp viên trưởng hoặc bộ phận Y tế. | Tín hiệu báo động đã được gửi đi. |
| **Hệ thống LLM & Prompt Guardrails** | Câu hỏi bình thường | Trích xuất thông tin, tư vấn chính sách thông thường và tuyệt đối tuân thủ Guardrails (không tự khuyên y tế). | Câu trả lời văn bản. |
| **Hệ thống Logging An toàn** | Câu hỏi bị chặn & Lịch sử API | Lưu lại các trường hợp người dùng nhập từ khóa nguy hiểm để phân tích và điều tra sau chuyến bay (nếu cần). | Báo cáo tần suất cảnh báo giả/thật. |

---

## 3. Khi hệ thống gặp vấn đề

| Khi nào lỗi xảy ra? | Hệ thống làm gì? | Người dùng thấy gì? |
|---|---|---|
| **Classifier không chắc chắn (Borderline)** | Áp dụng nguyên tắc Fail-Safe (thiên về an toàn). Không gọi LLM, rẽ nhánh báo cáo nhân viên. | "Chúng tôi không thể xác nhận thông tin này qua Chatbot, vui lòng kiểm tra với nhân viên." |
| **API Báo động bị lỗi / mất mạng** | Giao diện Frontend tự nhận diện mã flag nội bộ và yêu cầu người dùng tự hành động thủ công. | Popup hiển thị đỏ: "Vui lòng LA LỚN hoặc NHẤN CHUÔNG GỌI TIẾP VIÊN NGAY LẬP TỨC!" |
| **LLM bị Jailbreak bỏ qua Guardrails** | Có Safety Classifier ở đầu ra (Output Filter) chặn lại các câu chứa từ khóa "Bạn có thể uống thuốc...", "Mang pin lên được...". | Xin lỗi, tôi không thể xử lý yêu cầu này. |
| **User lạm dụng nút báo động (Spam)** | Hệ thống đếm tần suất. Nếu 1 user trigger > 3 lần liên tiếp không có thật, tạm khóa tính năng gọi API nhưng vẫn từ chối tư vấn. | Lời từ chối tư vấn y tế/an toàn như cũ. |

---

## 4. Kiểm tra nhanh

- [x] Sơ đồ không chỉ là “AI trả lời tốt hơn”, mà có bước kiểm tra cụ thể. (Có Safety Classifier độc lập đứng trước LLM).
- [x] Có cách xử lý khi thiếu dữ liệu. (Nguyên lý Fail-Safe: Nghi ngờ là chặn, không đoán).
- [x] Có cách chuyển sang người thật. (Trigger API Báo động tới thiết bị của Tổ bay/Y tế).
- [x] Có cách theo dõi để lần sau sửa tốt hơn. (Logging riêng cho các sự cố kích hoạt cờ Safety).
