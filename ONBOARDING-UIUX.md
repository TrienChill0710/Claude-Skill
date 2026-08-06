# Onboarding — Quy trình làm việc UIUX (dành cho member mới)

> Đọc file này TRƯỚC khi bắt đầu bất kỳ WIRE nào. Đây là quy trình con người (bạn + Claude), không phải tài liệu kỹ thuật cho AI — bản kỹ thuật đầy đủ nằm ở `.claude/agents/agent-ds-author.md` (Claude tự đọc, bạn không cần thuộc).

## 1. Bạn cần biết gì trước khi bắt đầu

- Bạn **không cần tự viết Markdown** (`SCREEN-*.md`, `COMP-*.md`). Việc của bạn là **thiết kế visual** trên file mockup HTML — Claude lo phần còn lại (audit, viết tài liệu, verify, đóng gói handoff).
- Mọi quyết định/fix không hiển nhiên đều được ghi vào `Execution/tracking/decisions.md` — nếu không chắc 1 màn được author ra sao, đọc file đó trước khi hỏi.
- Nếu Claude dừng lại hỏi bạn (STOP-AND-ASK) — thường là vì WIRE thiếu chi tiết hoặc có mâu thuẫn với mockup thật. Trả lời rõ ràng, đừng đoán giúp Claude.

## 2. Quy trình 3 bước (lặp lại cho mỗi WIRE / mỗi wave)

```
   PO/BA sync WIRE mới về (từ domain)
              │
              ▼
   BƯỚC 1 — Gen mockup (Claude làm, bạn prompt)
   "Vừa sync WIRE mới ... hãy gen mockup cho tôi"
   → mockup HTML mới, khớp visual language DS hiện có
              │
              ▼
   BƯỚC 2 — Bạn edit visual (bạn làm, thủ công)
   Sửa trực tiếp trên file mockup HTML — màu, layout,
   spacing, copy tạm... tuỳ ý, đây là bước sáng tạo của bạn
              │
              ▼
   BƯỚC 3 — Full pipeline tới handoff (Claude làm, bạn prompt)
   "Tôi edit xong ... chạy full pipeline cho tôi"
   → audit COMP/token, SCREEN-*.md, GEN-CHECK verify,
     sẵn sàng handoff cho dev
```

### Bước 1 — Prompt mẫu (gen mockup từ WIRE mới)

```
Vừa sync WIRE mới từ domain xong: <WIRE-ID-1, WIRE-ID-2, ...> (family: <tên family>).

Hãy làm cho tôi:
1. Đọc từng WIRE ở _inputs/domain/product/ux/ (chỉ đọc, không sửa).
2. Xác định target platform (web/app/cả 2), /spawn-ds-author cho đúng DS.
3. Grep Component index trước — ưu tiên tái dùng COMP đã có, chỉ tạo COMP mới khi thật sự cần.
4. Dựng mockup HTML mới khớp 1:1 visual language với mockup đã APPROVED gần nhất trong cùng DS.
5. Gắn đúng data-ds-component/data-ds-variant cho mọi element dùng component.
6. Screenshot-verify so với 1 mockup tham chiếu trước khi báo xong.

KHÔNG tự edit nội dung ngoài WIRE mô tả — thiếu chi tiết thì dừng lại hỏi tôi.
```

### Bước 2 — Bạn tự làm (không cần Claude)

Mở file mockup `.html` vừa được tạo, sửa trực tiếp bằng mắt/tay — giống thiết kế bình thường. Không có quy tắc ràng buộc ở bước này, đây là bước của bạn.

### Bước 3 — Prompt mẫu (full pipeline tới handoff)

```
Tôi vừa edit visual xong trên mockup: <đường dẫn file(s) đã sửa>.

Hãy chạy đủ pipeline sau, đúng chuẩn:
1. Audit 2 chiều component/token (mockup = ground truth nếu lệch COMP doc).
2. Đồng bộ component-gallery.html + screens/*.json nếu COMP đổi.
3. Author/update SCREEN-*.md (mode DEV-HANDOFF), verify pixel-level so mockup thật.
4. Dựng 1 GEN-CHECK reverse-generate từ SCREEN.md vừa viết, verify bằng screenshot thật.
5. Log quyết định + bump version, báo tôi kết quả kèm đường dẫn GEN-CHECK để tôi tự kiểm tra.
```

(2 prompt trên là bản rút gọn — bản đầy đủ + lý do từng bước xem lịch sử hội thoại đã lưu, hoặc hỏi Claude "cho tôi lại 2 prompt mẫu" — Claude sẽ tự nhớ nhờ file này + `agent-ds-author.md`.)

## 3. Thế nào là "đạt chuẩn"

Bạn không cần nhớ chi tiết kỹ thuật — chỉ cần biết Claude sẽ tự kiểm tra các điều sau trước khi báo "xong" (nếu Claude bỏ qua, đó là bug, nhắc Claude đọc lại `agent-ds-author.md`):

- Mọi component/token dùng trong tài liệu phải khớp đúng những gì mockup thật đang dùng (không đoán).
- Asset ảnh/icon phải là file/dữ liệu thật, không phải placeholder hay tự vẽ tay.
- File kiểm tra (GEN-CHECK) phải được chụp ảnh và so trực tiếp với mockup thật trước khi báo xong.
- Mỗi quyết định không hiển nhiên phải có 1 dòng trong `decisions.md` — nếu không thấy dòng nào cho 1 thay đổi lớn, đó là dấu hiệu bước đó bị bỏ sót.

## 4. Khi có lỗi / nghi ngờ kết quả sai

1. Mở file `GEN-CHECK-*.html` (trong `design-systems/<ds>/mockups/`) cạnh mockup thật — so trực tiếp bằng mắt.
2. Nếu nghi ngờ 1 giá trị CSS cụ thể (màu, cỡ chữ...) — dùng DevTools **element picker** (Cmd+Shift+C trên Chrome) để inspect đúng 1 phần tử ở cả 2 file, đừng click theo toạ độ ước lượng (dễ so nhầm 2 phần tử khác nhau).
3. Báo Claude kèm ảnh chụp/giá trị cụ thể — Claude sẽ tự script-diff trước khi sửa code, không đoán mù.

## 5. Tài liệu liên quan

| File | Vai trò |
|---|---|
| `CLAUDE.md` | Router — role/stage/lệnh slash command |
| `.claude/agents/agent-ds-author.md` | **Rule kỹ thuật đầy đủ** (RULE 0/0a/0b/0c) — Claude tự đọc mỗi lần |
| `_shared/definitions/AUTHORING-RULES.md` | Quy ước viết token/markup dùng chung |
| `Execution/tracking/decisions.md` | Lịch sử mọi quyết định không hiển nhiên |
| `Execution/tracking/sync-log.md` | Lịch sử mỗi lần push sang SPECS |
| `Plan/EXPORT-IMPORT-FRAMEWORK.md` | Cách mang quy trình này sang project mới |
