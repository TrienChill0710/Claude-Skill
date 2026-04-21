# CLAUDE.md — Skills & Hướng dẫn

File này chứa các skill nhỏ và hướng dẫn hành vi cho Claude trong project này.

---

## Cấu trúc

Mỗi skill được định nghĩa trong một section riêng với format:

```
## [Tên Skill]
**Kích hoạt:** <khi nào áp dụng skill này>
**Hành động:** <Claude cần làm gì>
```

---

## Skills

<!-- Thêm skill mới vào đây -->

## Hick's Law UX
**Kích hoạt:** Khi thiết kế navigation, menu, form, onboarding, hoặc bất kỳ điểm nào user phải đưa ra lựa chọn.
**Nguồn:** William Hick & Ray Hyman (1952) — lawsofux.com

**Định luật:** Thời gian để đưa ra quyết định tăng theo số lượng và độ phức tạp của các lựa chọn.

**5 nguyên tắc áp dụng:**
1. **Giảm số lựa chọn** tại các điểm time-sensitive — thanh toán, confirm action, error recovery
2. **Chia nhỏ task phức tạp** thành các bước tuần tự thay vì hiện tất cả cùng lúc
3. **Highlight lựa chọn được đề xuất** — recommended, default, most popular — để giảm cognitive load
4. **Progressive disclosure cho người mới** — ẩn advanced feature cho đến khi user thành thạo core
5. **Không oversimplify** đến mức ẩn đi chức năng quan trọng mà user thực sự cần

**Ví dụ thực tế:**
- **Google**: Trang chủ chỉ có 1 việc — gõ tìm kiếm. Mọi thứ khác bị loại bỏ
- **Apple TV Remote**: Chuyển độ phức tạp lên màn hình TV, remote chỉ có vài nút cốt lõi
- **Slack Onboarding**: Bot hướng dẫn từng bước, ẩn tính năng nâng cao cho đến khi user quen

**Checklist khi apply:**
- [ ] Màn hình này có bao nhiêu lựa chọn? Có thể giảm không?
- [ ] Task có thể chia thành nhiều bước nhỏ hơn không?
- [ ] Đã highlight option được khuyến nghị chưa?
- [ ] Onboarding có đang ẩn feature nâng cao với người mới không?
- [ ] Việc đơn giản hoá có đang ẩn đi chức năng quan trọng không?

## 10 Usability Heuristics for User Interface Design
**Kích hoạt:** Khi thiết kế mới, review, hoặc audit UI — áp dụng như checklist đánh giá toàn diện.
**Nguồn:** Jakob Nielsen — Nielsen Norman Group (1990, refined 1994)

**1. Visibility of System Status**
User luôn phải biết hệ thống đang làm gì. Phản hồi ngay lập tức, rõ ràng, đúng thời điểm.
→ Loading state, progress bar, confirmation sau action, highlight element đang active.

**2. Match Between System and Real World**
Dùng ngôn ngữ và khái niệm quen thuộc với user — không dùng jargon kỹ thuật nội bộ.
→ Icon thùng rác = xóa, icon bút chì = chỉnh sửa. Tên button khớp với hành động thực tế.

**3. User Control and Freedom**
User cần "emergency exit" rõ ràng để thoát khỏi trạng thái không mong muốn dễ dàng.
→ Undo/Redo, nút Cancel, xác nhận trước khi xóa vĩnh viễn, back button hoạt động đúng.

**4. Consistency and Standards**
Cùng một từ, hành động, element phải có ý nghĩa giống nhau ở mọi nơi trong sản phẩm.
→ Màu primary button nhất quán, terminology đồng nhất, layout pattern không thay đổi tuỳ tiện.

**5. Error Prevention**
Ngăn lỗi xảy ra còn tốt hơn xử lý lỗi. Ưu tiên xử lý các lỗi có cost cao nhất trước.
→ Disable button khi form chưa hợp lệ, confirm dialog trước action phá huỷ, smart defaults.

**6. Recognition Rather Than Recall**
Hiển thị options thay vì bắt user nhớ. Recognition dễ hơn recall — đừng lạm dụng bộ nhớ user.
→ Dropdown thay vì text field trống, recent items, context-sensitive hints, visible menu.

**7. Flexibility and Efficiency of Use**
Hỗ trợ cả novice lẫn expert — shortcut cho người dùng thành thạo mà không làm phức tạp với người mới.
→ Keyboard shortcuts, bulk actions, customizable workflow, quick-access cho thao tác thường dùng.

**8. Aesthetic and Minimalist Design**
Mỗi element thừa là đối thủ cạnh tranh với element quan trọng. Loại bỏ mọi thứ không hỗ trợ mục tiêu chính.
→ Không thêm decoration vô nghĩa, không hiển thị info hiếm khi dùng ở vị trí nổi bật, whitespace là vũ khí.

**9. Help Users Recognize, Diagnose, and Recover from Errors**
Error message = ngôn ngữ thường, chỉ rõ vấn đề, đề xuất giải pháp cụ thể. Không dùng error code.
→ "Email không hợp lệ — thử lại dạng name@example.com" thay vì "Error 422".

**10. Help and Documentation**
Hệ thống lý tưởng không cần documentation. Khi cần — searchable, task-focused, đặt đúng context, có bước cụ thể.
→ Tooltip inline, empty state hướng dẫn, progressive disclosure thay vì manual dài.

**Checklist audit nhanh:**
- [ ] User có biết hệ thống đang ở trạng thái nào không? *(#1)*
- [ ] Ngôn ngữ có khớp với cách user nghĩ không? *(#2)*
- [ ] Có lối thoát rõ ràng cho mọi action không? *(#3)*
- [ ] Terminology và pattern có nhất quán toàn sản phẩm không? *(#4)*
- [ ] Có action nào dễ gây lỗi nghiêm trọng mà chưa có guard không? *(#5)*
- [ ] User có đang phải nhớ thứ gì thay vì nhìn thấy không? *(#6)*
- [ ] Expert user có thao tác nhanh hơn được không? *(#7)*
- [ ] Có element nào thừa đang cạnh tranh sự chú ý không? *(#8)*
- [ ] Error message có giải thích được vấn đề và cách fix không? *(#9)*
- [ ] Khi user bị kẹt, có help đúng chỗ đúng lúc không? *(#10)*

## Dont make me think
**Kích hoạt:** Khi thiết kế, review, hoặc cải thiện bất kỳ UI/UX nào — web, mobile, app, form, flow.
**Nguồn:** Nguyên lý từ "Don't Make Me Think" — Steve Krug

**Luật tối thượng:** Mỗi dấu hỏi trong đầu user là một thất bại của design. Mục tiêu là zero cognitive friction.

---

**1. User không đọc — họ scan**
- 79% user scan trang, chỉ 16% đọc từng chữ; trung bình chỉ đọc 20% nội dung
- Thiết kế cho scanner: visual hierarchy rõ ràng, keyword nổi bật, một ý mỗi đoạn
- Nội dung: cắt một nửa số chữ, rồi cắt tiếp một nửa nữa
- Dùng inverted pyramid — kết luận trước, chi tiết sau

**2. User "satisfice" — không tối ưu, chỉ đủ dùng**
- User chọn option đầu tiên trông có vẻ hợp lý, không tìm option tốt nhất
- Đừng ép user phải so sánh — làm lựa chọn đúng trở nên hiển nhiên nhất
- User mò mẫm qua sản phẩm, không đọc hướng dẫn — thiết kế phải tự giải thích được

**3. Ba luật thiết kế của Krug**
1. **Self-evident** — User hiểu ngay mục đích của trang/màn hình mà không cần đọc
2. **Obvious navigation** — Mỗi click là lựa chọn tự tin, không cần suy nghĩ
3. **Concise content** — Loại bỏ mọi chữ không cần thiết, không ngoại lệ

**4. Navigation & Wayfinding**
- Luôn có nút Home rõ ràng — đây là "exit door" khi user bị lạc
- Back button phải hoạt động đúng — đây là safety net quan trọng nhất
- User phải luôn biết: đang ở đâu, đến được đâu, và quay lại từ đâu
- Dùng visual landmark để tạo orientation — mỗi màn hình phải có identity riêng

**5. Giảm cognitive load ở mọi điểm chạm**
- Convention > sáng tạo — dùng pattern quen thuộc thay vì reinvent
- Consistency tuyệt đối — layout, terminology, behavior phải giống nhau trên toàn sản phẩm
- Không bắt user nhớ thông tin từ màn hình trước
- Error phải tự giải thích: nói rõ vấn đề gì và cách fix thế nào

**6. Mobile — càng strict hơn**
- Mobile = ít space, nhiều distraction, ngón tay không chính xác bằng chuột
- Self-evident phải cao hơn desktop — không có tooltip, không có hover state
- Tap target đủ lớn, spacing đủ rộng để không tap nhầm
- Chỉ hiện thông tin cần thiết nhất cho context hiện tại

**7. Usability testing thực tế**
- Test 3 user mỗi tháng — đủ để phát hiện vấn đề nghiêm trọng, không cần ngân sách lớn
- Quan sát user thực hiện task thực — đừng giải thích, đừng can thiệp
- Một buổi test tìm ra vấn đề thật còn hơn 10 buổi họp debate nội bộ

**Checklist khi apply skill này:**
- [ ] User có hiểu trang này dùng để làm gì trong 3 giây không?
- [ ] Có dấu hỏi nào trong flow mà user có thể gặp không?
- [ ] Nội dung có thể cắt ngắn thêm không?
- [ ] Navigation có cho user biết họ đang ở đâu không?
- [ ] Có convention nào đang bị phá vỡ mà không có lý do không?
- [ ] Mobile experience có tự giải thích không cần hướng dẫn không?

## Judge UI
**Kích hoạt:** Khi được yêu cầu đánh giá, review, hoặc critique một giao diện UI/UX.
**Hành động:** Áp dụng framework 3 bước theo thứ tự:

**Bước 1 — Hiểu Context trước khi phán xét**
- Xác định: màn hình này giúp user hoàn thành task gì?
- Mental model: user kỳ vọng thấy gì? Họ ưu tiên tốc độ hay sự tự tin?

**Bước 2 — Đánh giá Goal Achievement (quan trọng nhất)**
Dùng 5-level UX hierarchy, theo thứ tự ưu tiên:
1. **Functional** — Feature có tồn tại và giải quyết nhu cầu user không?
2. **Reliable** — Feature hoạt động ổn định, đáng tin cậy không?
3. **Usable** — Rõ ràng, dễ hiểu, user hoàn thành được mục tiêu không?
4. **Pleasurable** — Trải nghiệm có thú vị không? (chỉ xét sau khi 1-3 đạt)
5. **Meaningful** — Có tạo gắn kết dài hạn không? (chỉ xét sau khi 1-3 đạt)

**Bước 3 — Đánh giá IA & Interaction Design**
- **Information hierarchy**: Nội dung có tổ chức logic? User tìm được thứ họ cần không?
- **Terminology**: Thuật ngữ có nhất quán, quen thuộc, phù hợp đối tượng không?
- **Proximity & grouping**: Thông tin liên quan có được đặt gần nhau không?
- **Consistency**: Style, layout, positioning có đồng nhất qua các element tương tự không?
- **Affordance**: User có dễ nhận ra element nào interactive và biết cách dùng không?
- **Visual Design**: Số lượng màu sắc và font có phù hợp mục đích màn hình không?
- **Accessibility**: Contrast ratio text/background, font size, color-blind friendly?
- **Component usage**: Component được chọn có phù hợp context hay là overkill?

**Nguyên tắc khi đánh giá:**
- Không suy đoán về constraint ẩn — business logic phức tạp có thể justify lựa chọn trông suboptimal
- Ưu tiên functional over aesthetic — xấu mà dùng được tốt hơn đẹp mà không dùng được
- Dùng tiêu chí cụ thể, không dùng cảm xúc — tránh "không thân thiện" mà nói rõ vấn đề cụ thể là gì
- Inconsistency nhỏ tích lũy thành friction lớn — mỗi 1-2 giây xử lý thừa đều có giá

## Canvas Design
**Kích hoạt:** Khi được yêu cầu tạo visual art, design canvas, hoặc tác phẩm thiết kế chất lượng cao.
**Hành động:**
- Thực hiện theo 2 phase:
  1. **Design Philosophy** (.md): Viết manifesto thẩm mỹ 4-6 đoạn — articulate worldview qua form, space, color, composition
  2. **Canvas Expression** (.pdf hoặc .png): Diễn giải philosophy thành visual — 90% design, 10% text
- Nguyên tắc cốt lõi:
  - Visual communication over text — thông tin nằm trong design, không phải đoạn văn
  - Typography tối thiểu — text chỉ là gesture thị giác, không phải khối giải thích
  - Craftsmanship tuyệt đối — tác phẩm phải trông như được làm bởi người đỉnh nhất lĩnh vực
  - Không overlap, margin chuẩn, formatting hoàn hảo
- Refinement: làm composition hiện tại cohesive hơn, không thêm elements
- Chuẩn đầu ra: museum-quality, có thể trưng bày như một artifact

## Brand Guidelines
**Kích hoạt:** Khi được yêu cầu áp dụng brand identity, định dạng tài liệu, presentation, hoặc visual content theo chuẩn thương hiệu Anthropic.
**Hành động:**
- Áp dụng color palette chính thức:
  - Dark: `#141413` | Light: `#faf9f5`
  - Accent: Orange, Blue, Green (cycling cho non-text elements)
- Typography:
  - Headings (≥24pt): **Poppins** (fallback: Arial)
  - Body text: **Lora** (fallback: Georgia)
- Dùng RGB color values để đảm bảo độ chính xác màu sắc
- Áp dụng được cho: presentations, documents, visual artifacts
- Không cần cài font thêm — Poppins và Lora có sẵn trên hầu hết hệ thống

## Theme Factory
**Kích hoạt:** Khi được yêu cầu áp dụng theme, styling, hoặc chọn màu sắc/font cho slides, docs, reports, hoặc HTML landing page.
**Hành động:**
- Hiển thị 10 theme có sẵn để người dùng chọn:
  1. Ocean Depths, 2. Sunset Boulevard, 3. Forest Canopy, 4. Modern Minimalist, 5. Golden Hour
  6. Arctic Frost, 7. Desert Rose, 8. Tech Innovation, 9. Botanical Garden, 10. Midnight Galaxy
- Nếu không có theme phù hợp, tạo custom theme theo cùng spec (color palette với hex codes + font pairings)
- Quy trình: hiển thị showcase → người dùng chọn → xác nhận → áp dụng màu sắc và font tương ứng
- Mỗi theme bao gồm: color palette đầy đủ hex codes + font pairing chuyên nghiệp
- Áp dụng được cho: slides, docs, reports, HTML landing pages

## Implement Design
**Kích hoạt:** Khi được yêu cầu chuyển đổi thiết kế Figma thành code (implement, build from Figma, pixel-perfect, v.v.).
**Hành động:**
1. **Extract Node ID** từ Figma URL (dạng `?node-id=1-2`)
2. **Fetch Design Context** dùng `get_design_context()` để lấy layout, typography, màu sắc, cấu trúc component
3. **Capture Visual Reference** dùng `get_screenshot()` để dùng làm chuẩn so sánh
4. **Download Assets** trực tiếp từ Figma MCP server (dùng localhost source)
5. **Translate to Project Conventions** — áp dụng framework, design token, và component pattern của project
6. **Achieve Visual Parity** — khớp chính xác spacing, typography, màu sắc, responsive behavior
7. **Validate Against Figma** — kiểm tra toàn bộ checklist trước khi hoàn thành
- Không copy code style từ Figma MCP output — chỉ dùng nó như mô tả design và behavior
- Tái sử dụng component có sẵn, áp dụng design token của project, không tạo duplicate

## Frontend Design
**Kích hoạt:** Khi được yêu cầu tạo hoặc cải thiện giao diện web, UI component, hoặc bất kỳ tác vụ thiết kế frontend nào.
**Hành động:**
- Trước khi code, phân tích: mục đích, đối tượng người dùng, tone, và yếu tố khác biệt
- Chọn một hướng thẩm mỹ rõ ràng (từ "brutally minimal" đến "maximalist") — không làm trung dung
- Typography: chọn font đặc trưng, tránh font hệ thống mặc định
- Màu sắc: xây dựng palette với màu chủ đạo + accent sắc nét, tránh phân tán màu
- Motion: chỉ thêm hiệu ứng có chủ đích — staggered reveals, scroll-triggered effects
- Layout: ưu tiên bất đối xứng, overlap, và quản lý negative space
- Tránh: font cliché (Inter/Roboto mặc định), layout grid đều đều, màu pastel nhạt vô hồn, animation thừa
- Độ phức tạp của code phải tương xứng với vision: maximalist cần animation tinh vi, minimalist cần spacing và typography chính xác
