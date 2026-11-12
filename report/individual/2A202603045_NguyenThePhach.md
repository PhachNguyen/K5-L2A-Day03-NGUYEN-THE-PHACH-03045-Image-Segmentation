# Báo cáo thực hành Day 3 — điền trực tiếp trong fork của bạn

**Cách dùng:** Thay mọi dấu `…` bằng bài làm thật của bạn trước khi nộp link fork trên [LMS](https://aithucchien.vinuni.edu.vn). Giữ nguyên bốn mục và bảng để coach đọc nhanh. Viết ngắn, cụ thể theo ảnh/vùng; không cần thuật ngữ chuyên sâu. Ví dụ trong [hướng dẫn mẫu](../../reports/REPORT_TEMPLATE.md) chỉ giúp hiểu cách điền, không phải câu trả lời để chép lại.

- Mã học viên theo lớp: 2A202603045
- Ngày / CVAT local: 2026-11-11 / CVAT local
- Công cụ đã dùng: CVAT để import/export và kiểm tra mask; mask gợi ý ban đầu được tạo tự động bằng mô hình segmentation. Không có thông tin xác nhận về việc dùng Brush, Polygon hoặc SAM trong CVAT.

Mã học viên là mã lớp cấp; không cần ghi họ tên trong report nếu kênh [LMS](https://aithucchien.vinuni.edu.vn) đã nhận diện bạn. Chỉ ghi công cụ thật sự đã dùng; không có SAM vẫn làm bài bình thường.

## 1. Bài đã nộp

Ghi tên ZIP đúng như file trong `submissions/` và số ảnh đã vẽ, Save. Chưa làm hoặc export lỗi thì ghi `chưa có`, không tạo ZIP rỗng. Cột điểm là điểm tối đa của task, **không phải điểm tự chấm**.

| Task            | File ZIP đúng tên     | Hoàn thành mấy ảnh | Điểm tối đa (coach chấm sau) |
| --------------- | --------------------- | -----------------: | ---------------------------: |
| easy_semantic   | `easy_semantic.zip`   |              3 / 3 |                           20 |
| medium_instance | `medium_instance.zip` |              3 / 3 |                           32 |
| hard_panoptic   | `hard_panoptic.zip`   |              2 / 2 |                           30 |
| cp1_holes       | `cp1_holes.zip`       |              1 / 1 |                            3 |
| cp2_slice       | `cp2_slice.zip`       |              1 / 1 |                            3 |
| cp5_occlusion   | `cp5_occlusion.zip`   |              1 / 1 |                            3 |
| cp3_thin        | `cp3_thin.zip`        |              1 / 1 |                            3 |
| cp4_curb        | `cp4_curb.zip`        |              1 / 1 |                            3 |
| cp6_coverage    | `cp6_coverage.zip`    |              1 / 1 |                            3 |
| **Tổng tối đa** |                       |                    |                      **100** |

Nếu export lỗi, ghi task, dữ liệu đã Save đến đâu và lỗi đã báo coach.

Số ảnh trong bảng được đối chiếu theo mask trong các ZIP ở `submissions/`; bộ kiểm tra cấu trúc báo OK cho cả 9 ZIP. Việc này không xác nhận ranh giới mask đúng hoặc tự chứng minh thao tác Save trong CVAT.

## 2. Một quyết định trước khi dùng gợi ý

Chọn object đầu tiên bạn tự vẽ ở `medium_instance`, trước khi xem bất kỳ đề xuất tự động nào cho object đó. Ghi ảnh/vị trí đủ để tìm lại; “quy tắc biên” là lý do bạn chọn hoặc dừng mask ở ranh đó.

- Ảnh, vị trí và object Medium đầu tiên tự vẽ: Chưa có thông tin xác nhận trong ghi chép hiện tại. Các mask gợi ý tự động đã được tạo trước khi nhập vào CVAT; không ghi nhận rằng object đầu tiên được tự vẽ trước khi xem gợi ý.
- Class và quy tắc tôi dùng để chọn biên: Chưa được ghi nhận; cần bổ sung theo quyết định thực tế trong CVAT.
- Nếu dùng gợi ý sau đó: Đã dùng mask gợi ý tự động để khởi tạo các annotation; chưa có ghi chép xác nhận vùng nào đã sửa hoặc giữ.
- Nếu không dùng gợi ý: Không áp dụng; đã có mask gợi ý tự động trong quy trình này.

## 3. Một lỗi tôi tìm thấy và sửa

Chọn một lỗi **có thật** trong bài. Nếu công cụ lỗi khiến bạn chưa sửa được, ghi rõ đã thử gì và cần coach hỗ trợ gì; không ghi “đã sửa” khi chưa sửa.

- Task/ảnh/vùng: `cp3_thin`, ảnh `839f7736-abe28069.jpg`, toàn ảnh.
- Lỗi thuộc loại: Khác — lỗi tương thích khi import mask semantic.
- Bằng chứng tôi nhìn thấy: CVAT báo màu nền đen `(0,0,0)` chưa khai báo; sau khi thêm `background` vào `labelmap.txt`, CVAT báo nhãn `background` chưa đăng ký cho task. Task chỉ có `pole`, `traffic sign`, `sky`, `road`.
- Quy tắc và hành động sửa: Không đổi vùng nền thành một class khác. Đã bổ sung file danh sách ảnh `ImageSets/Segmentation/default.txt` và khai báo màu nền trong ZIP; lần import cuối vẫn báo task chưa có label `background`, nên cần coach xác nhận cách xử lý nền/nhãn phù hợp trước khi khẳng định lỗi đã được sửa.
- Sau sửa đã Save và export lại chưa? ZIP `cp3_thin.zip` hiện có trong `submissions/` và qua kiểm tra cấu trúc; chưa có bằng chứng xác nhận lần import cuối đã thành công hoặc annotation đã được Save lại trong CVAT.

Nếu bạn **đã xem Summary tự đánh giá trên GitHub Actions hoặc tự chạy script**, ghi ngắn một kết quả liên quan lỗi vừa sửa (ví dụ task, metric trước/sau nếu có): Chưa có điểm. Kiểm tra cấu trúc ZIP trên máy: cả 9 task không có lỗi hợp đồng; đây không phải điểm segmentation. Scorecard ba tier tối đa **82**, không phải điểm cuối trên 100. Không tự ghi PASS/top 3/bonus; người phụ trách xác nhận theo tiêu chí lớp. Không đưa file ground truth vào fork.

## 4. Ba ca chưa chắc hoặc đã cân nhắc

Mỗi ca là một **vùng cụ thể** khiến bạn phải cân nhắc hai cách hiểu. Ghi dấu hiệu nhìn thấy hoặc quy tắc đã dùng, rồi nêu quyết định hoặc câu hỏi cho coach. Không cần ba lỗi; ca đã quyết định được cũng hợp lệ.

| Ảnh/vị trí                                                 | Hai cách hiểu có thể                              | Quy tắc/chứng cứ                                                    | Quyết định hoặc câu hỏi cho coach                                                            |
| ---------------------------------------------------------- | ------------------------------------------------- | ------------------------------------------------------------------- | -------------------------------------------------------------------------------------------- |
| 1 — `cp3_thin`, ảnh `839f7736-abe28069.jpg`, pixel nền đen | Nền không thuộc class hay là nhãn `background`    | Task quy định 4 class; CVAT yêu cầu đăng ký `background` khi import | Không gán nền sang class khác; cần coach xác nhận cách import nền không tạo nhãn ngoài task. |
| 2 — `cp2_slice`, ảnh `000000017627.jpg`, hàng xe gần nhau  | Một vùng xe bị dính vào xe bên cạnh hay là hai xe | Quy tắc checkpoint: hai xe sát nhau vẫn là hai instance             | Khi rà soát, giữ mỗi xe thành một mask riêng; kiểm tra lại đường phân cách trong CVAT.       |
| 3 — `cp4_curb`, ảnh `7d83710e-4697c3b2.jpg`, dọc bó vỉa    | Pixel thuộc road hay sidewalk                     | Ranh dựa theo chức năng và bó vỉa, không chỉ theo màu/mặt asphalt   | Dùng mép bó vỉa làm ranh để rà soát; xác nhận lại vùng chuyển tiếp khó nhìn trong CVAT.      |

Các điểm ở mục 4 được ghi làm ca cần đối chiếu theo quy tắc task và lỗi import đã gặp; chỉ giữ chúng như trải nghiệm cá nhân nếu đúng là bạn đã thực sự cân nhắc các vùng này.
