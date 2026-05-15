# 02 · Configuration Design — Đặt tên + Chốt knobs cho ≥3 Configs

> **Mục tiêu**: Biến phác thảo ở `01-base-flow.md` thành ≥3 configurations chi tiết, mỗi config có tên + 3 knobs đã chốt + lý do chọn.
>
> **Thời gian**: 15 phút (đầu phần Main, trước khi tính cost)

---

## Tại sao đặt tên + viết lý do?

Khi present, nhóm sẽ nói "Config 1, Config 2, Config 3" → người nghe sẽ chán ngay. Đặt tên gợi mở (Budget Bot, Premium Concierge, Smart Mix...) giúp memorable + cho thấy nhóm hiểu rõ tradeoff. Viết lý do giúp nhóm tự kiểm tra: "Mình chọn config này vì lý do gì? Có justify được không?"

---

## Cách điền

Với mỗi config: đặt tên + chốt 3 knobs + viết 2–3 câu lý do chọn. Mỗi câu lý do phải gắn với 1 tình huống thực tế (volume thấp / khách hỏi visa nhiều / budget bị siết...).

Tham khảo bảng pricing chi tiết tại `cost-reference-card.md` mục **3. Decision Points**.

---

## Config 1

**Tên config** (gợi mở: "Budget Bot", "Bare Minimum", "Lean Mode", "Night Mode" — đặt tên có cá tính):

```text
Budget-Traveler (Bare Minimum)
```


### 3 Knobs

**① Model tier**:

```text
Response model: GPT-4o-mini → giá $0.15 / $0.60 per 1M tokens (input/output)
Classifier model: GPT-4o-mini → giá $0.15 / $0.60 per 1M tokens
```

**② Web search**:

```text
☑ OFF
□ ON selective — bật cho intent: __________________
□ ON broad
```

**③ History management**:

```text
☑ Last 3
□ Last 5
□ Full
□ Summarize every ___ turns
```


### Lý do nhóm chọn config này

```text
1. Phục vụ giai đoạn mùa thấp điểm hoặc thử nghiệm ban đầu khi ưu tiên hàng đầu là kiểm soát chi phí.
2. Phù hợp cho các câu hỏi FAQ đơn giản trong Knowledge Base mà không cần dữ liệu thời gian thực.
3. Giảm thiểu chi phí tích lũy tokens từ lịch sử chat cho những cuộc hội thoại ngắn.
```

### Rủi ro lớn nhất của config này

```text
Thông tin về chính sách Visa hoặc sự kiện có thể bị lỗi thời (outdated) do không bật Web Search.
```


---

## Config 2

**Tên config**:

```text
Premium-Global-Concierge
```


### 3 Knobs

**① Model tier**:

```text
Response model: Claude Sonnet 4.6 → giá $3.00 / $15.00 per 1M tokens
Classifier model: GPT-4o-mini → giá $0.15 / $0.60 per 1M tokens
```

**② Web search**:

```text
□ OFF
□ ON selective — bật cho intent: __________________
☑ ON broad
```

**③ History management**:

```text
□ Last 3
□ Last 5
☑ Full
□ Summarize every ___ turns
```


### Lý do nhóm chọn config này

```text
1. Dành riêng cho đối tượng khách hàng VIP hoặc các tour cao cấp, nơi chất lượng phục vụ là ưu tiên số 1.
2. Đảm bảo bot không bao giờ quên các chi tiết quan trọng (budget, sở thích) nhờ Full History.
3. Luôn cung cấp thông tin mới nhất và chính xác nhất thông qua Web Search diện rộng.
```

### Rủi ro lớn nhất của config này

```text
Chi phí vận hành cực cao, có thể gây lỗ nếu không kiểm soát được số lượng tin nhắn từ người dùng.
```


---

## Config 3

**Tên config**:

```text
Smart-Voyager (Balanced Mix)
```


### 3 Knobs

**① Model tier**:

```text
Response model: DeepSeek V4 Pro → giá $1.74 / $3.48 per 1M tokens
Classifier model: GPT-4o-mini → giá $0.15 / $0.60 per 1M tokens
```

**② Web search**:

```text
□ OFF
☑ ON selective — bật cho intent: Visa, Weather
□ ON broad
```

**③ History management**:

```text
□ Last 3
☑ Last 5
□ Full
□ Summarize every ___ turns
```


### Lý do nhóm chọn config này

```text
1. Sử dụng DeepSeek V4 Pro để đạt chất lượng tương đương các model Strong nhưng với mức giá tối ưu hơn (rẻ hơn 4-5 lần so với Sonnet).
2. Kết hợp Web Search có chọn lọc cho các thông tin nhạy cảm (Visa, Thời tiết) để vừa đảm bảo độ chính xác vừa tiết kiệm API cost.
3. Cân bằng trải nghiệm người dùng với Last 5 turns, đủ cho hầu hết các luồng hội thoại du lịch.
```

### Rủi ro lớn nhất của config này

```text
Phụ thuộc vào sự ổn định của API DeepSeek và độ trễ (latency) có thể cao hơn các Big Tech providers.
```


---

## Config 4 (optional — nếu thời gian dư)

Nhóm có thể thiết kế thêm config thứ 4 để có thêm điểm so sánh. Không bắt buộc.

**Tên config**:

```text
(điền tên vào đây)
```

### 3 Knobs

```text
Model: ___    Web: ___    History: ___
```

### Lý do

```text
(điền 1–2 câu)
```

---

## Bảng kiểm trước khi tính cost

- [x] ≥3 configs đã đặt tên (không chỉ "Config 1/2/3")
- [x] Mỗi config đã chốt rõ 3 knobs (không còn ô trống)
- [x] Mỗi config có ≥2 câu lý do
- [x] 3 configs đủ khác biệt — không phải chỉ đổi mỗi 1 knob nhỏ
- [x] Nhóm đồng thuận đây là 3 configs đáng so sánh

**Nếu 3 configs quá giống nhau** (chỉ đổi model, knobs khác giống hệt) → quay lại tweak. Mục đích là thấy tradeoff — configs giống nhau quá → không thấy tradeoff.

Xong → mở `03-cost-calculation.md` để bắt đầu tính cost.
