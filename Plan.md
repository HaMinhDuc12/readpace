# Plan.md — ReadPace: Giao diện đọc thích ứng cho người đọc dễ mất tập trung

## 1. Giới thiệu

**1.1. Tên đồ án:** ReadPace — Giao diện đọc thích ứng giúp duy trì tập trung khi đọc văn bản dài

**1.2. Vấn đề:**
Người đọc thường xuyên bị mất chỗ đang đọc và phải đọc đi đọc lại cùng một đoạn khi đọc văn bản dài trên màn hình, do mật độ chữ dày đặc gây quá tải nhận thức (cognitive overload).

**1.3. Tại sao vấn đề này đáng giải quyết:**
Đây là vấn đề HCI kinh điển: sự không tương thích (mismatch) giữa mental model của người đọc và cách thông tin được trình bày. Các ứng dụng đọc hiện tại (Kindle, Medium, trình duyệt...) đều thiết kế theo hướng "one-size-fits-all", không thích ứng theo tốc độ và khả năng tập trung của từng người dùng. Hậu quả là người đọc mất thời gian đọc lại, giảm hiệu suất tiếp thu nội dung, và dễ bỏ dở tài liệu giữa chừng.

**1.4. Đối tượng người dùng:**
Người dùng chính là người đọc thường xuyên — sinh viên ôn thi, nhân viên văn phòng đọc báo cáo, người đọc truyện/tiểu thuyết dài kỳ — có thói quen đọc văn bản dài trên màn hình và tự nhận thấy hay mất tập trung hoặc mất chỗ đang đọc trong quá trình đọc. Tiêu chí chọn 5 end-users phỏng vấn: đọc liên tục ≥ 20–30 phút/ngày trên màn hình, tự nhận thấy thường phải đọc lại đoạn văn hoặc mất chỗ đang đọc.

**1.5. Bối cảnh sử dụng:**
Đọc tài liệu học thuật, bài báo dài, hoặc truyện/tiểu thuyết trên trình duyệt web.

**1.6. Ràng buộc:**
Nền tảng web-based, ưu tiên desktop/laptop cho bản MVP vì cơ chế cuộn/focus dễ kiểm soát hơn trên màn hình lớn. Không dùng eye-tracking làm cơ chế chính do sai số 50–150px và cần calibration phức tạp (WebGazer.js/MediaPipe); cơ chế chính dùng scroll-behavior kết hợp tốc độ đọc cá nhân hoá làm proxy đáng tin cậy. Thời gian thực hiện: 11 tuần, 4 thành viên.

---

## 2. Tài liệu liên quan (Related Work)

| Sản phẩm | Cách tiếp cận | Ưu điểm | Khoảng trống so với ReadPace |
|---|---|---|---|
| Microsoft Immersive Reader | Line focus (tô đậm 1-3 dòng), tách âm tiết, giãn cách chữ, đọc to | Miễn phí, tích hợp Office, hỗ trợ đọc tốt | Chế độ focus là tĩnh (bật/tắt thủ công), không tự cuộn theo nhịp đọc cá nhân |
| BeeLine Reader | Gradient màu chuyển dần theo dòng để mắt dễ dò đúng dòng tiếp theo | Đơn giản, nhẹ, giảm lỗi nhảy dòng | Không có focus window (blur), không tự động cuộn, không thích ứng theo tốc độ người dùng |
| Speechify | Text-to-speech, điều chỉnh tốc độ đọc | Giải quyết vấn đề bằng cách nghe thay vì đọc | Không giải quyết quá tải thị giác cho người vẫn muốn đọc bằng mắt |
| Readwise (Reader) | Highlight, lưu bài đọc, ôn lại theo spaced repetition | Tốt cho việc ghi nhớ/ôn tập sau khi đọc | Không hỗ trợ tập trung trong lúc đang đọc, chỉ hỗ trợ giai đoạn sau |

**2.1. Khoảng trống mà ReadPace lấp đầy:**
Chưa có sản phẩm nào kết hợp cuộn tự động theo tốc độ đọc cá nhân hoá với cửa sổ lấy nét (focus window) động thành một cơ chế liền mạch duy nhất. Đây là điểm mấu chốt mà ReadPace tập trung giải quyết, thay vì lặp lại những gì Immersive Reader hay BeeLine Reader đã làm.

---

## 3. Phương pháp

### 3.1. Mô hình thiết kế áp dụng

**Giai đoạn Discovery — Diverge:**
Nhóm đã tổ chức họp lần 1, thực hiện ánh xạ khái niệm (concept mapping) cho chủ đề "Việc đọc", phát sinh các nhánh: Môi trường, Vật lý, Người, Kỹ năng đọc, Sách, Công cụ, Ngôn ngữ, Nội dung, Trạng thái đọc (xem sơ đồ đính kèm — `conceptual_mapping-Page-2_drawio.png`).

**Giai đoạn Discovery — Converge:**
Từ sơ đồ trên, nhóm chọn ra các nhánh liên quan trực tiếp đến vấn đề nguyên tố (mục 1.2) để tiếp tục khai thác ở bước tiếp theo:
- Kỹ năng đọc → Sự tập trung, Tốc độ đọc
- Vật lý → Thao tác tay (Cuộn màn hình), Khoảng cách mắt, Tư thế đọc
- Nội dung → Hình thức trình bày → Cỡ chữ, Kiểu chữ, Giãn cách các chữ/dòng
- Môi trường → Không Gian → Bị tác động (xao nhãng từ ngoại cảnh)
- Trạng thái đọc → Chán, giác ngộ/say mê (dùng làm chỉ số tự đánh giá cảm xúc khi kiểm thử)

Các nhánh còn lại (Người/Đọc giả, Ngôn ngữ, Thể loại nội dung, Sách/Công cụ vật lý như Kính, Kindle...) nằm ngoài phạm vi giải quyết trực tiếp của ReadPace.

**Giai đoạn Conception, Prototyping, Evaluation:**
*(Sẽ bổ sung sau khi có kết quả phỏng vấn 5 end-users — mục 3.2)*

### 3.2. User Discovery

Kết hợp giữa hai phương pháp là “Ask” và “Observe” để khảo sát và khám phá người dùng.

### Ask
Trong phương pháp “Ask” ta dùng bảng câu hỏi để khảo sát số lượng lớn dữ liệu người dùng và phỏng vấn trực tiếp để khai thác thông tin các người dùng cốt yếu nhằm xây dựng các chức năng cho hệ thống.

**Bảng câu hỏi sàng lọc, gom nhóm đối tượng**
 
1.	Bạn thuộc nhóm nào? (Sinh viên / Người đi làm / Khác) 
2.	Trung bình mỗi ngày bạn đọc sách, truyện bao nhiêu phút trong một ngày? (Dưới 20 phút / Từ 20 đến 60 phút / Từ 61 đến 180 phút/ Trên 180 phút) 
3.	Bạn có tự nhận thấy mình khó tập trung khi đọc văn bản dài không? (Có hẳn / Thỉnh thoảng / Hiếm khi / Không bao giờ)

![Picture1](https://lh3.googleusercontent.com/d/1RcjrWKg1Kr08VdQ4yXkx6X5FfhpkzkD5)
![Picture2](https://lh3.googleusercontent.com/d/19e6a8_4g77y6KDf19jn4QOZGyS4ZyEPs)
![Picture4](https://lh3.googleusercontent.com/d/1diTEpvjiL884Ego1BMu__l1Fj1cZz5Rz)

**Bảng câu hỏi thăm dò hành vi đọc của đọc giả**

Thang 1-5 (1 Hoàn toàn không đồng ý- 2 Không đồng ý lắm- 3 Bình thường- 4 Đồng ý- 5 Rất đồng ý)

4.	Bạn thường phải đọc lại một đoạn văn nhiều lần mới hiểu.
5.	Bạn hay bị mất chỗ đang đọc khi nhìn ra chỗ khác rồi quay lại.
6.	Bạn thường bỏ dở câu truyện/đoạn văn giữa chừng vì mất tập trung.
7.	Bạn thấy các trang truyện/tài liệu hiện tại quá dày đặc chữ, gây ngợp.
8.	Bạn muốn biết mình còn bao nhiêu nội dung nữa mới đọc xong.
9.	Bạn thấy các công cụ hỗ trợ đọc hiện có (Kindle, Bionic Reading, v.v.) chưa thực sự giải quyết được vấn đề tập trung của bạn.
10.	Bạn muốn đọc lại một đoạn văn yêu thích trong một tác phẩm đã đọc nhưng không tìm lại được đoạn đó.

Theo dự kiến cần từ 40% người dùng chọn câu trả lời là thang 4-5 là đạt chỉ tiêu để chỉ ra tính thực tế và cần thiết của dự án này.
Dựa theo mẫu 9 câu trả lời thu thập được ta có các biểu đồ chính quan trọng là nền tảng để phát triển các chức năng về sau như dưới đây:

![Picture3](https://lh3.googleusercontent.com/d/12BxrafWm9H2TV7h6VGq6whceBY4naCfd)
![Picture5](https://lh3.googleusercontent.com/d/1Toh9dtMmqAh5BkDxKYR8a0XjwTB9x2Pc)
![Picture6](https://lh3.googleusercontent.com/d/15WbdTE4pmRqQAV5MsrW0kTOay9bsFA_U)
![Picture9](https://lh3.googleusercontent.com/d/1qu7GoV4roz51jPpqNdaVC3X-DJRG45bK)

➔Từ những biểu đồ ở trên ta có thể nói rằng nhu cầu cần tập trung của người dùng là rất quan trọng và từ đó sinh ra chức năng cốt lỗi của hệ thống đó chính là Focus Window chỉ tập trung vào nội dung ở giữa và làm mờ đi phần trên và phần dưới.

![Picture7](https://lh3.googleusercontent.com/d/17CfmYtlD8m92oR8_zS-DfkassuX3bbmF)

➔Không cần chú trọng thêm vào phần này nhưng có thể tối ưu trải nghiệm cho người dùng bằng cách cho phép họ điều chỉnh font chữ, kiểu chữ, màu nền,…..

![Picture8](https://lh3.googleusercontent.com/d/1clcJdSgpFvrJwDQY6V4o7brZxkXrWing)

➔Thêm tính năng hiển thị thanh tiến trình cho người dùng có cảm giác đạt được thành tụ

![Picture10](https://lh3.googleusercontent.com/d/19tW5JlFvJkyEuQ4R66EWuciuPXGv2LCN)

➔Thêm tính năng lưu chương, đoạn, trang… yêu thích


**Một số câu hỏi chính khi phỏng vấn**

Bạn hay đọc loại tài liệu gì nhất trong tuần vừa rồi? (giáo trình, tin tức, mạng xã hội, tài liệu công việc...)
Ứng dụng/trang web đọc nào bạn thấy khó chịu nhất khi dùng? Vì sao?
Kể cho mình nghe lần gần nhất bạn đọc một bài dài mà bị mất tập trung — chuyện gì đã xảy ra?
Bạn có dùng công cụ/app nào để giúp mình tập trung khi đọc không? Nó giúp được gì, và còn thiếu gì?



### 3.3. Thiết kế giao diện & tương tác

**Site map:**
```
ReadPace/
├── Onboarding (đo tốc độ đọc nền/calibration ban đầu)
├── Homepage (Thư viện + danh mục yêu thích)
├── Reading View  ← Màn hình lõi
│   ├── Auto-scroll engine (tốc độ cá nhân hoá)
│   └── Focus Window (blur phần trên/dưới, giữ rõ 2-3 dòng đang đọc)
├── Library (chương/đoạn đã lưu, sách yêu thích)
└── Settings (tốc độ cuộn, font, cỡ chữ, màu nền)
```

**Luồng tương tác giữa các màn hình:**
Onboarding → Homepage → chọn sách → Reading View ⇄ Settings (tinh chỉnh tốc độ/hiển thị) → Reading View → Save → Library

Bản MVP tập trung vào desktop/web vì cơ chế cuộn và focus dễ kiểm soát hơn với chuột/trackpad. Phiên bản mobile là hướng mở rộng, không nằm trong phạm vi chính do khác biệt về input (chạm vs. chuột) ảnh hưởng đến cơ chế tự cuộn.

### 3.4. Công cụ thiết kế

Nhóm chọn **Figma** làm công cụ wireframe/mockup chính.

| Tiêu chí | Đánh giá |
|---|---|
| Hiện đại/thô sơ | Hiện đại, hỗ trợ prototyping tương tác tốt |
| Đẹp/xấu | Giao diện sạch, dễ tạo design system nhất quán |
| Nhanh/chậm | Nhanh cho wireframe tĩnh và luồng chuyển màn hình cơ bản |
| Ưu điểm | Cộng tác realtime giữa 4 thành viên, thư viện component, Smart Animate mô phỏng chuyển động |
| Nhược điểm | Không mô phỏng được hiệu ứng blur động theo scroll thời gian thực — đây là cơ chế lõi của ReadPace |

Cơ chế auto-scroll và focus window động sẽ được dựng bằng prototype code (HTML/CSS/JS) riêng để phục vụ user testing; Figma chỉ dùng cho wireframe tĩnh và luồng màn hình.

### 3.5. Tiêu chí thành công đo lường được
*(Chưa có dữ liệu, sẽ bổ sung sau khi có kết quả phỏng vấn/khảo sát baseline)*

### 3.6. Kế hoạch kiểm thử

Thiết kế A/B: cùng một đoạn văn, đọc có/không có ReadPace, đo các chỉ số ở mục 3.5. Cơ chế theo dõi chính là log hành vi cuộn (scroll-behavior proxy) — đáng tin cậy, không cần phần cứng đặc biệt. Eye-tracking (WebGazer.js/MediaPipe) chỉ dùng như Wizard-of-Oz proof-of-concept phụ cho một nhóm nhỏ người test, không phải cơ chế sản phẩm chính thức.

### 3.7. Phân loại phạm vi tính năng

| Mức ưu tiên | Tính năng | Lý do |
|---|---|---|
| P0 — Lõi (bắt buộc, nộp giữa kỳ) | Auto-scroll cá nhân hoá + Focus Window (blur động) | Giải quyết trực tiếp vấn đề ở mục 1.2, là một cơ chế tích hợp duy nhất |
| P1 — Hỗ trợ (nếu đủ thời gian, nộp cuối kỳ) | Tuỳ biến font/cỡ chữ/màu nền (giới hạn màu an toàn cho mắt); Lưu chương/đoạn yêu thích | Đơn giản để triển khai, không xung đột với cơ chế lõi |
| P2 — Mở rộng (tương lai, không bắt buộc) | Micro-break prompts, Semantic progress bar theo khối ý | Cần thêm xử lý NLP để tách khối ý tự động — vượt phạm vi 11 tuần |

---

## 4. Lịch trình & phân công

| Tuần | Công việc | Kết quả kỳ vọng |
|---|---|---|
| 1 | Concept mapping, chốt vấn đề, lập kế hoạch | Plan.md nháp |
| 2 | Khảo sát state-of-the-art, phỏng vấn 5 end-users | Bảng so sánh SOTA + dữ liệu phỏng vấn |
| 3 | Phân tích affinity diagram, xây persona | Persona (ảnh) |
| 4 | Thiết kế site map, wireframe Figma cho P0 | Wireframe tĩnh |
| 5 | Hoàn thiện Plan.md, skill.md, slide, nộp giữa kỳ | Proposal package |
| 6–7 | Dựng prototype code cho auto-scroll + focus window | Prototype chạy được (P0) |
| 8 | User testing vòng 1 (A/B, đo SUS, log scroll) | Số liệu SUS/task completion vòng 1 |
| 9 | Điều chỉnh theo phản hồi, thêm P1 nếu kịp thời gian | Bản cải tiến |
| 10 | User testing vòng 2, quay video prototype | Video prototype, số liệu vòng 2 |
| 11 | Hoàn thiện báo cáo, slide, poster, code, nộp cuối kỳ | Full submission package |

**Phân vai trò nhóm (4 thành viên):**

| Vai trò | Nhiệm vụ chính |
|---|---|
| Quản lý nhóm / tài liệu | Tổng hợp Plan.md, skill.md, báo cáo, điều phối lịch họp |
| Thiết kế (UI/UX) | Wireframe Figma, site map, persona, chọn màu/font an toàn |
| Phát triển | Dựng prototype code (auto-scroll/focus window) |
| Kiểm định/kiểm thử | Thiết kế và chạy A/B test, thu thập và log dữ liệu |

---

## 5. Ước lượng kinh phí

| Hạng mục | Chi phí ước tính | Ghi chú |
|---|---|---|
| Công cụ thiết kế (Figma) | 0 VNĐ | Gói miễn phí đủ dùng cho 4 người |
| Công cụ dựng prototype (HTML/CSS/JS) | 0 VNĐ | Mã nguồn mở |
| WebGazer.js (Wizard-of-Oz PoC phụ) | 0 VNĐ | Thư viện mã nguồn mở |

**Tổng ước tính: 0 VNĐ** (chỉ dùng công cụ miễn phí)

---

## 6. Liên kết với skill.md

skill.md mô tả quy trình nhóm đã dùng để tạo ra Plan.md này (bước 1 dùng concept mapping từ các ý tưởng ban đầu, bước 2 áp dụng Diverge-Converge để chọn vấn đề, bước 3 khảo sát SOTA...), không lặp lại nội dung của Plan.md.
