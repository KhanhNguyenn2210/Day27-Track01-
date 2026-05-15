# 05 · Recommendation + Justification — Kết luận & Chuẩn bị Present

> **Mục tiêu**: Chọn 1 config (hoặc combo) nhóm recommend deploy, viết justification ngắn gọn, và chuẩn bị 5 phút present.
>
> **Thời gian**: 10 phút (cuối phần Final) — Pens down lúc 12:00

---

## Bảng số ai cũng tính được. PM giỏi phải **recommend** và **justify**.

Đây là phần quan trọng nhất — phần phân biệt nhóm chỉ làm xong với nhóm thực sự hiểu sản phẩm.

---

## 4 câu hỏi nhóm phải trả lời

Mỗi câu trả lời 2–4 câu. Không lan man, không clichés. Mỗi câu phải justify được bằng số trong bảng so sánh.

### Câu 1 — Recommend config nào?

Trước khi viết, thảo luận 1 phút:

- Recommend 1 config duy nhất chạy quanh năm? Hay 2 configs khác nhau cho mùa thấp / mùa cao?
- Có nên recommend "Smart Mix model theo intent" thay vì pick 1 config cố định không?
- Nếu sếp nói "chỉ deploy 1 config thôi" — chọn cái nào?

```text
Nhóm recommend triển khai Config 3 (Smart-Voyager) làm cấu hình mặc định. 
Lý do: Đây là "điểm ngọt" (sweet spot) tối ưu giữa chi phí và chất lượng. Chi phí chỉ khoảng $0.024-$0.031/cuộc hội thoại (tiết kiệm hơn 93% so với người), trong khi vẫn đảm bảo độ chính xác cao nhờ DeepSeek V4 Pro và Web Search có chọn lọc cho các thông tin nhạy cảm như Visa/Thời tiết.
```

### Câu 2 — So với human baseline $0.50/conv → tiết kiệm bao nhiêu? Có đắt hơn human ở chỗ nào không?

```text
Tiết kiệm 95.2% ở Scenario A ($4,284/tháng) và 93.8% ở Scenario B ($16,884/tháng). 
AI rẻ hơn con người ít nhất 16 lần trong mọi kịch bản. AI vượt trội ở khả năng trực 24/7, phản hồi tức thì và xử lý được hàng ngàn khách cùng lúc mà không cần scale nhân sự tuyến tính, giúp doanh nghiệp tối ưu biên lợi nhuận cực lớn.
```


### Câu 3 — Khi nào nên upgrade / downgrade config?

```text
1. Upgrade lên Premium khi: Tỷ lệ khách hỏi về các tour cao cấp (Luxury) tăng cao, hoặc khi nhận thấy "Smart-Voyager" trả lời sai các câu hỏi lịch trình phức tạp trên 15%.
2. Downgrade xuống Budget khi: Vào khung giờ đêm (12h đêm - 5h sáng) khi lượng khách ít và câu hỏi chủ yếu là FAQ đơn giản, hoặc khi ngân sách marketing bị siết chặt trong mùa thấp điểm cực độ.
```


### Câu 4 — Rủi ro lớn nhất của config được chọn?

```text
Rủi ro chính: Sự ổn định của API DeepSeek và độ trễ (latency) trong giờ cao điểm. 
Mitigation plan: Thiết lập hệ thống Fallback tự động sang GPT-4o-mini (Budget) hoặc Gemini Flash nếu API DeepSeek gặp sự cố hoặc phản hồi chậm quá 5 giây. Đồng thời, duy trì đội ngũ sales hỗ trợ ngay khi chatbot chuyển trạng thái "Escalate".
```


---

## Final answer — Recommendation in 1 paragraph

Tổng hợp 4 câu trên thành 1 paragraph 5–7 câu — đây là phần nhóm sẽ đọc / chiếu khi present.

```text
Nhóm đề xuất triển khai cấu hình Smart-Voyager làm giải pháp cốt lõi cho Travel Agency. Với mức chi phí tối ưu chỉ từ $0.024 đến $0.031 mỗi cuộc hội thoại, giải pháp này giúp tiết kiệm trung bình 94% chi phí so với nhân viên vận hành, tương đương khoảng 4.000 đến 16.000 USD mỗi tháng tùy mùa. Smart-Voyager sử dụng model DeepSeek V4 Pro kết hợp với tìm kiếm Web có chọn lọc cho Visa và Thời tiết, đảm bảo độ chính xác thông tin cao và khả năng ghi nhớ context tốt (Last 5 turns). Đây là phương án khả thi nhất để triển khai ngay lập tức, vừa mang lại trải nghiệm khách hàng hiện đại, vừa tối đa hóa lợi nhuận cho doanh nghiệp trong bối cảnh du lịch quốc tế phục hồi mạnh mẽ.
```

---

## Chuẩn bị Present (5 phút)

Chia 5 phút thành 5 nhịp. 1 người trong nhóm chính phụ trách 1 nhịp. Người còn lại trả lời Q&A.

### Nhịp 0:00 – 0:30 — Base flow + 3 knobs đã chọn
Ai trình bày: Nguyễn Bá Khánh
Nói gì: "Flow của chúng tôi tập trung vào việc phân loại intent sớm để route khách hàng vào các nhánh tối ưu chi phí. Chúng tôi điều chỉnh 3 knobs: Model Tier, Web Search và History để tạo ra 3 cấu hình phục vụ các mục tiêu kinh doanh khác nhau."

### Nhịp 0:30 – 1:00 — Config overview
Ai trình bày: Lưu Thị Ngọc Quỳnh
Nói gì: "3 Config của nhóm gồm: Budget-Traveler (siêu rẻ, không Web), Premium-Concierge (tối đa chất lượng với Claude Sonnet) và Smart-Voyager (cân bằng giữa chi phí và hiệu năng dùng DeepSeek)."

### Nhịp 1:00 – 2:00 — Cost comparison
Ai trình bày: Nguyễn Phương Nam
Nói gì: "Bảng so sánh cho thấy tất cả AI config đều rẻ hơn con người ít nhất 7 lần. Budget Bot chỉ tốn $13/tháng mùa thấp điểm, trong khi Premium có thể lên tới $2.400 vào mùa cao điểm."

### Nhịp 2:00 – 3:00 — Key insight
Ai trình bày: Nguyễn Bá Khánh
Nói gì: "Insight quan trọng nhất là Model Tier quyết định 80% chi phí. Chúng ta không cần dùng model mạnh nhất cho mọi câu hỏi, mà nên mix thông minh để tối ưu ROI."

### Nhịp 3:00 – 4:30 — Recommendation + justification
Ai trình bày: Nguyễn Phương Nam
Nói gì: (Đọc paragraph Final answer ở trên)

### Nhịp 4:30 – 5:00 — Hardest question prep
Ai trình bày: Cả nhóm
Câu hỏi khó nhất: "Nếu DeepSeek bị lỗi hoặc chính sách Visa thay đổi quá nhanh thì sao?"
Trả lời: "Chúng tôi có cơ chế Fallback sang GPT-4o-mini và hệ thống Web Search selective luôn đảm bảo dữ liệu Visa mới nhất được cập nhật theo thời gian thực."


---

## Q&A — 2 phút sau khi present xong

Sẵn sàng cho 1 câu từ class + 1 câu từ instructor. Không cần lo lắng — nếu chưa biết câu trả lời, nói "đây là điểm nhóm chưa nghĩ đến — sẽ tính lại sau buổi".

**3 câu instructor thường hỏi**:

1. *"Knob nào ảnh hưởng cost nhiều nhất trong config của nhóm? Tại sao?"*
2. *"Nếu provider tăng giá API ×2 → config của nhóm còn sống được không?"*
3. *"So với nhóm X (vừa present trước) — tại sao nhóm bạn chọn khác?"*

Suy nghĩ trước câu trả lời ngắn:

```text
1. Model Tier là knob ảnh hưởng nhất vì giá token chênh lệch cực lớn giữa các đời model.
2. Hệ thống vẫn sống tốt vì biên lợi nhuận tiết kiệm được là hơn 90%, đủ dư địa để hấp thụ việc tăng giá.
3. Nhóm chọn DeepSeek để tối ưu chi phí mà vẫn giữ được chất lượng của một 'Strong model', thay vì chọn Claude Sonnet quá đắt đỏ.
```

---

## Bảng kiểm cuối cùng — trước 12:00 Pens Down

- [x] Đã trả lời 4 câu PM (Recommend / Savings / Threshold / Risk)
- [x] Final answer paragraph viết gọn (5–7 câu)
- [x] Phân công 5 nhịp present cho mỗi thành viên
- [x] Có sẵn câu trả lời cho 3 câu Q&A dự đoán
- [x] Comparison table có sẵn để chiếu / chuyền tay khi present
- [x] Repo đã commit + push (sẽ nộp link sau buổi học)

---

## Sau buổi học

1. **Commit + push repo** với tất cả file đã điền.
2. **Dán link repo** vào Discord `#day27-evidence-boards` trước 23:59.
3. **Chuẩn bị cho D28**: peer review giữa các nhóm — sẽ bị hỏi câu chất vấn khó hơn instructor. Polish thêm bảng + recommendation tối nay.

*Hôm nay bạn chứng minh bằng số. Ngày mai bạn bảo vệ bằng logic.*
