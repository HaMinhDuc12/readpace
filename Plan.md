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

![Picture1](https://lh3.googleusercontent.com/d/1ETTBlvUOdfypvyXO5qejbXj09v23gCi4)

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

<img src="https://lh3.googleusercontent.com/d/1RcjrWKg1Kr08VdQ4yXkx6X5FfhpkzkD5" width="70%" />
<img src="https://lh3.googleusercontent.com/d/19e6a8_4g77y6KDf19jn4QOZGyS4ZyEPs" width="70%" />
<img src="https://lh3.googleusercontent.com/d/1diTEpvjiL884Ego1BMu__l1Fj1cZz5Rz" width="70%" />

➔Đa số người dành thời gian cho việc đọc nhất hiện nay là sinh viên, và số lượng người và tần suất bị mất tập trung khi đọc cũng không phải là quá thấp. Nên có thể coi đây là một vấn đề cần đầu tư để giải quyết chứ không thể bỏ qua.


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

<img src="https://lh3.googleusercontent.com/d/12BxrafWm9H2TV7h6VGq6whceBY4naCfd" width="70%" />
<img src="https://lh3.googleusercontent.com/d/1Toh9dtMmqAh5BkDxKYR8a0XjwTB9x2Pc" width="70%" />
<img src="https://lh3.googleusercontent.com/d/15WbdTE4pmRqQAV5MsrW0kTOay9bsFA_U" width="70%" />
<img src="https://lh3.googleusercontent.com/d/1qu7GoV4roz51jPpqNdaVC3X-DJRG45bK" width="70%" />

➔Từ những biểu đồ ở trên ta có thể nói rằng nhu cầu cần tập trung của người dùng là rất quan trọng và từ đó sinh ra chức năng cốt lỗi của hệ thống đó chính là Focus Window chỉ tập trung vào nội dung ở giữa và làm mờ đi phần trên và phần dưới.

<img src="https://lh3.googleusercontent.com/d/17CfmYtlD8m92oR8_zS-DfkassuX3bbmF" width="70%" />

➔Không cần chú trọng thêm vào phần này nhưng có thể tối ưu trải nghiệm cho người dùng bằng cách cho phép họ điều chỉnh font chữ, kiểu chữ, màu nền,…..

<img src="https://lh3.googleusercontent.com/d/1clcJdSgpFvrJwDQY6V4o7brZxkXrWing" width="70%" />

➔Thêm tính năng hiển thị thanh tiến trình cho người dùng có cảm giác đạt được thành tụ

<img src="https://lh3.googleusercontent.com/d/19tW5JlFvJkyEuQ4R66EWuciuPXGv2LCN" width="70%" />

➔Thêm tính năng lưu chương, đoạn, trang… yêu thích


**Một số câu hỏi chính khi phỏng vấn**

Bạn hay đọc loại tài liệu gì nhất trong tuần vừa rồi? (giáo trình, tin tức, mạng xã hội, tài liệu công việc...)
Ứng dụng/trang web đọc nào bạn thấy khó chịu nhất khi dùng? Vì sao?
Kể cho mình nghe lần gần nhất bạn đọc một bài dài mà bị mất tập trung — chuyện gì đã xảy ra?
Bạn có dùng công cụ/app nào để giúp mình tập trung khi đọc không? Nó giúp được gì, và còn thiếu gì?



### Observe

Trong phương pháp “Observe” ta dùng cách “Ethnography” đối tượng được ưu tiên quan sát sẽ là sinh viên đại học năm ba vì theo khảo sát thì sinh viên là nhóm người dùng có số lượng đông nhất:

**TH 1**: 
- Đối tượng L mở một website tài liệu chuyên ngành tiếng Anh. Đồng thời, thanh điều hướng (tab bar) của trình duyệt hiển thị các ứng dụng giải trí và liên lạc khác như Facebook, YouTube và ChatGPT.
- Sau trung bình 8–10 phút đọc tài liệu, đối tượng có xu hướng chuyển sang tab Facebook để kiểm tra thông báo. Khi quay lại tab tài liệu, đối tượng mất từ 15–20 giây dùng con trỏ chuột quét (highlight) lại từ đầu đoạn văn để định vị vị trí đang đọc dở. Biểu cảm khuôn mặt thể hiện sự bối rối và đối tượng phải đọc lại toàn bộ đoạn văn đó từ đầu.
- Sự xao nhãng từ môi trường số làm đứt gãy luồng tư duy. Người dùng mất nhiều thời gian và nhận thức để tái định vị vị trí và hiểu lại văn bản sau khi bị ngắt quãng.

➔ReadPace thật sự cần thiết để hỗ trợ cho sinh viên đọc văn bản tốt hơn và hiệu suất học tập cao hơn 

**TH 2**: 
- Đối tượng V sử dụng ChatGPT và Gemini để tra cứu các khái niệm mới. Đối tượng tương tác rất nhanh, đọc lướt qua các đoạn văn bản có định dạng in đậm, in nghiêng hoặc danh sách dạng thẻ do AI tạo ra.
- Khi gặp các câu hỏi chuyên sâu, đối tượng click vào các đường link tài liệu gốc do AI cung cấp. Ngay khi giao diện trang web mới hiện ra với mật độ chữ dày đặc (bản văn xuôi dài, không có định dạng đặc biệt), đối tượng có hành vi cuộn chuột nhanh từ trên xuống dưới, dừng lại không quá 5 phút và nhanh chóng tắt tab.
- Người dùng đã quen với kiểu hiển thị thông tin ngắn, có phân cấp thị giác từ AI. Khi đối mặt với tài liệu truyền thống có mật độ chữ dày, họ gặp hội chứng "ngại đọc" và có xu hướng bỏ cuộc trước khi tìm thấy thông tin cần thiết.

➔Vẫn cần một ứng dụng chuyên dụng để đọc tài liệu

### 3.3. Danh sách chức năng dự kiến

Dựa trên các rào cản về mặt nhận thức và thị giác đã phát hiện ở giai đoạn khám phá người dùng (User Discovery), hệ thống **ReadPace** định hình các nhóm chức năng cốt lõi nhằm tối ưu hóa trải nghiệm đọc tài liệu số trên nền tảng Web/Desktop. Các chức năng được phân loại cụ thể bao gồm:

### 3.3.1. Nhóm chức năng cốt lõi hỗ trợ hành vi đọc (Core Reading Features)

* **Chế độ tự động cuộn cá nhân hóa (Adaptive Auto-scroll Engine):**
    * *Mô tả:* Giải quyết áp lực thao tác vật lý liên tục (cuộn chuột/trackpad) khi người dùng xử lý các văn bản dài. Hệ thống tự động cuộn màn hình theo dòng chảy của văn bản để người dùng tập trung hoàn toàn vào việc tiếp nhận thông tin.
    * *Cơ chế tương tác:* Người dùng có thể tùy chỉnh tốc độ cuộn thủ công thông qua phím tắt hoặc thanh trượt. Đồng thời, hệ thống tự động ghi nhận tốc độ đọc nền (WPM - Words Per Minute) ở bước Onboarding và hành vi đọc thực tế của từng người để tự động tinh chỉnh tốc độ cuộn phù hợp, tạo ra trải nghiệm trượt cá nhân hóa.
* **Cửa sổ lấy nét thị giác (Focus Window):**
    * *Mô tả:* Tạo ra hiệu ứng "Spotlight" nhằm giảm thiểu tối đa hiện tượng nhiễu thị giác và giải quyết triệt để vấn đề mất dấu vị trí đọc dở khi người dùng bị ngắt quãng (như trường hợp xao nhãng do chuyển tab).
    * *Cơ chế tương tác:* Hệ thống sẽ làm mờ (blur) hoặc giảm độ tương phản của phần văn bản phía trên và phía dưới, chỉ giữ lại sự rõ nét và độ sáng chuẩn xác tại vùng trung tâm chứa từ 2 đến 3 dòng văn bản mà người dùng đang đọc.
* **Ngắt đoạn thông minh và Điểm nghỉ vi mô (Smart Chunking & Micro-break Prompts):**
    * *Mô tả:* Giảm hội chứng "ngại đọc" và quá tải thông tin khi đối mặt với các khối văn bản có mật độ chữ dày đặc.
    * *Cơ chế tương tác:* Dựa trên thuật toán phân tích độ dài đoạn văn và thời gian đọc liên tục, UI sẽ tự động tính toán để chèn các khoảng dừng thị giác ngắn (khoảng 3 giây "thở" - micro-breaks) tại các điểm ngắt ý tự nhiên (kết thúc một phân đoạn, không ngắt giữa câu). Điều này giúp não bộ có thời gian cô đọng kiến thức trước khi tiếp tục.
 * **Up file để định dạng đọc (Upload the file to a readable format):**
    * *Mô tả:* Cho phép người dùng up file text thô để dùng các chức năng của ứng dụng để hỗ trợ đọc.
    * *Cơ chế tương tác:* Dựa trên thuật toán phân tích độ dài đoạn văn và các dấu câu để tự động định dạng lại file ban đầu(ngắt đoạn, dãn đoạn, kiểu chữ, cỡ chữ) đồng thời cho phép sử dụng chức năng “Focus windown” để người dùng đọc dễ hơn.


### 3.3.2. Nhóm chức năng điều hướng và Cấu trúc nội dung (Navigation & Structure)

* **Thanh tiến trình ngữ nghĩa (Semantic Progress Bar):**
    * *Mô tả:* Thay thế cho các thanh tiến trình hiển thị phần trăm (%) từ đó củng cố tâm lý kiểm soát (Locus of Control) cho người đọc.
    * *Cơ chế tương tác:* Thanh tiến trình được thiết kế trực quan, phân chia rõ ràng theo từng "khối ý chính" hoặc phân đoạn nội dung của bài viết. Người dùng có thể nhìn vào để biết mình đang ở phân đoạn kiến thức nào và cấu trúc tổng thể của tài liệu ra sao.

### 3.3.3. Nhóm chức năng Quản lý cá nhân (Library & Personalization)

* **Lưu trữ phân đoạn và Chương sách (Granular Bookmarking & Library):**
    * *Mô tả:* Đáp ứng nhu cầu tái định vị nhanh các kiến thức quan trọng hoặc các đoạn văn tâm đắc để phục vụ cho việc tra cứu, nghiên cứu sau này.
    * *Cơ chế tương tác:* Tích hợp các shortcut/icon trực quan ngay bên cạnh văn bản cho phép người dùng click để lưu nhanh một chương cụ thể hoặc chỉ một đoạn văn ngắn vào "Tủ sách cá nhân" (Library).
* **Danh mục yêu thích (Favorites Categorization):** * *Mô tả:* Hệ thống cung cấp không gian riêng để người dùng lưu trữ toàn bộ các đầu truyện, tài liệu lớn vào danh mục yêu thích tại giao diện Homepage để truy cập nhanh.
* **Tùy biến hiển thị tối ưu thị giác (Visual Customization):**
    * *Mô tả:* Giảm mỏi mắt (Visual Fatigue) khi phải tương tác với màn hình máy tính trong thời gian dài.
    * *Cơ chế tương tác:* Cho phép người dùng linh hoạt điều chỉnh phông chữ (Fonts dành riêng cho việc đọc chuyên dụng), cỡ chữ và màu nền. Nhóm nghiên cứu giới hạn bộ lọc màu nền trong các gam màu đã được chứng minh khoa học là thân thiện và an toàn cho mắt (như màu Sepia, Dark mode tiêu chuẩn, hoặc nền mờ giảm ánh sáng xanh).

### 3.4. Thiết kế giao diện & tương tác

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

### 3.5. Công cụ thiết kế

Nhóm chọn **Figma** làm công cụ wireframe/mockup chính.

| Tiêu chí | Đánh giá |
|---|---|
| Hiện đại/thô sơ | Hiện đại, hỗ trợ prototyping tương tác tốt |
| Đẹp/xấu | Giao diện sạch, dễ tạo design system nhất quán |
| Nhanh/chậm | Nhanh cho wireframe tĩnh và luồng chuyển màn hình cơ bản |
| Ưu điểm | Cộng tác realtime giữa 4 thành viên, thư viện component, Smart Animate mô phỏng chuyển động |
| Nhược điểm | Không mô phỏng được hiệu ứng blur động theo scroll thời gian thực — đây là cơ chế lõi của ReadPace |

Cơ chế auto-scroll và focus window động sẽ được dựng bằng prototype code (HTML/CSS/JS) riêng để phục vụ user testing; Figma chỉ dùng cho wireframe tĩnh và luồng màn hình.

### 3.6. Tiêu chí thành công đo lường được
*(Chưa có dữ liệu, sẽ bổ sung sau khi có kết quả phỏng vấn/khảo sát baseline)*

### 3.7. Kế hoạch kiểm thử

Thiết kế A/B: cùng một đoạn văn, đọc có/không có ReadPace, đo các chỉ số ở mục 3.5. Cơ chế theo dõi chính là log hành vi cuộn (scroll-behavior proxy) — đáng tin cậy, không cần phần cứng đặc biệt. Eye-tracking (WebGazer.js/MediaPipe) chỉ dùng như Wizard-of-Oz proof-of-concept phụ cho một nhóm nhỏ người test, không phải cơ chế sản phẩm chính thức.

### 3.8. Phân loại phạm vi tính năng

| Mức ưu tiên | Tính năng | Lý do |
|---|---|---|
| P0 — Lõi| Auto-scroll cá nhân hoá + Focus Window (blur động) | Giải quyết trực tiếp vấn đề ở mục 1.2, là một cơ chế tích hợp duy nhất |
| P1 — Hỗ trợ | Tuỳ biến font/cỡ chữ/màu nền (giới hạn màu an toàn cho mắt); Lưu chương/đoạn yêu thích | Đơn giản để triển khai, không xung đột với cơ chế lõi |
| P2 — Mở rộng| Micro-break prompts, Semantic progress bar theo khối ý | Cần thêm xử lý NLP để tách khối ý tự động — vượt phạm vi 11 tuần |

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
