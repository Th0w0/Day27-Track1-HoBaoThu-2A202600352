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

**Tên config**:

```text
Budget Backpacker Bot
```

### 3 Knobs

**① Model tier**:

```text
Response model: GPT-4o-mini → giá $0.15 / $0.60 per 1M tokens
Classifier model: keyword routing → giá $0
```

**② Web search**:

```text
☑ ON selective — bật cho intent: Weather, Visa
```

**③ History management**:

```text
☑ Last 3
```

### Lý do nhóm chọn config này

```text
Config này phù hợp cho travel agency nhỏ hoặc mùa thấp điểm khi cần tối ưu chi phí. Phần lớn tourist chỉ hỏi FAQ đơn giản như thời tiết, địa điểm, food nên GPT-4o-mini là đủ tốt.

Nhóm vẫn bật selective web search cho weather và visa vì đây là hai loại thông tin thay đổi liên tục. Last 3 turns giúp giảm token cost và giữ response nhanh hơn.
```

### Rủi ro lớn nhất của config này

```text
Chatbot có thể quên các thông tin quan trọng như budget hoặc itinerary nếu conversation kéo dài hơn 4–5 turns.
```

---

## Config 2

**Tên config**:

```text
Luxury Travel Concierge
```

### 3 Knobs

**① Model tier**:

```text
Response model: Claude Sonnet 4.6 → giá $3.00 / $15.00 per 1M tokens
Classifier model: GPT-4o-mini → giá $0.15 / $0.60 per 1M tokens
```

**② Web search**:

```text
☑ ON broad
```

**③ History management**:

```text
☑ Full
```

### Lý do nhóm chọn config này

```text
Config này hướng tới khách VIP hoặc khách đặt private/custom tours. Claude Sonnet cho khả năng conversation tự nhiên hơn, xử lý itinerary dài và nhiều constraints tốt hơn.

Web search broad giúp đảm bảo mọi thông tin luôn updated, đặc biệt cho events, weather hoặc visa changes. Full history giúp chatbot nhớ toàn bộ context khi khách chat dài nhiều lượt.
```

### Rủi ro lớn nhất của config này

```text
Cost sẽ tăng rất nhanh nếu volume conversation lớn hoặc khách chat quá dài.
```

---

## Config 3

**Tên config**:

```text
Smart Hybrid Assistant
```

### 3 Knobs

**① Model tier**:

```text
Response model:
- GPT-4o-mini cho FAQ / Guide
- DeepSeek V4 Pro cho Visa / Complaint / Itinerary

→ giá:
GPT-4o-mini: $0.15 / $0.60
DeepSeek V4 Pro: $1.74 / $3.48

Classifier model: keyword + lightweight classifier → gần như $0
```

**② Web search**:

```text
☑ ON selective — bật cho intent: Weather, Visa
```

**③ History management**:

```text
☑ Last 5
```

### Lý do nhóm chọn config này

```text
Nhóm nghĩ đây là config thực tế nhất cho production vì balance được quality và cost. Các câu FAQ đơn giản dùng model rẻ để tiết kiệm, còn các intent khó hơn như visa hoặc complaint mới dùng strong model.

Selective web search giúp tránh outdated information nhưng không làm cost tăng quá nhiều. Last 5 turns đủ để chatbot nhớ budget, family size hoặc travel style của tourist.
```

### Rủi ro lớn nhất của config này

```text
Routing sai intent có thể khiến câu hỏi khó bị gửi sang cheap model và làm giảm chất lượng trả lời.
```

---

## Config 4 (optional)

**Tên config**:

```text
Long Conversation Optimizer
```

### 3 Knobs

```text
Model: Gemini 2.5 Flash
Web: ON selective
History: Summarize every 5 turns
```

### Lý do

```text
Config này phù hợp với các conversation dài như planning full itinerary nhiều ngày. Summarization giúp giảm token cost ở các cuộc hội thoại dài nhưng vẫn giữ được context quan trọng.
```

---

## Bảng kiểm trước khi tính cost

- [ ] ≥3 configs đã đặt tên (không chỉ "Config 1/2/3")
- [ ] Mỗi config đã chốt rõ 3 knobs (không còn ô trống)
- [ ] Mỗi config có ≥2 câu lý do
- [ ] 3 configs đủ khác biệt — không phải chỉ đổi mỗi 1 knob nhỏ
- [ ] Nhóm đồng thuận đây là 3 configs đáng so sánh

**Nếu 3 configs quá giống nhau** (chỉ đổi model, knobs khác giống hệt) → quay lại tweak. Mục đích là thấy tradeoff — configs giống nhau quá → không thấy tradeoff.

Xong → mở `03-cost-calculation.md` để bắt đầu tính cost.
