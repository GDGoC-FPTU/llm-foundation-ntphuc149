# Ngày 1 — Bài Tập & Phản Ánh

## Nền Tảng LLM API | Phiếu Thực Hành

**Thời lượng:** 1:30 giờ  
**Cấu trúc:** Lập trình cốt lõi (60 phút) → Bài tập mở rộng (30 phút)

---

## Phần 1 — Lập Trình Cốt Lõi (0:00–1:00)

Chạy các ví dụ trong Google Colab tại: https://colab.research.google.com/drive/172zCiXpLr1FEXMRCAbmZoqTrKiSkUERm?usp=sharing

Triển khai tất cả TODO trong `template.py`. Chạy `pytest tests/` để kiểm tra tiến độ.

**Điểm kiểm tra:** Sau khi hoàn thành 4 nhiệm vụ, chạy:

```bash
python template.py
```

Bạn sẽ thấy output so sánh phản hồi của GPT-4o và GPT-4o-mini.

---

## Phần 2 — Bài Tập Mở Rộng (1:00–1:30)

### Bài tập 2.1 — Độ Nhạy Của Temperature

Gọi `call_openai` với các giá trị temperature 0.0, 0.5, 1.0 và 1.5 sử dụng prompt **"Hãy kể cho tôi một sự thật thú vị về Việt Nam."**

**Bạn nhận thấy quy luật gì qua bốn phản hồi?** (2–3 câu)

> Ở temperature 0.0, phản hồi rất nhất quán và súc tích, tập trung vào một sự thật cụ thể. Khi temperature tăng lên 0.5 và 1.0, câu trả lời trở nên phong phú và đa dạng hơn về từ ngữ. Ở temperature 1.5, phản hồi có xu hướng sáng tạo nhưng đôi khi thiếu tập trung hoặc lặp ý.

**Bạn sẽ đặt temperature bao nhiêu cho chatbot hỗ trợ khách hàng, và tại sao?**

> Nên đặt temperature = 0.2. Chatbot hỗ trợ khách hàng cần câu trả lời chính xác, nhất quán và đáng tin cậy — temperature thấp giúp model bám sát thông tin thực tế, tránh "hallucination" và đảm bảo khách hàng nhận được thông tin đồng nhất qua nhiều lần hỏi.

---

### Bài tập 2.2 — Đánh Đổi Chi Phí

Xem xét kịch bản: 10.000 người dùng hoạt động mỗi ngày, mỗi người thực hiện 3 lần gọi API, mỗi lần trung bình ~350 token.

**Ước tính xem GPT-4o đắt hơn GPT-4o-mini bao nhiêu lần cho workload này:**

> Tổng token/ngày = 10.000 × 3 × 350 = 10.500.000 token. Giả sử input/output = 50/50 (175.000 input + 175.000 output mỗi batch):
>
> - GPT-4o: (5.25M × $5.00 + 5.25M × $20.00) / 1M = **$131.25/ngày**
> - GPT-4o-mini: (5.25M × $0.15 + 5.25M × $0.60) / 1M = **$3.94/ngày**  
>   GPT-4o đắt hơn khoảng **33 lần**.

**Mô tả một trường hợp mà chi phí cao hơn của GPT-4o là xứng đáng, và một trường hợp GPT-4o-mini là lựa chọn tốt hơn:**

> GPT-4o xứng đáng khi cần phân tích văn bản pháp lý hoặc y tế — nơi độ chính xác và khả năng suy luận phức tạp ảnh hưởng trực tiếp đến kết quả quan trọng. GPT-4o-mini phù hợp hơn cho các tác vụ đơn giản như phân loại email, trả lời FAQ, hay tóm tắt nội dung ngắn — nơi chất lượng đủ dùng và chi phí là ưu tiên hàng đầu.

---

### Bài tập 2.3 — Trải Nghiệm Người Dùng với Streaming

**Streaming quan trọng nhất trong trường hợp nào, và khi nào thì non-streaming lại phù hợp hơn?** (1 đoạn văn)

> Streaming quan trọng nhất trong các ứng dụng chatbot hoặc trợ lý ảo tương tác trực tiếp với người dùng — khi response dài và người dùng cần thấy kết quả ngay lập tức thay vì chờ toàn bộ. Non-streaming phù hợp hơn khi xử lý batch (ví dụ phân tích hàng nghìn văn bản tự động), khi kết quả cần hoàn chỉnh trước khi xử lý tiếp (ví dụ parse JSON từ response), hoặc khi tích hợp vào pipeline backend không có giao diện người dùng trực tiếp.

## Danh Sách Kiểm Tra Nộp Bài

- [ ] Tất cả tests pass: `pytest tests/ -v`
- [ ] `call_openai` đã triển khai và kiểm thử
- [ ] `call_openai_mini` đã triển khai và kiểm thử
- [ ] `compare_models` đã triển khai và kiểm thử
- [ ] `streaming_chatbot` đã triển khai và kiểm thử
- [ ] `retry_with_backoff` đã triển khai và kiểm thử
- [ ] `batch_compare` đã triển khai và kiểm thử
- [ ] `format_comparison_table` đã triển khai và kiểm thử
- [ ] `exercises.md` đã điền đầy đủ
- [ ] Sao chép bài làm vào folder `solution` và đặt tên theo quy định
