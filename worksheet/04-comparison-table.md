# 04 · Comparison Table — Bảng so sánh đầy đủ

> **Mục tiêu**: Tổng hợp tất cả số đã tính ở `03-cost-calculation.md` thành 1 bảng so sánh duy nhất — đây là artifact chính nhóm sẽ present.
>
> **Thời gian**: 10 phút (đầu phần Final)

---

## Vì sao có bảng so sánh?

Khi sếp hỏi "Nên deploy config nào?", bạn cần đặt lên bàn **1 bảng** thay vì đọc 3 báo cáo riêng. Bảng so sánh đầy đủ cho phép so sánh thẳng từng dòng, dễ nhìn ra tradeoff.

---

## Bảng chính

Điền số đã tính. Số nào chưa có → quay lại `03-cost-calculation.md` tính cho xong.

| | Config 1 | Config 2 | Config 3 |
|---|---|---|---|
| **Tên** | Budget-Traveler | Premium-Concierge | Smart-Voyager |
| **① Model** | GPT-4o-mini | Claude Sonnet 4.6 | DeepSeek V4 Pro |
| **② Web search** | OFF | ON broad | ON selective |
| **③ History** | Last 3 | Full | Last 5 |
| **Intent classifier** | LLM (GPT-4o-mini) | LLM (GPT-4o-mini) | LLM (GPT-4o-mini) |
| **Cost / conv (Scenario A — 4 turns)** | $0.0015 | $0.057 | $0.024 |
| **Cost / conv (Scenario B — 7 turns)** | $0.0018 | $0.069 | $0.031 |
| **Monthly A** (300 conv/day × 30) | $13.5 | $513 | $216 |
| **Monthly B** (1,200 conv/day × 30) | $64.8 | $2,484 | $1,116 |
| **vs human $4,500/mo (A)** | rẻ 333× | rẻ 8.7× | rẻ 20.8× |
| **vs human $18,000/mo (B)** | rẻ 277× | rẻ 7.2× | rẻ 16.1× |
| **Savings % (A)** | 99.7% | 88.6% | 95.2% |
| **Savings % (B)** | 99.6% | 86.2% | 93.8% |
| **Quality estimate** | Low-Med | High | Med-High |
| **Speed estimate** | High | Low | Medium |
| **Điểm yếu chính** | Info có thể bị cũ | Chi phí vận hành cao | Phụ thuộc API DeepSeek |
| **Best for** (khi nào nên dùng) | Mùa thấp điểm, FAQ | Khách VIP, tour luxury | Hoạt động chính hàng ngày |


---

## Quan sát nhanh từ bảng

Trước khi sang file recommendation, trả lời 4 câu — đây là material để present:

### Câu 1 — Config rẻ nhất là gì? Đắt nhất là gì?

```text
Rẻ nhất: Budget-Traveler — monthly B = $64.8
Đắt nhất: Premium-Concierge — monthly B = $2,484
Chênh: 38× lần
```


### Câu 2 — Knob nào ảnh hưởng cost nhiều nhất?

```text
Model tier là knob ảnh hưởng nhất (GPT-4o-mini vs Claude Sonnet chênh lệch giá 20-25 lần). Tiếp đến là Web Search (tốn thêm $0.005/query và ~800 input tokens mỗi lượt bật).
```


### Câu 3 — Tại sao Scenario B không đắt ×4 lần Scenario A?

```text
Mặc dù Volume tăng x4 và số lượt chat dài hơn (x1.75), nhưng Scenario B có tỷ lệ Booking/Khiếu nại cao hơn (45% so với 15%). Các intent này được handoff ngay lập tức nên tốn $0 LLM cost, giúp "pha loãng" chi phí tổng thể.
```


### Câu 4 — Có config nào AI đắt hơn human không?

```text
Không có config nào đắt hơn human. Ngay cả Premium-Concierge vẫn rẻ hơn con người 7-8 lần trong khi hoạt động 24/7 và xử lý đa ngôn ngữ tốt hơn. Điều này chứng minh hiệu quả kinh tế cực lớn của AI trong trường hợp này.
```


---

## Bảng kiểm trước khi sang file tiếp theo

- [x] Bảng đầy đủ — không còn ô trống
- [x] Đã có 4 câu trả lời cho 4 quan sát ở trên
- [x] Nhóm đồng thuận về số trong bảng (đã sanity check)

Xong → mở `05-recommendation.md` để viết recommendation cuối + chuẩn bị present.
