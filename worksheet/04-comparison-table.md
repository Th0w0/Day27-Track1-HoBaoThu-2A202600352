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


| | Config 1 | Config 2 | Config 3 | Config 4 |
|---|---|---|---|---|
| **Tên** | Budget Backpacker Bot | Luxury Travel Concierge | Smart Hybrid Assistant | Long Conversation Optimizer |
| **① Model** | GPT-4o-mini | Claude Sonnet 4.6 | Mix: GPT-4o-mini + DeepSeek V4 Pro | Gemini 2.5 Flash |
| **② Web search** | ON selective | ON broad | ON selective | ON selective |
| **③ History** | Last 3 | Full | Last 5 | Summarize every 5 |
| **Intent classifier** | Keyword | LLM | Keyword + lightweight classifier | LLM |
| **Cost / conv (Scenario A — 4 turns)** | $0.008 | $0.061 | $0.021 | $0.017 |
| **Cost / conv (Scenario B — 7 turns)** | $0.013 | $0.108 | $0.037 | $0.028 |
| **Monthly A** (300 conv/day × 30) | $72 | $549 | $189 | $153 |
| **Monthly B** (1,200 conv/day × 30) | $468 | $3,888 | $1,332 | $1,008 |
| **vs human $4,500/mo (A)** | rẻ 62.5× | rẻ 8.2× | rẻ 23.8× | rẻ 29.4× |
| **vs human $18,000/mo (B)** | rẻ 38.5× | rẻ 4.6× | rẻ 13.5× | rẻ 17.8× |
| **Savings % (A)** | 98.4% | 87.8% | 95.8% | 96.6% |
| **Savings % (B)** | 97.4% | 78.4% | 92.6% | 94.4% |
| **Quality estimate** | Medium | High | High | Medium-High |
| **Speed estimate** | High | Low | Medium | Medium |
| **Điểm yếu chính** | Dễ quên context conversation dài | Cost tăng mạnh ở peak season | Sai routing sẽ giảm quality | Summarization thêm latency |
| **Best for** (khi nào nên dùng) | Startup nhỏ / low budget | VIP concierge service | Production thực tế balance cost-quality | Conversation dài nhiều turns |

---

## Quan sát nhanh từ bảng

Trước khi sang file recommendation, trả lời 4 câu — đây là material để present:

### Câu 1 — Config rẻ nhất là gì? Đắt nhất là gì?

```text
Rẻ nhất: Budget Backpacker Bot — monthly B = $468
Đắt nhất: Luxury Travel Concierge — monthly B = $3,888

Chênh: khoảng 8.3× lần
```

### Câu 2 — Knob nào ảnh hưởng cost nhiều nhất?

```text
Knob ảnh hưởng mạnh nhất là model tier.

Đổi từ GPT-4o-mini sang Claude Sonnet làm cost tăng khoảng 4–8× tùy scenario.
History Full vs Last 3 làm Scenario B tăng đáng kể vì mỗi turn thêm ~260 tokens.
Web search selective chỉ tăng nhẹ vài cent mỗi conversation, nhỏ hơn nhiều so với model cost.
```

### Câu 3 — Tại sao Scenario B không đắt ×4 lần Scenario A?

```text
Mặc dù Scenario B có volume ×4 và turns dài hơn, intent mix thay đổi đáng kể:
Booking + Complaint chiếm 45% conversations và được handoff sang human nên gần như không tốn LLM cost.

Vì vậy monthly cost tăng thấp hơn mức ×7 lý thuyết.
```

### Câu 4 — Có config nào AI đắt hơn human không?

```text
Không có config nào đắt hơn human baseline.

Ngay cả config premium nhất (Luxury Travel Concierge) vẫn rẻ hơn human support khoảng 4.6× ở Scenario B.
Ngoài cost thấp hơn, AI còn có lợi thế hoạt động 24/7, hỗ trợ đa ngôn ngữ và scale tốt hơn khi volume tăng.
```
---

## Bảng kiểm trước khi sang file tiếp theo

- [ ] Bảng đầy đủ — không còn ô trống
- [ ] Đã có 4 câu trả lời cho 4 quan sát ở trên
- [ ] Nhóm đồng thuận về số trong bảng (đã sanity check)

Xong → mở `05-recommendation.md` để viết recommendation cuối + chuẩn bị present.
