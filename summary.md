# CR Flow — AI Chat UX Conversation Summary

## Context

**Màn hình:** Product detail edit page (Dropship Products)
**Trigger:** User đọc banner "What do you want to improve this product page?" → click "Start now" → vào AI Mode editor
**Goal:** Thiết kế UX flow cho AI chat giúp user tăng CR và AOV cho sản phẩm cụ thể đang xem

---

## Phần 1 — Suggestion chips dưới chat box

### Yêu cầu ban đầu (tiếng Việt)
2 goal muốn suggest:
1. Giúp tăng CR cho sản phẩm này
2. Giúp tăng AOV cho sản phẩm này

### Iteration 1 — Generic outcome language
> Tôi muốn nhiều khách mua hàng hơn

> Tôi muốn mỗi đơn hàng có giá trị cao hơn

### Iteration 2 — Link với sản phẩm cụ thể
> Tại sao khách xem nhưng không mua sản phẩm này?

> Làm sao để khách chi nhiều hơn khi mua sản phẩm này?

**Lý do cải tiến:** "sản phẩm này" tạo cảm giác AI đang phân tích đúng sản phẩm user đang mở, không phải tư vấn chung chung.

### Iteration 3 — Tiếng Anh (final)

**Chip 1 — CR:**
> How do I get more visitors to actually buy this product?

**Chip 2 — AOV:**
> How do I get customers to spend more when buying this product?

**Lý do:**
- "actually buy" — giải quyết ambiguity, rõ là đang nói về conversion (người xem → người mua), không phải mua lại
- "spend more when buying" — "when buying" anchor vào moment of purchase, tránh hiểu nhầm là mua thường xuyên hơn
- Cả hai giữ "this product" để AI có cảm giác đang phân tích đúng sản phẩm

---

## Phần 2 — AI Chat Response Flow (Kịch bản)

### Flow tổng quan
1. User click chip → thành user chat prompt
2. AI analyze product page
3. AI hiển thị change plan
4. User review / edit plan
5. User nhấn Implement → AI implement
6. User xem result → Done

---

### State 1 — User sends prompt

```
[User bubble]
How do I get more visitors to actually buy this product?
```

---

### State 2 — AI analyzing (loading)

```
[AI bubble — với animated indicator]

🔍 Analyzing your product page...

▪ Reading product content
▪ Checking page structure
▪ Identifying conversion gaps
```

*Khoảng 2–3 giây, sau đó transition sang State 3*

---

### State 3 — AI trả kết quả + Change Plan

```
[AI bubble]

I found 4 issues likely hurting your conversion rate.
Here's what I'd change:
```

```
┌─────────────────────────────────────────────┐
│ CHANGE PLAN · 4 improvements                │
├─────────────────────────────────────────────┤
│ ☑  1. Rewrite product title                 │
│    Current title is generic — missing the   │
│    key benefit that triggers purchase.      │
│    Impact: High                             │
├─────────────────────────────────────────────┤
│ ☑  2. Add social proof section              │
│    No reviews visible above the fold.      │
│    Buyers need validation before deciding. │
│    Impact: High                             │
├─────────────────────────────────────────────┤
│ ☑  3. Reorder description bullets           │
│    Benefits buried — features shown first. │
│    Lead with outcomes, not specs.           │
│    Impact: Medium                           │
├─────────────────────────────────────────────┤
│ ☑  4. Add urgency signal near Buy button    │
│    Nothing nudges undecided visitors.       │
│    A stock/time cue reduces drop-off.       │
│    Impact: Medium                           │
└─────────────────────────────────────────────┘

[  Edit plan  ]          [  Implement all →  ]
```

---

### State 4 — User nhấn "Implement all"

```
[AI bubble]

Applying changes to your product page...

✅ Title rewritten
✅ Social proof section added
⏳ Reordering description...
○  Adding urgency signal
```

*Preview panel bên phải live-update theo từng item*

---

### State 5 — Done

```
[AI bubble]

All 4 changes applied. Your page has been updated.

You can review each change in the editor,
or undo all if anything looks off.

[  Review changes  ]     [  Undo all  ]
```

---

## Ghi chú thiết kế

**Change Plan card:**
- Checkbox per item → user có thể deselect trước khi implement
- "Edit" per item → mở inline edit nếu user muốn tweak copy trước khi apply
- Impact badge (High/Medium) → giúp user prioritize nếu không muốn implement tất cả

**Preview panel (bên phải):**
- Live-update trong khi AI implement — user thấy thay đổi xảy ra real-time
- Không cần navigate đi đâu, mọi thứ xảy ra trong cùng màn hình

**"Undo all" luôn visible sau implement** — safety net quan trọng nhất, tránh user sợ thử.
