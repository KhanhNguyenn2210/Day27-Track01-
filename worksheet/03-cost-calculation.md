# 03 · Cost Calculation — Tính chi phí từng Config × 2 Scenarios

> **Mục tiêu**: Với mỗi config đã thiết kế ở `02-config-design.md`, tính cost/turn → cost/conversation → monthly cho cả 2 scenarios (low season + high season).
>
> **Thời gian**: 55 phút (phần lớn của Main phase) — checkpoint 11:00 và 11:20

---

## Cách làm

**Đừng tính tay từng turn — đó là cách thừa thời gian.** Dùng AI để tính. Dán prompt template từ `prompts/01-cost-calc.md` vào ChatGPT/Claude/Gemini, thay parameters theo config của nhóm, AI sẽ tính cho.

Tuy nhiên nhóm phải **hiểu** kết quả AI trả về, không phải copy-paste mù. Mỗi lần AI trả số, nhóm phải tự kiểm 1 lần: con số này có hợp lý không? Có vẻ quá đắt hay quá rẻ?

---

## Trước khi gọi AI — Setup chung

**Các tham số cố định cho tất cả configs** (tham khảo `cost-reference-card.md` mục 4):

```text
System prompt:              500 tokens
User message:                80 tokens
Assistant response:         180 tokens (output)
1 prior turn (history):     260 tokens (80 user + 180 assistant)
RAG top-5 chunks:         1,250 tokens (cố định)
Web search results:         800 tokens (khi bật)
Web search API call:       $0.005 / call (Tavily)
LLM classifier:            ~170 tokens (150 in + 20 out) — nếu dùng
```

**Scenario A — mùa thấp điểm**:

```text
Volume:            300 conversations / ngày
Turns/conv:        avg 4 lượt
Intent mix:        Guide 50%, Visa 25%, Weather 10%, Booking 10%, Complaint 5%
AI-served ratio:   85% (15% là Booking + Complaint = handoff)
```

**Scenario B — mùa cao điểm**:

```text
Volume:           1,200 conversations / ngày (×4)
Turns/conv:        avg 7 lượt
Intent mix:        Guide 30%, Visa 15%, Weather 10%, Booking 35%, Complaint 10%
AI-served ratio:   55% (45% là handoff)
```

**Human baseline để so sánh**: $0.50 / conversation cố định.

---

## Quy trình tính cho 1 config (lặp lại cho từng config)

### Bước 1 — Cost per turn (4 mốc: Turn 1, 3, 5, 7)

Với mỗi mốc, tính:

1. **History tokens** = (T − 1) × 260 nếu Full · min(T−1, N) × 260 nếu Last N · ~150 cố định nếu Summarize.
2. **Input total** = 500 (sys) + history + 1,250 (RAG) + (800 nếu web ON cho intent này) + 80 (msg)
3. **Output** = 180 tokens
4. **Cost model** = (input × $/M_input + output × $/M_output) / 1,000,000
5. **Cost web API** = $0.005 nếu web ON cho intent này, ngược lại $0
6. **Cost classifier** = ~$0.000035 nếu dùng LLM classifier, ngược lại $0
7. **Total cost/turn** = cost model + cost web + cost classifier

→ Dùng prompt template, AI sẽ tự tính. Nhập config + intent + turn number, AI ra bảng kết quả.

### Bước 2 — Cost per conversation cho từng intent

Cost 1 conversation = sum(cost từng turn) trong conversation đó.

- Scenario A: cộng cost của Turn 1 → Turn 4 (4 turns)
- Scenario B: cộng cost của Turn 1 → Turn 7 (7 turns)

Tính riêng cho mỗi intent (vì web search có thể khác — Visa/Weather bật web, Guide không bật):

```text
cost_conv_guide   (4 turns) = ____
cost_conv_visa    (4 turns) = ____  (web search bật cho Visa)
cost_conv_weather (4 turns) = ____  (web search bật cho Weather)
cost_1_turn_only             = ____  (Booking + Complaint chỉ 1 turn rồi handoff,
                                       chỉ tốn classifier nếu dùng LLM)
```

### Bước 3 — Weighted average cost per conversation (toàn bộ intent)

Lấy % intent mix × cost từng intent:

**Scenario A** (Guide 50%, Visa 25%, Weather 10%, Booking 10%, Complaint 5%):

```text
avg_cost_A = 50% × cost_conv_guide_4t
          + 25% × cost_conv_visa_4t
          + 10% × cost_conv_weather_4t
          + 10% × cost_1_turn_only
          +  5% × cost_1_turn_only
```

**Scenario B** (Guide 30%, Visa 15%, Weather 10%, Booking 35%, Complaint 10%, 7 turns cho AI-served):

```text
avg_cost_B = 30% × cost_conv_guide_7t
          + 15% × cost_conv_visa_7t
          + 10% × cost_conv_weather_7t
          + 35% × cost_1_turn_only
          + 10% × cost_1_turn_only
```

### Bước 4 — Monthly cost

```text
monthly_A = avg_cost_A × 300 conv/ngày × 30 ngày
monthly_B = avg_cost_B × 1,200 conv/ngày × 30 ngày
```

### Bước 5 — So sánh với human baseline

```text
human_A = $0.50 × 300 × 30 = $4,500 / tháng
human_B = $0.50 × 1,200 × 30 = $18,000 / tháng

savings_A% = (4,500 − monthly_A) / 4,500 × 100
savings_B% = (18,000 − monthly_B) / 18,000 × 100
```

Nếu savings ÂM → AI đắt hơn human → cần justify (24/7? đa ngôn ngữ? scale?).

---

## Điền số cho từng config

Dùng AI tính xong, copy số vào đây. Đừng quên kiểm 1 lần xem số có hợp lý không.

### Config 1 — Budget-Traveler (Bare Minimum)

| Item | Scenario A (4 turns) | Scenario B (7 turns) |
|---|---|---|
| Cost / conversation (avg) | $0.0015 | $0.0018 |
| Monthly cost | $13.5 | $64.8 |
| Human baseline | $4,500 | $18,000 |
| **Rẻ hơn human ___×** | 333× | 277× |
| **Savings %** | 99.7% | 99.6% |

**Sanity check**:

```text
Cost cực kỳ thấp vì GPT-4o-mini rất rẻ và không dùng Web Search. Scenario B chỉ đắt hơn A khoảng 20% dù số lượt chat tăng gần gấp đôi, nhờ history bị giới hạn ở Last 3 turns.
```


---

### Config 2 — Premium-Global-Concierge

| Item | Scenario A | Scenario B |
|---|---|---|
| Cost / conversation (avg) | $0.057 | $0.069 |
| Monthly cost | $513 | $2,484 |
| **Rẻ hơn human ___×** | 8.7× | 7.2× |
| **Savings %** | 88.6% | 86.2% |

**Sanity check**:

```text
Cost cao nhất trong 3 config do dùng Claude Sonnet và Web Search diện rộng. Tuy nhiên vẫn tiết kiệm được hơn 85% so với chi phí thuê người, trong khi cung cấp dịch vụ 24/7 và thông tin luôn cập nhật.
```


---

### Config 3 — Smart-Voyager (Balanced Mix)

| Item | Scenario A | Scenario B |
|---|---|---|
| Cost / conversation (avg) | $0.024 | $0.031 |
| Monthly cost | $216 | $1,116 |
| **Rẻ hơn human ___×** | 20.8× | 16.1× |
| **Savings %** | 95.2% | 93.8% |

**Sanity check**:

```text
Đây là "điểm ngọt" (sweet spot). Chi phí tăng đáng kể so với Budget nhưng đổi lại được độ chính xác của Web Search cho Visa/Weather và sự thông minh của DeepSeek V4 Pro. Rất khả thi để triển khai đại trà.
```


---

### Config 4 (optional)

| Item | Scenario A | Scenario B |
|---|---|---|
| Cost / conversation (avg) | $________ | $________ |
| Monthly cost | $________ | $________ |
| **Rẻ hơn human ___×** | _____× | _____× |
| **Savings %** | ___% | ___% |

---

## Quality + Speed estimate (qualitative)

Mỗi config — estimate Low / Medium / High. Không có công cụ đo chính xác trong lab, ước tính dựa trên model tier + web search + history.

| Config | Quality (Low/Med/High) | Speed (Low/Med/High) | Lý do |
|---|---|---|---|
| 1: Budget-Traveler | Low-Med | High | Model mini cực nhanh nhưng thiếu info real-time. |
| 2: Premium-Concierge | High | Low | Sonnet cực thông minh + Web search nhưng phản hồi chậm (~3-5s). |
| 3: Smart-Voyager | Med-High | Medium | DeepSeek V4 Pro tối ưu tốt, Web search có chọn lọc nên tốc độ ổn. |
| 4: ___ | ___ | ___ | (1 câu) |

**Hướng dẫn ước tính**:

- **Quality**: Cheap model → Low (70%). Strong model → High (88%). Web search bật → Quality tăng vì info real-time. History Full → Quality tốt hơn ở conversation dài.
- **Speed**: Cheap model thường nhanh (~200ms). Strong model chậm hơn (~1–3s). Web search bật → +1–2s.

---

## Bảng kiểm trước khi sang file tiếp theo

- [x] Tất cả ≥3 configs đã có cost/conv + monthly cho cả 2 scenarios
- [x] Đã so sánh từng config với human baseline ($0.50/conv)
- [x] Có quality + speed estimate cho mỗi config
- [x] Đã sanity check — không có số "quá lạ" (cost <$0.001 hoặc >$1/conv)

⚑ **Checkpoint 11:00**: ≥1 config đã tính cost xong &nbsp; · &nbsp; ⚑ **Checkpoint 11:20**: tất cả configs đã tính cost xong cho cả 2 scenarios.

Xong → mở `04-comparison-table.md`.
