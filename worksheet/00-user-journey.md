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

### Tourist #1 (Tên thành viên: Hồ Bảo Thư)

```text
1. Where should I travel in Vietnam this season if I want both beautiful scenery and good local food?

2. How much does a normal trip to Vietnam usually cost per day for tourists?

3. What’s the weather like in Vietnam these days? Is it a good time to visit Hanoi, Da Nang, or Ho Chi Minh City?

4. Is Vietnam safe for solo travelers, especially at night?

5. Do most people in tourist areas speak English, or should I prepare translation apps?

6. What are the must-try Vietnamese dishes for first-time visitors?

7. Are there any scams or tourist traps I should be careful about in Vietnam?
```


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
| 1 | Where should I travel in Vietnam this season? | Điểm đến/Guide | 2–3 lượt | ☑ Bot · □ Người |
| 2 | How much does a normal Vietnam trip cost per day? | Điểm đến/Guide | 1–2 lượt | ☑ Bot · □ Người |
| 3 | What’s the weather like in Vietnam these days? | Thời tiết/Sự kiện | 1 lượt | ☑ Bot · □ Người |
| 4 | Is Vietnam safe for solo travelers at night? | Visa/Policy | 2 lượt | ☑ Bot · □ Người |
| 5 | Do people in tourist areas speak English? | Điểm đến/Guide | 1 lượt | ☑ Bot · □ Người |
| 6 | What Vietnamese foods should first-time tourists try? | Điểm đến/Guide | 2 lượt | ☑ Bot · □ Người |
| 7 | Are there any scams tourists should avoid in Vietnam? | Visa/Policy | 2–3 lượt | ☑ Bot · □ Người |
| 8 | Can you help me book a Ha Long Bay cruise for next week? | Tour/Booking | 3–5 lượt | □ Bot · ☑ Người |
| 9 | I want a 7-day Vietnam itinerary for my family. | Tour/Booking | 4–6 lượt | ☑ Bot · ☑ Người |
| 10 | My hotel airport pickup never arrived. What should I do? | Khiếu nại | 3–4 lượt | □ Bot · ☑ Người |
---
## Bước 3 — Rút insight cho nhóm (cuối phần Setup)

**Tổng số câu hỏi nhóm gom được**:

```text
10 câu hỏi
```

**Phân bố intent thực tế của nhóm** (% mỗi intent):

```text
Guide: 50%
Visa: 20%
Weather: 10%
Booking: 10%
Khiếu nại: 10%
```

**Số lượt chat trung bình để xong 1 chủ đề**:

```text
2–3 lượt cho các câu hỏi thông tin (guide, weather, safety)

4–6 lượt cho booking hoặc lên lịch trình

3–4 lượt cho khiếu nại cần xử lý với nhân viên thật
```

**Đối chiếu với đề bài** (Scenario A = 4 lượt, Scenario B = 7 lượt):

```text
Hợp lý vì phần lớn các câu hỏi thông tin cơ bản như weather, food, destinations thường chỉ cần 1–3 lượt chat là đủ. Tuy nhiên, khác ở chỗ các câu hỏi booking hoặc itinerary thực tế thường dài hơn Scenario A vì tourist hay thay đổi yêu cầu giữa cuộc trò chuyện.
```

**Insight bất ngờ — điều gì nhóm chỉ hiểu sau khi đóng vai?**

```text
Insight bất ngờ — nhóm nhận ra rằng tourist thường hỏi nhiều intent trong cùng một conversation, ví dụ vừa hỏi weather, budget, rồi chuyển sang booking. Ngoài ra, các câu hỏi về safety/scam và visa phức tạp hơn tưởng tượng vì cần giải thích theo quốc tịch, khu vực và tình huống cụ thể.
```

---

## Bảng kiểm trước khi sang file tiếp theo

- [ ] Mỗi người trong nhóm đã viết ≥5 câu hỏi tourist
- [ ] Đã gom + phân loại intent cho ≥10 câu (bảng trên)
- [ ] Đã có phân bố intent % của nhóm (so với đề bài)
- [ ] Có ít nhất 1 insight về cách tourist thật sự dùng chatbot

Xong → mở `01-base-flow.md`.
