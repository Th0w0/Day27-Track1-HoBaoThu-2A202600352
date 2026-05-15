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
Nhóm recommend Config 3 — Smart Hybrid Assistant làm config chính để deploy quanh năm. 
Lý do là cost vẫn thấp: $189/tháng ở Scenario A và $1,332/tháng ở Scenario B, rẻ hơn human lần lượt 23.8× và 13.5×. 
So với Budget Bot, Smart Hybrid đắt hơn nhưng quality cao hơn vì dùng model mạnh cho visa, complaint và itinerary — những intent dễ ảnh hưởng trực tiếp đến niềm tin và booking.
```

### Câu 2 — So với human baseline $0.50/conv → tiết kiệm bao nhiêu? Có đắt hơn human ở chỗ nào không?

```text
Smart Hybrid tiết kiệm 95.8% ở Scenario A và 92.6% ở Scenario B. 
Tính theo tháng, chi phí AI chỉ $189 so với $4,500 ở low season, và $1,332 so với $18,000 ở high season. 
Không có scenario nào AI đắt hơn human, nhưng AI không nên thay thế hoàn toàn sales agent vì booking và complaint vẫn cần người thật xử lý để tăng conversion và giữ trải nghiệm khách hàng.
```

### Câu 3 — Khi nào nên upgrade / downgrade config?

Trước khi viết, tự hỏi:

- Volume bao nhiêu thì cost AI scale lớn hơn benefit?
- Quality complaint rate bao nhiêu thì biết Budget Bot không đủ?
- Có signal nào báo nên chuyển sang Premium? (mùa cao điểm bắt đầu? customer feedback?)

```text
Nên upgrade lên Luxury Travel Concierge khi bước vào mùa cao điểm, có nhiều khách VIP/private tour, hoặc khi complaint về chất lượng câu trả lời vượt khoảng 5%. 
Ngược lại, có thể downgrade về Budget Backpacker Bot ở low season nếu phần lớn câu hỏi chỉ là FAQ đơn giản như điểm đến, food, weather và volume thấp. 
Nếu chỉ được chọn 1 config cố định, Smart Hybrid vẫn hợp lý nhất vì giữ được quality cao mà monthly cost Scenario B vẫn chỉ $1,332.
```


### Câu 4 — Rủi ro lớn nhất của config được chọn?

Trước khi viết, tự hỏi:

- Rủi ro về quality? (visa info outdated? language mismatch?)
- Rủi ro về cost? (provider tăng giá? volume spike?)
- Rủi ro về business? (khách bị bot trả lời sai → bad review → mất khách?)
- Có mitigation plan không?


```text
Rủi ro lớn nhất của Smart Hybrid là routing sai intent: câu hỏi visa hoặc itinerary phức tạp có thể bị gửi sang model rẻ, làm giảm chất lượng trả lời. 
Mitigation là đặt rule rõ: visa, weather, complaint, itinerary dài hoặc câu có booking intent phải được chuyển sang model mạnh hoặc human. 
Rủi ro phụ là thông tin visa/weather outdated, nên web search phải bật selective cho hai intent này và bot cần handoff nếu confidence thấp.
```

---

## Final answer — Recommendation in 1 paragraph

Tổng hợp 4 câu trên thành 1 paragraph 5–7 câu — đây là phần nhóm sẽ đọc / chiếu khi present.

```text
Nhóm recommend Smart Hybrid Assistant là config phù hợp nhất để deploy cho travel chatbot vì balance tốt giữa cost, quality và speed. Config này dùng GPT-4o-mini cho FAQ đơn giản và DeepSeek V4 Pro cho visa, complaint và itinerary phức tạp, giúp tối ưu chi phí mà vẫn giữ chất lượng trả lời cao. Monthly cost chỉ khoảng $189 ở low season và $1,332 ở high season, vẫn rẻ hơn human support lần lượt 23.8× và 13.5×. Ngoài ra, selective web search cho weather và visa giúp chatbot tránh trả lời outdated information mà không làm cost tăng quá nhiều. Nhóm cũng chọn Last 5 turns để chatbot nhớ đủ context như budget, family size hoặc travel style của tourist. Tuy nhiên, booking và complaint quan trọng vẫn nên handoff sang human để đảm bảo conversion và customer experience. Đây là config phù hợp nhất cho production thực tế vì vừa scalable vừa đủ chất lượng cho phần lớn khách du lịch quốc tế.
```

---
## Chuẩn bị Present (5 phút)

### Nhịp 0:00 – 0:30 — Base flow + 3 knobs đã chọn

Ai trình bày: Thành viên 1

Nói gì:

```text
Nhóm xây dựng chatbot cho travel agency với flow gồm: intent classification → routing → context assembly → response generation. 
Ba knobs chính nhóm phân tích là model tier, web search và history management vì đây là ba yếu tố ảnh hưởng trực tiếp đến cost, quality và speed.
```

---

### Nhịp 0:30 – 1:00 — Config overview

Ai trình bày: Thành viên 1

Nói gì (đọc nhanh tên + knobs 3 configs):

```text
Config 1 — Budget Backpacker Bot: GPT-4o-mini, web selective, Last 3 turns.

Config 2 — Luxury Travel Concierge: Claude Sonnet, web broad, Full history.

Config 3 — Smart Hybrid Assistant: mix GPT-4o-mini + DeepSeek V4 Pro, web selective, Last 5 turns.
```

---

### Nhịp 1:00 – 2:00 — Cost comparison

Ai trình bày: Thành viên 2

Nói gì (chiếu bảng so sánh, highlight rẻ nhất / đắt nhất):

```text
Config rẻ nhất là Budget Backpacker Bot với monthly cost chỉ khoảng $468 ở Scenario B, rẻ hơn human support khoảng 38.5 lần. 
Config đắt nhất là Luxury Travel Concierge với khoảng $3,888/tháng ở Scenario B, nhưng vẫn rẻ hơn human khoảng 4.6 lần. 
Smart Hybrid nằm ở giữa với $1,332/tháng, nhưng quality estimate gần premium hơn là budget. 
Điều này cho thấy có thể tăng quality đáng kể mà cost vẫn thấp hơn human support rất nhiều.
```

---

### Nhịp 2:00 – 3:00 — Key insight

Ai trình bày: Thành viên 2

Nói gì (knob nào ảnh hưởng cost nhiều nhất + tại sao):

```text
Insight lớn nhất của nhóm là model tier ảnh hưởng cost mạnh hơn nhiều so với web search hoặc history. 
Đổi từ GPT-4o-mini sang Claude Sonnet làm monthly cost tăng khoảng 4–8 lần, trong khi selective web search chỉ tăng vài cent mỗi conversation. 
Ngoài ra, Scenario B không tăng cost quá mạnh vì gần một nửa intent là booking hoặc complaint được handoff sang human.
```

---

### Nhịp 3:00 – 4:30 — Recommendation + justification

Ai trình bày: Thành viên 1

Nói gì:

```text
Nhóm recommend Smart Hybrid Assistant là config phù hợp nhất để deploy cho travel chatbot vì balance tốt giữa cost, quality và speed. Config này dùng GPT-4o-mini cho FAQ đơn giản và DeepSeek V4 Pro cho visa, complaint và itinerary phức tạp, giúp tối ưu chi phí mà vẫn giữ chất lượng trả lời cao. Monthly cost chỉ khoảng $189 ở low season và $1,332 ở high season, vẫn rẻ hơn human support lần lượt 23.8× và 13.5×. Ngoài ra, selective web search cho weather và visa giúp chatbot tránh trả lời outdated information mà không làm cost tăng quá nhiều. Nhóm cũng chọn Last 5 turns để chatbot nhớ đủ context như budget, family size hoặc travel style của tourist. Tuy nhiên, booking và complaint quan trọng vẫn nên handoff sang human để đảm bảo conversion và customer experience. Đây là config phù hợp nhất cho production thực tế vì vừa scalable vừa đủ chất lượng cho phần lớn khách du lịch quốc tế.
```

---

### Nhịp 4:30 – 5:00 — Hardest question prep

Ai trình bày: Thành viên 2

Nhóm dự đoán câu hỏi khó nhất sẽ bị hỏi là gì?

```text
"Tại sao không chọn luôn Budget Backpacker Bot nếu nó rẻ hơn nhiều?"
```

Câu trả lời sẵn:

```text
Budget Backpacker Bot phù hợp cho FAQ đơn giản nhưng dễ fail ở các intent quan trọng như visa, itinerary hoặc complaint. 
Trong travel business, chỉ cần một số câu trả lời sai hoặc thiếu context cũng có thể làm giảm trust và mất booking. 
Smart Hybrid tăng cost không quá nhiều nhưng cải thiện quality đáng kể ở các tình huống ảnh hưởng trực tiếp đến customer experience.
```

## Q&A — 2 phút sau khi present xong

Sẵn sàng cho 1 câu từ class + 1 câu từ instructor. Không cần lo lắng — nếu chưa biết câu trả lời, nói "đây là điểm nhóm chưa nghĩ đến — sẽ tính lại sau buổi".

**3 câu instructor thường hỏi**:

1. *"Knob nào ảnh hưởng cost nhiều nhất trong config của nhóm? Tại sao?"*
2. *"Nếu provider tăng giá API ×2 → config của nhóm còn sống được không?"*
3. *"So với nhóm X (vừa present trước) — tại sao nhóm bạn chọn khác?"*

Suy nghĩ trước câu trả lời ngắn:
```text
1. Knob ảnh hưởng cost lớn nhất là model tier vì đổi từ cheap model sang strong model làm token cost tăng khoảng 4–8 lần, lớn hơn nhiều so với web search hoặc history.

2. Nếu provider tăng giá API ×2 thì config vẫn sống được vì Smart Hybrid hiện vẫn rẻ hơn human support khoảng 13.5× ở Scenario B. Ngoài ra nhóm có thể fallback sang model rẻ hơn như DeepSeek Flash hoặc giảm web usage để giữ margin.

3. Nhóm chọn Smart Hybrid thay vì full premium vì travel chatbot có rất nhiều FAQ đơn giản không cần model mạnh. Mix model theo intent giúp giữ quality ở các case quan trọng nhưng vẫn tối ưu cost cho production thực tế.
```

---

## Bảng kiểm cuối cùng — trước 12:00 Pens Down

- [ ] Đã trả lời 4 câu PM (Recommend / Savings / Threshold / Risk)
- [ ] Final answer paragraph viết gọn (5–7 câu)
- [ ] Phân công 5 nhịp present cho mỗi thành viên
- [ ] Có sẵn câu trả lời cho 3 câu Q&A dự đoán
- [ ] Comparison table có sẵn để chiếu / chuyền tay khi present
- [ ] Repo đã commit + push (sẽ nộp link sau buổi học)

---

## Sau buổi học

1. **Commit + push repo** với tất cả file đã điền.
2. **Dán link repo** vào Discord `#day27-evidence-boards` trước 23:59.
3. **Chuẩn bị cho D28**: peer review giữa các nhóm — sẽ bị hỏi câu chất vấn khó hơn instructor. Polish thêm bảng + recommendation tối nay.

*Hôm nay bạn chứng minh bằng số. Ngày mai bạn bảo vệ bằng logic.*
