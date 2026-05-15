# 00 · User Journey Simulation — Đóng vai Tourist

> **Mục tiêu**: Trước khi tính chi phí, nhóm phải hình dung được khách hàng thật sự hỏi gì, hỏi như thế nào, và 1 conversation thực tế trông ra sao.
>
> **Thời gian**: 8 phút (trong 15 phút phần Setup)

---

## Tại sao phải làm bước này?

Nếu nhóm bắt đầu tính cost mà chưa biết tourist hỏi gì → mọi con số chỉ là lý thuyết. Bước này buộc nhóm "chạm" sản phẩm trước khi mở Excel.

---

## Bước 1 — Mỗi người đóng vai 1 tourist (4 phút)

Tưởng tượng mình là 1 khách du lịch nước ngoài đang plan trip Việt Nam. Bạn vừa mở website công ty du lịch, thấy có chatbot ở góc màn hình. Bạn sẽ hỏi gì?

Trước khi viết, tự hỏi:

- Mình từ đâu đến? Mỹ, Anh, Hàn, Nhật, Úc?
- Đi 1 mình hay đi nhóm? Budget khoảng bao nhiêu?
- Đã biết gì về Việt Nam? Lần đầu đến hay đã đến rồi?
- Mình lo lắng điều gì nhất? (visa, an toàn, ngôn ngữ, thời tiết, ẩm thực, lừa đảo...)

Viết **5–7 câu hỏi bằng tiếng Anh** mình sẽ thật sự gửi cho chatbot. Viết câu hỏi tự nhiên, đúng giọng tourist — không phải đặt câu hỏi "nghe có vẻ technical".

→ Mỗi người viết vào ô dưới (chưa có gì sẵn — đừng nhìn người bên cạnh):

### Tourist #1 (Tên thành viên: Nguyễn Bá Khánh )

```text
1.what the best time to visit Vietnam?
2.how many days needed to visit Vietnam?
3.what is the best foods I should try in Vietnam?
4.is it safe to travel to Vietnam?
5.how much money is needed for a 10 days trip to Vietnam?
```

### Tourist #2 (Tên thành viên: Lưu Thị Ngọc Quỳnh )

```text
1. I'm from Korea, is it easy to get a vietnam e-visa?
2. How much should I budget for 7 days in Vietnam, excluding flights?
3. Is it safe to travel to Vietnam as a solo female traveler in 2026?
4. What are the must-try street foods in Hanoi and Ho Chi Minh City?
5. Do I need any vaccinations before traveling to Vietnam?
6. Can you recommend a 7-day itinerary for first-time visitors to Vietnam?
```

### Tourist #3 (Tên thành viên: Nguyễn Phương Nam )

```text
I'm from Australia and planning a trip to Vietnam in December. I'd like to visit Hanoi, Ha Long Bay, and Hoi An. Can you suggest an itinerary and let me know about the weather conditions during that time?

I'm also interested in experiencing local culture. What are some traditional festivals or events happening in December that I shouldn't miss?

Regarding safety, are there any specific precautions I should be aware of when traveling to Vietnam as a tourist?

Do I need to arrange my own transportation between cities, or is that something your company can handle?

Finally, what's the currency and payment situation like? Is it easy to use credit cards, or should I rely mostly on cash?
```

---

## Bước 2 — Gom lại và phân loại (4 phút)

Cả nhóm chụm vào, gom tất cả câu hỏi lại. Trước khi điền bảng, thảo luận 1 phút:

- Có câu hỏi nào lặp lại giữa các tourist không?
- Có chủ đề nào không ai trong nhóm nghĩ tới ban đầu nhưng quan trọng?
- Câu nào chatbot có thể trả lời được? Câu nào cần chuyển sang nhân viên thật?

5 intent có sẵn (tham khảo `cost-reference-card.md` mục 2):

- **Visa/Policy** — chính sách, thủ tục nhập cảnh
- **Điểm đến/Guide** — gợi ý đi đâu, làm gì, ăn gì
- **Thời tiết/Sự kiện** — info real-time
- **Tour/Booking** — đặt vé, đặt tour, đặt phòng → chuyển sales
- **Khiếu nại** — phàn nàn → chuyển manager

Sau khi gom, điền bảng phân loại:

| # | Câu hỏi (1 dòng) | Intent thuộc loại nào | Cần bao nhiêu lượt chat để xong? | Bot trả lời hay chuyển người? |
|---|---|---|---|---|
| 1 | What is the best time to visit Vietnam? | Điểm đến/Guide | 2-3 | ☑ Bot · □ Người |
| 2 | I'm from Korea, is it easy to get a vietnam e-visa? | Visa/Policy | 3-4 | ☑ Bot · □ Người |
| 3 | How much should I budget for 7 days in Vietnam? | Điểm đến/Guide | 3-4 | ☑ Bot · □ Người |
| 4 | Is it safe to travel to Vietnam as a solo female traveler? | Visa/Policy | 2-3 | ☑ Bot · □ Người |
| 5 | Suggest an itinerary for Hanoi, Ha Long, Hoi An in Dec. | Điểm đến/Guide | 5-6 | ☑ Bot · □ Người |
| 6 | Festivals or events in December I shouldn't miss? | Thời tiết/Sự kiện | 3-4 | ☑ Bot · □ Người |
| 7 | Do I need any vaccinations before traveling? | Visa/Policy | 2-3 | ☑ Bot · □ Người |
| 8 | Transportation between cities: can your company handle? | Tour/Booking | 1 | □ Bot · ☑ Người |
| 9 | Currency situation: credit cards or mostly cash? | Visa/Policy | 2-3 | ☑ Bot · □ Người |
| 10 | What are must-try street foods in Hanoi and HCMC? | Điểm đến/Guide | 3-4 | ☑ Bot · □ Người |

---

## Bước 3 — Rút insight cho nhóm (cuối phần Setup)

Trả lời nhanh 4 câu — sẽ dùng lại ở các bước sau:

**Tổng số câu hỏi nhóm gom được**:

```text
16
```

**Phân bố intent thực tế của nhóm** (% mỗi intent):

```text
Guide: 50%
Visa: 38%
Weather: 6%
Booking: 6%
Khiếu nại: 0%
```

**Số lượt chat trung bình để xong 1 chủ đề**:

```text
3-4 lượt cho thông tin (Guide/Visa/Weather), 1 lượt cho booking (chuyển người)
```

**Đối chiếu với đề bài** (Scenario A = 4 lượt, Scenario B = 7 lượt):

```text
Hợp lý vì đa số câu hỏi của nhóm là FAQ và Guide cơ bản, tốn khoảng 3-4 lượt để trả lời đầy đủ thông tin, khá sát với Scenario A.
```

**Insight bất ngờ — điều gì nhóm chỉ hiểu sau khi đóng vai?**

```text
1. Khách du lịch hỏi rất nhiều về an toàn và ngân sách cụ thể, đòi hỏi bot phải có khả năng trích xuất dữ liệu từ RAG chính xác.
2. Các câu hỏi về thủ tục (visa, tiêm chủng) thường đi kèm với bối cảnh cá nhân (quốc tịch, thời điểm đi), cần bot nhớ context tốt.
```


---

## Bảng kiểm trước khi sang file tiếp theo

- [ ] Mỗi người trong nhóm đã viết ≥5 câu hỏi tourist
- [ ] Đã gom + phân loại intent cho ≥10 câu (bảng trên)
- [ ] Đã có phân bố intent % của nhóm (so với đề bài)
- [ ] Có ít nhất 1 insight về cách tourist thật sự dùng chatbot

Xong → mở `01-base-flow.md`.
