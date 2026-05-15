# 01 · Base Flow + Chốt 3 Knobs

> **Mục tiêu**: Hiểu chatbot hoạt động ra sao ở mức base (không chọn config gì) — và xác định 3 knobs nhóm sẽ tweak ở các bước sau.
>
> **Thời gian**: 7 phút (trong 15 phút phần Setup)

---

## Bước 1 — Đọc base flow trong cost reference card

Mở file `cost-reference-card.md` ở phần **2. Base Flow** — xem flow chatbot mặc định. Đây là cấu trúc mọi config sẽ build dựa trên.

Đọc xong, tự kiểm tra hiểu:

- Khi tourist gửi tin nhắn, AI làm gì đầu tiên?
- 5 intent dẫn đến 5 hành động khác nhau — hành động nào tốn LLM, hành động nào không?
- Sau khi route, AI ráp gì lại để generate response?

Nếu chưa hiểu → quay lại đọc lại 1 lần nữa. Đừng đi tiếp khi còn mơ hồ.

---

## Bước 2 — Vẽ lại flow theo cách hiểu của nhóm

Vẽ flow ra giấy hoặc trên bảng (1 thành viên vẽ, cả nhóm góp ý). Có thể dùng ASCII đơn giản:

```text
Tourist opens website chatbot
          │
          ▼

┌─────────────────────────────┐
│ Detect user need            │
│ (What is the tourist asking?)│
└─────────────┬───────────────┘
              │
    ┌─────────┼─────────┬─────────┐
    ▼         ▼         ▼         ▼

 Travel Info  Live Info  Booking  Problems
 (food, city, (weather,  request  / bad exp
 itinerary)   events)             

    │            │         │         │
    ▼            ▼         ▼         ▼

 Use KB      Search Web  Send to  Human support
 + RAG       for latest  Sales    / manager
             updates

    │            │
    └──────┬─────┘
           ▼

┌─────────────────────────────┐
│ Build AI context            │
│                             │
│ - System instructions       │
│ - Previous messages         │
│ - Tourist current message   │
│ - KB results                │
│ - Web results (if needed)   │
└─────────────┬───────────────┘
              │
              ▼

┌─────────────────────────────┐
│ AI generates response       │
│                             │
│ - Answer tourist question   │
│ - Recommend places          │
│ - Ask follow-up questions   │
│ - Or transfer to human      │
└─────────────────────────────┘


```

Khi vẽ, đảm bảo flow có 4 điểm:

1. **Intent classification** — phân loại ý định
2. **Route theo intent** — 5 nhánh đi đâu (RAG / Web search / Handoff / Escalate)
3. **Context assembly** — ráp system prompt + history + RAG + web (nếu bật) + user msg
4. **Response generation** — model tạo câu trả lời

Nếu nhóm vẽ thiếu 1 trong 4 bước → bổ sung trước khi đi tiếp.

---

## Bước 3 — Xác định 3 Knobs

3 knobs là 3 quyết định thiết kế nhóm có thể tweak. Mỗi config nhóm thiết kế = 1 bộ chọn tại 3 knobs này.

Trước khi điền vào ô bên dưới, đọc nhanh mục **3. Decision Points** của `cost-reference-card.md`. Sau đó tự hỏi:

- Knob 1 — Model tier: model rẻ và model mạnh chênh bao nhiêu lần? Có thể mix theo intent không?
- Knob 2 — Web search: intent nào *cần* real-time? intent nào không cần?
- Knob 3 — History: 7 lượt chat cuối đắt hay rẻ? Cắt history có rủi ro gì?
### Knob 1 — Model tier

**Suy nghĩ của nhóm:**

```text
Nhóm thấy phần lớn tourist hỏi các câu khá đơn giản như địa điểm, thời tiết, food, budget nên không cần model quá mạnh cho mọi trường hợp. Tuy nhiên, các câu liên quan đến visa, complaint hoặc itinerary dài sẽ cần model tốt hơn để trả lời tự nhiên và chính xác hơn.

Nhóm nghĩ nên dùng mix model:
- Cheap model cho intent classification và FAQ đơn giản
- Strong hoặc Mid model cho visa / complaint / planning itinerary

Cách này giúp giảm cost nhưng vẫn giữ được chất lượng ở các tình huống khó.
```

---

### Knob 2 — Web search

**Suy nghĩ của nhóm:**

```text
Nhóm nghĩ web search nên bật selective thay vì broad.

Lý do:
- Weather gần như bắt buộc cần realtime data
- Visa policy có thể thay đổi nên đôi khi cần web search để tránh trả lời outdated
- Các câu hỏi về destinations, food, culture thì KB + RAG là đủ

Nếu bật web search cho mọi intent sẽ tăng cost không cần thiết và làm chatbot chậm hơn.
```

---

### Knob 3 — History management

**Suy nghĩ của nhóm:**

```text
Nhóm thấy tourist thường nhắc lại thông tin cũ như budget, số ngày đi hoặc travelling with family. Nếu chatbot quên các thông tin này thì trải nghiệm sẽ khá tệ.

Scenario A chỉ khoảng 4 turns nên full history chưa quá tốn. Nhưng Scenario B có thể lên 7 turns hoặc hơn, mỗi turn tăng thêm khoảng 260 tokens nên cost sẽ tăng khá nhanh.

Nhóm nghĩ Last 5 turns là lựa chọn cân bằng nhất:
- Đủ nhớ context quan trọng
- Không quá tốn token như full history
- Hầu hết conversation du lịch không quá dài
```
---
## Bước 4 — Sơ bộ nhóm muốn thử những combo nào?

### Combo 1 (định hướng cheap)

```text
Model: GPT-4o-mini
Web: OFF
History: Last 3 turns

(Tên dự kiến: Budget Saver)
```

---

### Combo 2 (định hướng premium)

```text
Model: Claude Sonnet 4.6
Web: ON broad
History: Full history

(Tên dự kiến: Premium Travel Assistant)
```

---

### Combo 3 (định hướng balanced / smart mix)

```text
Model: Mix
- GPT-4o-mini cho classification + FAQ
- DeepSeek V4 Pro cho visa / itinerary / complaint

Web: ON selective
History: Last 5 turns

(Tên dự kiến: Smart Hybrid)
```

---

### Combo 4 (optional)

```text
Model: Gemini 2.5 Flash
Web: ON selective
History: Summarize every 5 turns

(Tên dự kiến: Long Trip Optimized)
```

---

## Bảng kiểm trước khi sang file tiếp theo

- [ ] Đã vẽ flow base có đủ 4 bước (Intent → Route → Context → Response)
- [ ] Hiểu Booking + Khiếu nại = $0 LLM cost (chuyển con người)
- [ ] Đã phác thảo ≥3 combo khác nhau (chưa cần chi tiết)
- [ ] Nhóm đồng thuận về hướng đi mỗi combo

Xong → 10:25 chuyển sang **Main phase**. Mở `02-config-design.md`.
