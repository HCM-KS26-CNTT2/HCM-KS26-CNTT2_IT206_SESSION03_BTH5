# [Bài thực hành 5] Phân loại phản hồi của khách hàng
### THIẾT KẾ HAI PROMPT THỰC THI
```
--- PROMPT 1: ZERO-SHOT PROMPT ---
Bạn là trợ lý AI chuyên phân tích dữ liệu chăm sóc khách hàng.
Hãy phân loại các phản hồi của khách hàng dưới đây thành 3 nhãn: "Tích cực", "Tiêu cực", hoặc "Yêu cầu hỗ trợ".
Danh sách phản hồi cần phân loại:
1. "Sản phẩm đẹp, giao hàng nhanh, rất hài lòng."
2. "Tôi đã đặt hàng 5 ngày nhưng chưa nhận được."
3. "Tai nghe không kết nối được Bluetooth."
4. "Nhân viên tư vấn rất nhiệt tình."
5. "Tôi muốn hoàn tiền vì sản phẩm bị lỗi."
```
```
--- PROMPT 2: FEW-SHOT PROMPT ---
Bạn là chuyên gia phân loại dữ liệu trải nghiệm khách hàng với độ chính xác tuyệt đối.
Hãy phân loại các phản hồi của khách hàng thành 3 nhãn chuẩn xác: "Tích cực", "Tiêu cực", hoặc "Yêu cầu hỗ trợ".

Examples:
- Input: "Máy dùng rất tốt, pin trâu, đáng tiền." -> Nhãn: Tích cực | Lý do: Khách hàng khen ngợi sản phẩm.
- Input: "Chất lượng dịch vụ quá tệ, nhân viên thái độ kém." -> Nhãn: Tiêu cực | Lý do: Khách hàng phàn nàn về dịch vụ.
- Input: "Hướng dẫn giúp tôi cách kết nối thiết bị với điện thoại." -> Nhãn: Yêu cầu hỗ trợ | Lý do: Khách hàng cần giải quyết vấn đề kỹ thuật cụ thể.

Danh sách phản hồi cần phân loại thực tế:
1. "Sản phẩm đẹp, giao hàng nhanh, rất hài lòng."
2. "Tôi đã đặt hàng 5 ngày nhưng chưa nhận được."
3. "Tai nghe không kết nối được Bluetooth."
4. "Nhân viên tư vấn rất nhiệt tình."
5. "Tôi muốn hoàn tiền vì sản phẩm bị lỗi."
```
### KẾT QUẢ ĐẦU RA (DẠNG BẢNG SO SÁNH)

| STT | Phản hồi | Nhãn phân loại | Lý do |
| :---: | :--- | :--- | :--- |
| **1** | "Sản phẩm đẹp, giao hàng nhanh, rất hài lòng." | Tích cực | Khách hàng bày tỏ sự hài lòng và khen ngợi chất lượng sản phẩm, dịch vụ. |
| **2** | "Tôi đã đặt hàng 5 ngày nhưng chưa nhận được." | Yêu cầu hỗ trợ | Phản hồi nêu rõ vấn đề đơn hàng trễ hạn cần cửa hàng kiểm tra và xử lý gấp. |
| **3** | "Tai nghe không kết nối được Bluetooth." | Yêu cầu hỗ trợ | Khách hàng gặp sự cố kỹ thuật sản phẩm và cần bộ phận kỹ thuật hướng dẫn khắc phục. |
| **4** | "Nhân viên tư vấn rất nhiệt tình." | Tích cực | Khách hàng đánh giá cao và khen ngợi thái độ phục vụ của nhân viên tư vấn. |
| **5** | "Tôi muốn hoàn tiền vì sản phẩm bị lỗi." | Tiêu cực | Khách hàng không hài lòng do sản phẩm lỗi và đưa ra yêu cầu đổi trả/hoàn tiền. |

---------------------
### SO SÁNH KẾT QUẢ GIỮA ZERO-SHOT VÀ FEW-SHOT
- **Zero-shot Prompting:**
  + *Ưu điểm:* Nhanh chóng, không cần chuẩn bị trước các ví dụ phức tạp.
  + *Nhược điểm:* Với các câu phản hồi ranh giới (ví dụ như câu số 2 hoặc số 5), mô hình Zero-shot đôi khi nhầm lẫn giữa nhãn "Tiêu cực" và "Yêu cầu hỗ trợ" do thiếu định nghĩa ngữ cảnh rõ ràng về mặt hành động.

- **Few-shot Prompting:**
  + *Ưu điểm vượt trội:* Độ chính xác và tính nhất quán cao hơn hẳn. Nhờ có các ví dụ mẫu (Examples), AI hiểu chính xác tiêu chí tách biệt giữa việc phàn nàn thông thường (Tiêu cực) với việc yêu cầu giải quyết một vấn đề cụ thể (Yêu cầu hỗ trợ), từ đó gắn nhãn cực kỳ chuẩn xác cho toàn bộ tập dữ liệu.