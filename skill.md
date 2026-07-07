# skill.md — Quy trình thực hiện đồ án ReadPace

File này mô tả **quy trình (procedure)** nhóm đã và sẽ thực hiện qua từng giai đoạn của mô hình Diverge–Converge để tạo ra Plan.md, không lặp lại nội dung của Plan.md.

---

## Giai đoạn 1: Discovery

**Bước 1.** Cả nhóm cùng đọc lại ý tưởng gốc (readpace.docx) — bản mô tả liệt kê 7 tính năng đề xuất cho ReadPace.

**Bước 2.** Họp nhóm lần 1, thực hiện ánh xạ khái niệm (concept mapping) cho chủ đề "Việc đọc":
- Liệt kê các từ/khái niệm liên quan đến việc đọc.
- Nhóm các từ vào thể loại: Môi trường, Vật lý, Người, Kỹ năng đọc, Sách, Công cụ, Ngôn ngữ, Nội dung, Trạng thái đọc.
- Vẽ sơ đồ bằng drawio (`conceptual_mapping-Page-2_drawio.png`).

**Bước 3.** Đối chiếu sơ đồ concept map với 7 tính năng trong ý tưởng gốc, xác định nhánh nào của sơ đồ liên quan trực tiếp đến hiện tượng "mất chỗ đang đọc / đọc lại đoạn văn" — từ đó chốt **vấn đề nguyên tố** duy nhất cho đồ án (thay vì giữ nguyên 7 tính năng rời rạc).

**Bước 4.** Làm nổi bật (converge) các nhánh liên quan trực tiếp đến vấn đề đã chọn: Kỹ năng đọc (Sự tập trung, Tốc độ đọc), Vật lý (Thao tác tay, Khoảng cách mắt), Hình thức trình bày (Cỡ chữ, Kiểu chữ, Giãn cách chữ/dòng), Không Gian (Bị tác động), Trạng thái đọc (Chán, giác ngộ/say mê). Loại các nhánh không liên quan trực tiếp ra khỏi phạm vi đồ án.

**Bước 5.** Khảo sát state-of-the-art: tìm và so sánh 4 sản phẩm đọc hiện có (Microsoft Immersive Reader, BeeLine Reader, Speechify, Readwise) để xác định khoảng trống (gap) mà ReadPace có thể lấp đầy.

**Bước 6.** *(Chưa thực hiện)* Phỏng vấn 5 end-users theo tiêu chí đã xác định (người đọc thường xuyên ≥ 20–30 phút/ngày trên màn hình, tự nhận thấy hay mất chỗ đọc), phân tích affinity diagram, xây dựng persona (xuất file ảnh).

---

## Giai đoạn 2: Conception

**Bước 1.** *(Chưa thực hiện)* Brainstorm các phương án giải quyết vấn đề nguyên tố (auto-scroll, focus window, âm thanh nhắc, rung thiết bị...).

**Bước 2.** *(Chưa thực hiện)* Đánh giá và hội tụ về một cơ chế lõi duy nhất, dự kiến là kết hợp auto-scroll cá nhân hoá + focus window động.

**Bước 3.** *(Chưa thực hiện)* Phân loại các tính năng còn lại trong ý tưởng gốc theo mức ưu tiên P0/P1/P2 dựa trên mức độ liên quan đến vấn đề nguyên tố và tính khả thi trong 11 tuần.

---

## Giai đoạn 3: Prototyping

**Bước 1.** *(Chưa thực hiện)* Thiết kế site map và luồng tương tác giữa các màn hình.

**Bước 2.** *(Chưa thực hiện)* Dựng wireframe tĩnh bằng Figma cho các màn hình chính (Onboarding, Homepage, Reading View, Library, Settings).

**Bước 3.** *(Chưa thực hiện)* Dựng prototype code (HTML/CSS/JS) riêng cho cơ chế auto-scroll + focus window động, vì Figma không mô phỏng được hiệu ứng blur động theo thời gian thực.

---

## Giai đoạn 4: Evaluation

**Bước 1.** *(Chưa thực hiện)* Thiết kế kiểm thử A/B: cùng một đoạn văn, đọc có/không có ReadPace.

**Bước 2.** *(Chưa thực hiện)* Thu thập dữ liệu qua log hành vi cuộn (scroll-behavior), kết quả SUS, task completion rate.

**Bước 3.** *(Chưa thực hiện)* Thử nghiệm Wizard-of-Oz với eye-tracking (WebGazer.js) trên một nhóm nhỏ người test, làm bằng chứng bổ sung, không phải cơ chế chính thức.

**Bước 4.** *(Chưa thực hiện)* Tổng hợp kết quả, đối chiếu với tiêu chí thành công (mục 3.5 trong Plan.md), điều chỉnh cho vòng lặp tiếp theo nếu cần.

---

## Công cụ hỗ trợ trong quá trình thực hiện

| Công cụ | Mục đích sử dụng |
|---|---|
| drawio | Vẽ sơ đồ ánh xạ khái niệm |
| Figma | Wireframe, mockup, luồng màn hình |
| HTML/CSS/JS | Dựng prototype code cho cơ chế lõi (auto-scroll + focus window) |
| WebGazer.js | Wizard-of-Oz proof-of-concept phụ cho eye-tracking |
