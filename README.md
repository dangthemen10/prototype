# Đề Xuất Chiến Lược Tái Thiết Kế UI/UX & Tích Hợp AI Cho Yahoo! Net Bokin

**Mục tiêu cốt lõi:** Chuyển đổi `donation.yahoo.co.jp` từ một cổng danh mục quyên góp truyền thống thành một nền tảng thiện nguyện thông minh, cá nhân hóa cao, tối đa hóa **tỷ lệ người dùng quay lại (Retention)** và **giá trị quyên góp trọn đời (LTV)**.

---

## 1. Bối Cảnh & Giải Phẫu Vấn Đề Hiện Tại (Pain Points)

Để thành công tại thị trường Nhật Bản, thiết kế cần giải quyết 3 rào cản tâm lý cốt lõi của người quyên góp (Donor): **Sự tin cậy (Trust), Tính minh bạch (Transparency), và Sự gắn kết cảm xúc (Emotional Connection)**.

* **Quá tải thông tin (Information Overload):** Giao diện hiện tại liệt kê quá nhiều dự án theo dạng danh sách chữ dày đặc, dễ gây "tê liệt lựa chọn" (Choice Paralysis).
* **Thiếu tính cá nhân hóa:** Mọi người dùng đều thấy cùng một giao diện tĩnh, không phân biệt người dùng mới hay người đã quyên góp nhiều lần.
* **Trải nghiệm mang tính "một lần" (Transactional):** Quyên góp xong là kết thúc quy trình. Người dùng thiếu động lực quay lại kiểm tra xem số tiền của mình đã tạo ra tác động thực tế gì.

---

## 2. Các Trụ Cột Tích Hợp AI (AI-Driven UX)

### A. AI Matching & Smart Feed (Cá nhân hóa trang chủ)
* **Dành riêng cho bạn (AI Pick):** Sử dụng dữ liệu từ hệ sinh thái Yahoo! JAPAN (lịch sử quyên góp, khu vực sinh sống, chủ đề hay đọc trên Yahoo! News, cảnh báo thời tiết từ Yahoo! Weather/Disaster) để đề xuất 3–5 dự án phù hợp nhất ngay đầu trang.
* **AI Empathy Summary (Tóm tắt chạm cảm xúc):** Tích hợp nút *"Tóm tắt nhanh bằng AI"* trên từng thẻ dự án, rút gọn các mô tả dài dòng thành 3 gạch đầu dòng súc tích:
  1. *Chuyện gì đang xảy ra?*
  2. *Số tiền sẽ dùng làm gì?*
  3. *Tại sao cần gấp ngay bây giờ?*

### B. AI Impact Simulator (Trực quan hóa tác động trước khi bấm nút)
* **Thanh trượt tương tác thời gian thực:** Xóa bỏ tâm lý *"100 yên hay 500 yên của mình thì thấm vào đâu"*. Khi người dùng kéo thanh chọn số tiền, giao diện lập tức dịch con số đó thành giá trị thực tế kèm hình ảnh minh họa.
  * *Ví dụ:* Thay vì chỉ hiển thị `¥1,500`, giao diện hiển thị: **"¥1,500 = 3 bữa ăn nóng hổi giàu dinh dưỡng cho trẻ em vùng lũ"**.

### C. AI Impact Storytelling (Vòng lặp kéo người dùng quay lại)
* **Thẻ cập nhật tự động (Impact Stories):** AI tổng hợp hình ảnh thực địa và hóa đơn giải ngân từ các tổ chức NPO để tạo thành các bản tin ngắn dạng Story (tương tự Instagram/LINE VOOM), gửi thông báo qua ứng dụng Yahoo! hoặc LINE.
* **Hành trình đồng tiền của bạn (My Impact Timeline):** Khi quay lại trang chủ, người dùng thấy ngay tổng tác động tích lũy của bản thân (ví dụ: *14 bữa ăn đã trao, 3 cây xanh đã trồng*).

---

## 3. Tối Ưu Hóa Chuyển Đổi & Cơ Chế Giữ Chân (Conversion & Retention)

### A. Quyên góp "1-Chạm" với hệ sinh thái điểm thưởng
* **Point-Sweeping (Quét điểm sắp hết hạn):** Tích hợp sâu với **PayPay** và **V-Point**. Hiển thị thẻ nổi bật ngay đầu trang: *"Bạn đang có 340 điểm sắp hết hạn — Quyên góp ngay chỉ với 1 chạm"*. Loại bỏ hoàn toàn cảm giác "tiêu tiền mặt".
* **Smart Auto-Roundup (Làm tròn tự động):** Cho phép người dùng bật tính năng tự động trích phần tiền lẻ (ví dụ: 10–50 yên) khi thanh toán qua PayPay hoặc mua sắm trên Yahoo! Shopping.

### B. Thiết kế lại thẻ dự án theo hướng Visual-First & Tâm lý học
* **Thanh tiến độ cột mốc (Milestone Progress Bar):** Làm nổi bật các cột mốc ngắn hạn sắp đạt được (ví dụ: *"Chỉ còn thiếu ¥18,500 để đạt mốc 100 túi cứu trợ đợt 2"*) để kích thích tâm lý muốn làm "người chốt hạ".
* **Huy hiệu minh bạch (Trust Badges):** AI kiểm duyệt hồ sơ và gắn nhãn trực quan (*"100% đến hiện trường"*, *"Đã kiểm toán tài chính"*).

### C. Gamification đậm chất văn hóa Nhật Bản
* **Hộ chiếu Thiện nguyện (Digital Goshuin Stamp Rally):** Mỗi lần quyên góp theo từng chủ đề (Thiên tai, Trẻ em, Động vật, Môi trường...), người dùng sưu tầm được một con dấu kỹ thuật số (Tem Goshuin) để mở khóa huy hiệu *Đại sứ Nhân ái*.
* **Góp tự động khi có thiên tai (Auto-Disaster Pledge):** Người dùng cài đặt trước mức trần (ví dụ: ¥500/tháng). Khi hệ thống Yahoo! Disaster AI phát tín hiệu động đất/bão lớn, hệ thống tự động kích hoạt quyên góp khẩn cấp.

---

## 4. Phác Thảo Wireframe Cấu Trúc Trang Chủ Mới

| Thứ tự | Khu vực (Section) | Nội dung & Chức năng chính | Mục tiêu UX |
| :--- | :--- | :--- | :--- |
| **1** | **Urgent AI Disaster Radar** | Cảnh báo thiên tai khẩn cấp theo thời gian thực kèm thanh tiến độ cột mốc gần nhất. | Đánh vào tính cấp bách (Urgency). |
| **2** | **Hero Impact & 1-Tap Points** | Thống kê tác động tích lũy cá nhân + Nút quyên góp 1-chạm bằng điểm PayPay / V-Point sắp hết hạn. | Kích hoạt niềm tự hào & chốt đơn 0 rào cản. |
| **3** | **My Impact Stories** | Vòng tròn cập nhật tiến độ thực tế từ các quỹ người dùng từng hỗ trợ. | Xây dựng niềm tin & kéo user quay lại. |
| **4** | **AI Impact Simulator** | Thanh trượt chọn mức tiền quy đổi trực tiếp thành hiện vật/tác động thực tế. | Tăng giá trị trung bình mỗi lần góp (AOV). |
| **5** | **AI Pick Cho Bạn** | Danh sách thẻ dự án trực quan được AI chọn lọc theo sở thích, kèm nút tóm tắt 30 giây. | Giảm quá tải lựa chọn, tăng tỷ lệ nhấp. |
| **6** | **Impact Passport** | Bộ sưu tập tem Goshuin kỹ thuật số & nút bật/tắt chế độ góp tự động khi có thiên tai. | Duy trì thói quen & chuỗi đóng góp dài hạn. |

---

## 5. Đánh Giá Khả Thi & Kiến Trúc Triển Khai Kỹ Thuật

| Tính năng | Phương án triển khai kỹ thuật | Mức độ khả thi | Lưu ý vận hành |
| :--- | :--- | :---: | :--- |
| **AI Matching & Smart Feed** | Kết hợp dữ liệu hành vi Yahoo! ID lưu dưới dạng vector embedding (Redis/Qdrant). Dùng mô hình xếp hạng kết hợp LLM tinh gọn (AWS Bedrock vùng Japan). | **Rất cao** | Tận dụng được hạ tầng Big Data sẵn có của Yahoo! JAPAN. |
| **AI Impact Simulator** | Xử lý 100% ở Front-end (React/Next.js) dựa trên bảng hệ số quy đổi JSON do từng dự án cấu hình sẵn ở Back-end. | **Cao tuyệt đối** | Độ trễ bằng 0 khi kéo thanh trượt, không tốn chi phí gọi API AI real-time. |
| **AI Empathy Summary** | Dùng tác vụ chạy ngầm (Celery worker) gọi LLM tóm tắt ngay khi dự án được đăng tải và lưu tĩnh vào MySQL. | **Cao** | Tiết kiệm chi phí token và đảm bảo tốc độ tải trang nhanh. |
| **Impact Stories & NPO Portal** | Xây dựng ứng dụng di động siêu tối giản cho NPO chụp ảnh gửi báo cáo; AI tự động kiểm duyệt hình ảnh và dàn trang thành Story. | **Trung bình - Cao** | **Yếu tố quyết định:** Nhân sự các tổ chức NPO tại Nhật thường lớn tuổi, cần giao diện đăng bài đơn giản như LINE. |
| **1-Tap Point Sweeping** | Tích hợp SDK nội bộ của PayPay API và V-Point API với cơ chế tokenization cho các giao dịch vi mô (micro-transactions). | **Cao** | Phụ thuộc vào quy trình phê duyệt bảo mật nội bộ của hệ sinh thái PayPay/Yahoo!. |

---

## 6. Hiểu Rõ Đối Tác: Vai Trò Của NPO Tại Nhật Bản

* **NPO (Non-Profit Organization - Tổ chức phi lợi nhuận):** Tại Nhật Bản được quản lý chặt chẽ theo Luật NPO (*特定非営利活動法人*), hoạt động trong 20 lĩnh vực công ích và tái đầu tư 100% nguồn thu cho sứ mệnh xã hội.
* **Chiến lược hai chiều:** Để người quyên góp (Donor) nhận được các cập nhật minh bạch và sinh động, hệ thống cần đồng thời giải phóng sức lao động cho NPO bằng cách để AI đảm nhận khâu biên tập nội dung, tóm tắt báo cáo tài chính và tạo thẻ cập nhật tiến độ tự động.
